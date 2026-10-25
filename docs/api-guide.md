# Wellhead Telemetry API Reference

This reference documents an illustrative REST API for retrieving wellhead telemetry data. It demonstrates API documentation practices for endpoint definitions, authentication, request parameters, JSON responses, error handling, and rate limits.

!!! warning "Demonstration API"
    This is a portfolio example, not a verified or deployed API. The base URL, credentials, responses, rate limits, and endpoint behaviour are illustrative. Requests will not retrieve live well data. Do not use these examples for operational or safety-critical decisions.

## 1. Overview

The example API represents a service that provides telemetry readings associated with a wellhead monitoring system.

### Intended audience

- Software developers integrating telemetry data into an application
- Technical teams reviewing a monitoring API
- Engineers and documentation specialists evaluating the example interface

### Example capabilities

- Request telemetry for a specified rig
- Review pressure and temperature readings
- Inspect the reported telemetry status
- Handle invalid requests and authentication errors

## 2. Base URL

The reserved `.invalid` domain is used to prevent the example from being mistaken for a live service.

```text
https://api.example.invalid
```

| Property | Description |
|---|---|
| API style | REST |
| Data format | JSON |
| Example API version | v1 |
| Authentication model | Bearer token |
| Transport | HTTPS in the illustrative design |

## 3. Authentication

The example uses a Bearer token in the HTTP `Authorization` header.

```http
Authorization: Bearer YOUR_EXAMPLE_TOKEN
```

`YOUR_EXAMPLE_TOKEN` is a placeholder, not a working credential. This portfolio example does not provide a token issuance or validation service.

### Authentication requirements

- Include the token in the `Authorization` header.
- Do not place credentials in query parameters.
- Avoid committing real credentials to source control.
- A real implementation should use an approved token provisioning and rotation process.

An unauthenticated or invalidly authenticated request is illustrated as returning `401 Unauthorized`.

## 4. Retrieve Telemetry

Returns an illustrative telemetry record for the requested rig.

### `GET /v1/sensors/telemetry`

**Purpose:** Retrieve an example telemetry record associated with a specified rig.

**Authentication:** Bearer token, as described in Section 3.

### Request parameters

| Parameter | Location | Type | Required | Description |
|---|---|---|---|---|
| `rig_id` | Query | String | Yes | Identifier of the rig whose telemetry is requested |

### Example request

```bash
curl --get "https://api.example.invalid/v1/sensors/telemetry" \
  --header "Authorization: Bearer YOUR_EXAMPLE_TOKEN" \
  --header "Accept: application/json" \
  --data-urlencode "rig_id=RIG-001"
```

This command illustrates the request format only. The reserved host does not provide a live API service.

### Example successful response

Illustrative HTTP status: `200 OK`

```json
{
  "timestamp": "2026-10-20T10:30:00Z",
  "rig_id": "RIG-001",
  "pressure_psi": 1250.5,
  "temperature_f": 178.4,
  "status": "normal"
}
```

### Response fields

| Field | Type | Description |
|---|---|---|
| `timestamp` | String (date-time) | Example timestamp for the reading, represented in UTC |
| `rig_id` | String | Identifier associated with the requested rig |
| `pressure_psi` | Number | Illustrative pressure reading in pounds per square inch |
| `temperature_f` | Number | Illustrative temperature reading in degrees Fahrenheit |
| `status` | String | Example status label associated with the telemetry record |

The example values are fictional and do not represent actual operating conditions or approved alarm thresholds.

## 5. HTTP Status Codes and Error Handling

The following responses illustrate how a real implementation could communicate common request failures.

| Status code | Meaning | Example cause |
|---|---|---|
| `200 OK` | Request succeeded | A telemetry record is returned |
| `400 Bad Request` | Request is invalid | Required `rig_id` is missing or malformed |
| `401 Unauthorized` | Authentication failed | Token is missing, invalid, or expired |
| `429 Too Many Requests` | Rate limit exceeded | Request quota has been exceeded |

### Example error response

Illustrative HTTP status: `400 Bad Request`

```json
{
  "error": {
    "code": "INVALID_REQUEST",
    "message": "The rig_id query parameter is required."
  }
}
```

This is a proposed error format for the demonstration. It is not a confirmed response from a live service.

### Troubleshooting guidance

**400 Bad Request**

Check that `rig_id` is present, correctly spelled, and supplied as a query parameter.

**401 Unauthorized**

Check that the `Authorization` header uses the Bearer scheme and that a valid token has been supplied. This example does not issue or validate tokens.

**429 Too Many Requests**

Stop sending requests temporarily and follow the retry guidance provided by the actual service, if available. A production API should document whether it provides a `Retry-After` header and rate-limit headers.

## 6. Rate Limits

Rate limits define how many requests a client may make within a specified period.

This example does not establish a verified rate limit. Any quota documented for a real implementation must be confirmed with the service owner.

A production API should document:

- The applicable quota and its time window
- Whether limits apply per user, token, or API key
- The response returned when a quota is exceeded
- Any rate-limit headers and retry guidance

## 7. Request and Response Conventions

The example uses the following conventions:

- HTTP methods describe the intended operation.
- Query parameters identify the requested rig.
- JSON represents the example response payload.
- Bearer authentication is illustrated through an HTTP header.
- HTTP status codes communicate success or failure.

A production implementation should also define field validation, timestamp guarantees, units, nullability, data freshness, and the meaning of each possible status value.

## 8. Security and Operational Considerations

Telemetry can inform engineering decisions, so a real implementation requires controls beyond documenting an endpoint.

- Enforce HTTPS and secure credential handling.
- Authenticate and authorize callers.
- Validate request parameters.
- Define monitoring, logging, and error-handling requirements.
- Document data freshness and measurement units.
- Establish appropriate access controls and retention policies.
- Verify all behaviour against the deployed service and approved engineering requirements.

**Important:** This API example is not a control system and must not be used to operate equipment, determine safe operating limits, or replace approved field procedures.

## 9. Related Resources

- [Home — Technical Documentation Portfolio](index.md)
- [Wellhead Documentation](Guide.md)
- [Technical Guide](Guide2.md)

## 10. Scope and Limitations

This reference demonstrates the structure and writing style of an API reference. It does not establish that an API implementation exists.

Before adapting this documentation for a real service, verify the base URL, authentication mechanism, endpoint behaviour, schemas, error responses, rate limits, and security requirements with the service owner and approved technical sources.