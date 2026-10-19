
# Wellhead Telemetry API Guide

> **Portfolio demonstration:** This guide describes an illustrative API. The server address, credentials, and sensor readings are examples and are not confirmed to represent a live service.

## 1. Overview

The Wellhead Telemetry API is a demonstration interface for retrieving pressure and temperature measurements associated with a drilling rig.

This guide explains authentication, endpoint usage, query parameters, example responses, rate limits, and error handling.

## 2. Authentication

Requests must include a valid Bearer token in the `Authorization` HTTP header.

Example header:

```http
Authorization: Bearer YOUR_API_KEY
```

Replace `YOUR_API_KEY` with a valid token issued by the API provider. Never publish real API credentials in documentation or source control.

## 3. Endpoint Reference

### Get Live Sensor Telemetry

Retrieves a telemetry record for the specified rig.

| Property | Value |
|---|---|
| HTTP Method | `GET` |
| Endpoint | `/v1/sensors/telemetry` |
| Authentication | Bearer token |
| Required Parameter | `rig_id` |

### 3.1 Example Request

The hostname below is a placeholder. Replace it with the actual API base URL before making a real request.

```bash
curl --request GET \
  "https://api.example.com/v1/sensors/telemetry?rig_id=Rig-Alpha-10" \
  --header "Authorization: Bearer YOUR_API_KEY"
```

### 3.2 Query Parameters

| Parameter | Details |
|---|---|
| `rig_id` | **Type:** string<br>**Required:** Yes<br>**Description:** Identifier of the rig whose telemetry is requested, for example, `Rig-Alpha-10`. |

The accepted parameter format and validation rules must be confirmed against the API implementation.

## 4. Example Success Response

**HTTP Status:** `200 OK`

The following JSON is an illustrative response and does not represent verified live sensor data.

```json
{
  "timestamp": "2026-10-18T02:00:00Z",
  "pressure_psi": 9850.5,
  "temperature_f": 185.2,
  "status": "OPTIMAL"
}
```

### 4.1 Response Fields

| Field | Type | Description |
|---|---|---|
| `timestamp` | string | Example timestamp in UTC using ISO 8601 format. |
| `pressure_psi` | number | Example pressure measurement in pounds per square inch (psi). |
| `temperature_f` | number | Example temperature measurement in degrees Fahrenheit. |
| `status` | string | Illustrative status associated with the reading. |

The permitted status values, measurement limits, and response schema must be verified before this example is treated as an implementation contract.

## 5. Rate Limits

The original portfolio example specifies a limit of 1,000 requests per hour per API key. This limit has not been verified against a running service.

For a production API, the documentation should explain how clients can identify the request limit, determine when it resets, and respond to rate limiting.

## 6. Error Responses

The following error codes are proposed examples. Actual behavior must be verified against the API implementation.

| HTTP Status | Meaning | Recommended Client Action |
|---|---|---|
| `400 Bad Request` | A required query parameter is missing or invalid. | Check the request parameters and submit a valid request. |
| `401 Unauthorized` | The authentication token is missing or invalid. | Check the token and Authorization header. |
| `429 Too Many Requests` | The request limit has been exceeded. | Reduce the request rate and retry according to the service's documented policy. |

## 7. Security Considerations

- Use HTTPS for API communications.
- Store API credentials securely.
- Do not commit real tokens, passwords, or other secrets to a public repository.
- Follow the API provider's authentication and access-control requirements.

These are general documentation recommendations and do not confirm that the illustrative API implements these controls.

## 8. Implementation Notes

Before this guide is used as production documentation:

1. Verify the base URL and endpoint against the actual API.
2. Confirm the authentication mechanism and token requirements.
3. Validate the query parameters and response schema.
4. Confirm rate limits and error-response behavior.
5. Ensure this guide matches the OpenAPI specification.
6. Have all safety-critical or operational information reviewed by the appropriate subject-matter expert.

---

**Document Status:** Portfolio Demonstration

**Document Version:** 1.0.0

**Last Updated:** 19 October 2026