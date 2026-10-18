# Wellhead API Guide

Welcome to the developer portal for the **Wellhead Telemetry System**. This guide outlines how to authenticate, fetch real-time sensor data, and handle error responses.

## Authentication
All requests to the Wellhead API must include a valid Bearer token in the HTTP header:

```bash
curl -X GET "https://api.wellhead-docs.com/v1/sensors/telemetry?rig_id=Rig-Alpha-10" \
     -H "Authorization: Bearer YOUR_API_KEY"
```

## Interactive Endpoint Reference
You can test and inspect our core endpoints below:

<div class="swagger-container" data-src="../assets/openapi.yaml"></div>

## Rate Limits & Errors
* **Rate Limit:** 1,000 requests per hour per API key.
* **Error Codes:** 
  * `400 Bad Request`: Missing required query parameters.
  * `429 Too Many Requests`: Rate limit exceeded.