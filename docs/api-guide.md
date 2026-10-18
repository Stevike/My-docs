Markdown
# Wellhead API Guide

Welcome to the developer portal for the **Wellhead Telemetry System**. This guide outlines how to authenticate, fetch real-time sensor data, and handle error responses.

## Authentication
All requests to the Wellhead API must include a valid Bearer token in the HTTP header:

```bash
curl -X GET "[https://api.wellhead-docs.com/v1/sensors/telemetry?rig_id=Rig-Alpha-10](https://api.wellhead-docs.com/v1/sensors/telemetry?rig_id=Rig-Alpha-10)" \
     -H "Authorization: Bearer YOUR_API_KEY"
Endpoint Reference
Get Live Sensor Telemetry
URL: /v1/sensors/telemetry

Method: GET

Description: Returns real-time pressure and temperature metrics for downhole sensors.

Query Parameters
Parameter	Type	Required	Description
rig_id	string	Yes	The unique identifier of the drilling rig (e.g., Rig-Alpha-10).
Example Success Response (200 OK)
JSON
{
  "timestamp": "2026-10-18T02:00:00Z",
  "pressure_psi": 9850.5,
  "temperature_f": 185.2,
  "status": "OPTIMAL"
}
Rate Limits & Errors
Rate Limit: 1,000 requests per hour per API key.

Error Codes:

400 Bad Request: Missing required query parameters.

401 Unauthorized: Invalid or missing API bearer token.

429 Too Many Requests: Rate limit exceeded.


---

### Step 2: Save, Commit, and Push

<Steps>
  <Step subtitle="10 sec" title="Save the file">
    Press `Ctrl + S` to save `api-guide.md`.
  </Step>

  <Step subtitle="30 sec" title="Run git commands">
    Run these commands in your VS Code terminal:
    ```bash
    git add .
    git commit -m "Clean up markdown formatting for api guide"
    git push origin main
    ```
  </Step>
</Steps>

Once GitHub Actions finishes building, do a hard refresh (`Ctrl + F5`) on your browser tab, and your page will display beautifully with clean tables, styled code blocks, and proper headings!