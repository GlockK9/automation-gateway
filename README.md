# API Gateway Automation System

A modular API gateway built with **n8n**. It receives HTTP requests through a webhook, generates a unique request ID, and routes requests to dedicated sub-workflows based on their `requestType`.

The project consists of a main gateway, three request handlers, and a centralized error handler.

## Overview

The gateway is configured to accept `POST` requests at:

```text
/webhook/automation-gateway
```

The exact production URL depends on your n8n instance.

### Supported Request Types

| Request Type | Sub-workflow | Current Function |
|---|---|---|
| `email` | GW - Email Handler | Prepares an email request result |
| `data` | GW - Data Handler | Prepares a data request result |
| `notification` | GW - Notification Handler | Prepares a notification result |

**Note:** The handlers currently prepare response data. Actual email delivery, notification delivery, and external data operations have not yet been implemented.

## Architecture

```text
             HTTP POST Request
                     |
                     v
              API Gateway
                     |
                     v
            Generate Request ID
                     |
                     v
           Validate Request Type
                     |
                     v
               Route Request
              /      |       \
             /       |        \
          Email     Data   Notification
            |        |          |
            v        v          v
         Handler  Handler    Handler
              \      |       /
               \     |      /
                Merge Results
                     |
                     v
             Response Handling
                     |
                     v
              Google Sheets

             Central Error Handler
```

## Main Workflow

The main gateway handles:

1. Receiving incoming webhook requests.
2. Generating unique request IDs.
3. Checking that `requestType` is provided.
4. Routing requests to the appropriate sub-workflow.
5. Merging handler results.
6. Preparing error responses.
7. Logging request results in Google Sheets.

### Sub-workflows

- **GW - Email Handler:** Processes email-related request fields and prepares a response.
- **GW - Data Handler:** Processes data-related request fields and prepares a response.
- **GW - Notification Handler:** Processes notification-related request fields and prepares a response.
- **GW - Error Handler:** Uses an n8n Error Trigger to prepare generic error information.

## Request Format

Example JSON request:

```json
{
  "requestType": "email",
  "name": "Jane Doe",
  "email": "jane@example.com",
  "message": "Your message here"
}
```

Supported `requestType` values:

```text
email
data
notification
```

The gateway generates the request ID automatically.

## Authentication

The gateway checks for an API key through the `x-api-key` request header.

Example headers:

```text
Content-Type: application/json
x-api-key: YOUR_API_KEY
```

**Security Notice:**

The current workflow export contains a hard-coded API-key comparison value.

Before deployment:

- Replace the hard-coded value with a securely stored secret.
- Rotate the exposed API key.
- Move authentication validation before request routing and sub-workflow execution.

**Important:** In the current implementation, the API-key check happens after handler execution. Therefore, it does not currently prevent unauthenticated requests from reaching the sub-workflows.

## Response and Logging

The workflows prepare response fields such as:

- `requestId`
- `requestType`
- `name`
- `email`
- `status`
- `handler`
- `message`
- `timestamp`

The main workflow is configured to log request results in Google Sheets.

The HTTP response configuration also requires further testing. In the exported workflow, the node named `Request Type validation` is configured with HTTP 400 and is connected to the merged handler path. This should be reviewed to ensure successful requests receive the correct response.

## Setup

1. Create an n8n instance.
2. Import the workflow JSON files.
3. Configure Google Sheets credentials.
4. Select the spreadsheet and worksheet for logging.
5. Replace the hard-coded API key with a secure secret.
6. Move authentication before request routing.
7. Review and correct HTTP response routing.
8. Test all request types and error paths.
9. Activate the workflows after successful testing.

The supplied exports show the main gateway and three request handlers as inactive. The error handler is active.

## Repository Contents

| File | Description |
|---|---|
| `API Gateway Automation System.json` | Main gateway |
| `GW - Email Handler.json` | Email request handler |
| `GW - Data Handler.json` | Data request handler |
| `GW - Notification Handler.json` | Notification request handler |
| `GW - Error Handler.json` | Central error handler |

## Current Scope and Limitations

This project represents an initial implementation of a modular API gateway.

Current limitations:

- Actual email delivery is not implemented.
- Actual notification delivery is not implemented.
- External data operations are not implemented.
- Authentication must be moved before handler execution.
- HTTP response routing requires correction and testing.
- The API key must be stored securely.
- Workflows require activation and end-to-end testing.

## Built With

- n8n
- Webhooks
- Sub-workflows
- JavaScript
- Google Sheets

---

**Project Status:** Initial Implementation  
**Workflow Platform:** n8n


<img width="991" height="631" alt="Screenshot 4" src="https://github.com/user-attachments/assets/a0ce1618-e3a1-4cb2-9402-e9ad03f74316" />
<img width="1205" height="937" alt="Screenshot 11" src="https://github.com/user-attachments/assets/689f4875-a1f6-4654-9ee4-7c09065640d4" />
<img width="1318" height="306" alt="Screenshot 12" src="https://github.com/user-attachments/assets/3e594ac2-8355-40a9-b8e7-196072b6adf0" />



