# Project 3 verification checklist

- [x] Vapi FitLife Gym Receptionist created and browser voice response tested.
- [x] n8n POST webhook accepted PowerShell-generated fictional test JSON.
- [x] Google Sheets Append Row returned 1 successful item in test.
- [x] `save_gym_lead` API Request tool created and attached to published Vapi assistant.
- [x] A browser-call test was followed by new records in Google Sheets and successful n8n executions.
- [x] Vapi `X-API-Key` credential created with prefix disabled and assigned to tool.
- [ ] Verify newest POST was from Vapi, with n8n header authentication active, using a redacted execution detail screenshot.
- [ ] Confirm n8n editor's latest changes are **Published** and retest once.
- [ ] Verify actual `Respond to Webhook` response body and HTTP status.
- [ ] Format Google Sheets phone column as Plain text.
- [ ] Add n8n JSON export, sanitized to exclude account-specific information.
- [ ] Add assistant/tool export or sanitized configuration screenshots if allowed.
- [ ] Record Loom and paste video link in README.
- [ ] Verify no API keys, real client PII, email inboxes or hidden server URL credentials were committed.
- [ ] Push to assigned GitHub repository and submit official link.

**Note:** A green n8n run demonstrates workflow execution, but alone does not prove the new credential was used; check the relevant call/headers and publish state.
