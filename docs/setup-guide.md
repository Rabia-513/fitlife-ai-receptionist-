# Setup and export guide

## What was built
**Vapi → API Request Tool → n8n Webhook (POST) → Google Sheets Append Row → Respond to Webhook (JSON)**.

### n8n configuration
1. Create/open the workflow `TAW – Gym Membership – Vapi Lead Capture`.
2. Webhook node: `POST`, path `gym-membership-lead`, Authentication **Header Auth** with credential header name `X-API-Key`; Respond **Using Respond to Webhook Node**.
3. Add Google Sheets `Append row in sheet`: select `TAW – Gym Membership Leads` / `Gym_Leads` and map fields:
   - Timestamp: `{{ $now.toISO() }}`
   - Full Name: `{{ $json.body.name }}`
   - Phone: `{{ $json.body.phone }}`
   - Email: `{{ $json.body.email }}`
   - Membership Plan: `{{ $json.body.membership_plan }}`
   - Inquiry Type: `{{ $json.body.inquiry_type }}`
   - Lead Status: `New Lead`
   - Source: `Vapi Voice Agent`
4. Add `Respond to Webhook` node: JSON body `{"success":true,"message":"Lead saved successfully"}`, HTTP status 200. Confirm this only follows a successful Sheets operation.
5. **Publish** changes, then test once with fictional information.

### Vapi configuration
1. Create assistant `FitLife Gym Receptionist` with demo gym membership instructions and a conversational voice.
2. Create API Request tool `save_gym_lead`, with method `POST`, URL set to your n8n production webhook.
3. Request Body properties: `name`, `phone`, `membership_plan`, `inquiry_type` required strings; `email` optional string.
4. Create Vapi Custom Credential matching n8n `X-API-Key` Header Auth. Bearer prefix disabled. Keep secret in credential storage, not prompt/body/repository.
5. Under the tool's **Authorization** section select that credential; publish tool changes. Attach tool to assistant and publish assistant changes.
6. Test with fictional lead. Inspect the newest n8n execution (Webhook and Google Sheets nodes) and confirm row creation.

## Export actual n8n workflow
1. Open your workflow **Editor**.
2. Open the **workflow menu (three dots / ⋯)** in the editor's top bar, not the `Executions` tab.
3. Choose **Download**. n8n downloads the current workflow as `.json`.
4. Name it `gym-membership-n8n-workflow.json` on your computer.
5. **Review and sanitize the export before sharing:** it can expose credential labels/IDs, workbook IDs, node parameters and webhook paths. Never commit API keys, real caller details or private URLs.
6. Place a reviewed export in `workflows/`. If the downloaded JSON cannot be safely sanitized without breaking functionality, submit a clearly labeled redacted documentation version and keep original private.
7. A JSON export does **not** include usable credential secrets; credentials need to be reconnected after import.

## Export Vapi assistant / tool
Vapi supports version history exports in the Dashboard. Open an **Assistant**, click its version badge, open version history, and use **Export** for that version's JSON. For the API Request **Tool**, similarly open the tool version menu, **View Full History**, then **Export**. Review both JSON files for endpoints, IDs, customer data or sensitive configuration before sharing. You may instead supply redacted screenshots and setup instructions when an export isn't necessary.

## Google Sheets CRM template
Use `docs/crm-columns.csv` as a headers-only blank template. You may also download a scrubbed `.xlsx` from Google Sheets via **File → Download → Microsoft Excel** and put it in `docs/` after checking there is no real contact information.

## Before submission
- Check n8n's orange **Publish** button and publish final changes if outstanding.
- Perform an authenticated Vapi-to-n8n test with a fictional caller, inspecting webhook headers with values hidden.
- Format the Phone column as **Plain text** to preserve leading zero.
- Verify expected successful response and one CRM row per test.
- Add Loom URL and anonymized screenshots.
