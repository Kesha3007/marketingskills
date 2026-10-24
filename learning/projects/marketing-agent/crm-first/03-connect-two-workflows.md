# Step 2 — connect CRM tool to Main Agent

1. The main workflow `AI CRM | 01 - Main Agent` is already imported.
2. Create a **second** workflow named `AI CRM | 02 - Get Buyer`.
3. Download [02-get-keycrm-buyer.json](02-get-keycrm-buyer.json) using GitHub Raw → Save; import it into the new workflow. Don't overwrite the Main Agent.
4. Confirm the four nodes in the second workflow: `When executed by CRM Agent` → `Validate buyer ID` → `GET buyer from KeyCRM` → `Return minimal buyer summary`.
5. Create a KeyCRM API credential in n8n. In HTTP Request node: **Authentication: Generic Credential Type → Header Auth**. Set header name `Authorization` and value `Bearer <KEYCRM_API_KEY>` **inside n8n credentials only**. The API key must never go into GitHub, screenshots, the system prompt, or this chat.
6. Save the second workflow. Depending on the n8n version, publishing the sub-workflow might be required when used outside manual test mode.
7. Open the main workflow. In `Get KeyCRM Buyer Tool`: set **Source → Database**, choose the newly imported `AI CRM | 02 - Get Buyer`. Refresh the input schema and map the `buyer_id` field through `$fromAI`. If import shows invalid node parameters, configure them manually according to the installed n8n version.
8. Update **AI CRM Agent → System Message** using [system-prompt-en.md](system-prompt-en.md). The changed GitHub JSON is not automatically synced to the already imported n8n workflow.
9. Connect OpenAI credentials to OpenAI Chat Model. Save. Leave the chat private.
10. **Do not run or publish yet** if we are still agreeing permissions and retention. This step configures the workflow, not the real data connection test.

Security reminder: raw buyer data can appear in internal execution history between the HTTP Request and redaction node. Limit execution log retention and access; do not export execution data.

Official n8n tool workflow documentation: https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolworkflow/
