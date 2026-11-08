# API Gateway Automation System

A modular API Gateway built with **n8n**. It receives HTTP requests through a webhook, generates a unique request ID, and routes requests to dedicated sub-workflows based on their `requestType`.

## Overview

The gateway accepts POST requests through:

```text
/webhook/automation-gateway
```

### Supported Request Types

| Request Type | Handler | Function |
|---|---|---|
| `email` | GW - Email Handler | Processes email requests |
| `data` | GW - Data Handler | Processes data requests |
| `notification` | GW - Notification Handler | Processes notification requests |

**Note:** The current handlers format success responses. Actual email delivery, notification delivery, and external data operations have not yet been implemented.

## Architecture

```text
                  HTTP POST Request
                         |
                         v
                API Gateway Webhook
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
                |        |         |
                v        v         v
           Email Handler | Notification Handler
                         |
                    Data Handler
                         |
                         v
                   Merge Results
                         |
                         v
                 Response Handling
                         |
                         v
                 Google Sheets Logging

                  Error Handler
```

## Key Features

- Webhook-based API entry point.
- Automatic request ID generation.
- Request type validation.
- Conditional routing to dedicated sub-workflows.
- Centralized error handling.
- API key authentication check.
- Google Sheets request logging.
- Structured JSON responses.

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

Supported request types:

```text
email
data
notification
```

## Authentication

The gateway checks for an API key through the `x-api-key` request header.

Example headers:

```text
Content-Type: application/json
x-api-key: YOUR_API_KEY
```

**Security Note:** The exported workflow contains a hard-coded API key comparison. Replace it with a securely stored credential or environment variable before deployment. Rotate the exposed test key.

## Workflow Structure

| Workflow | Description |
|---|---|
| API Gateway Automation System | Main webhook, routing, response handling, and logging |
| GW - Email Handler | Handles email-related requests |
| GW - Data Handler | Handles data-related requests |
| GW - Notification Handler | Handles notification-related requests |
| GW - Error Handler | Centralized error handling |

## Technologies Used

- **n8n** – Workflow automation
- **JavaScript** – Data processing and request handling
- **Webhooks** – API communication
- **Google Sheets** – Request logging
- **JSON** – Data exchange format

## Setup Instructions

1. Install or access an n8n instance.
2. Import the workflow JSON files.
3. Configure your Google Sheets credentials.
4. Connect the appropriate spreadsheet.
5. Replace the hard-coded API key with a secure credential.
6. Move authentication before request routing and execution.
7. Review and configure the HTTP response nodes.
8. Test all three request types.
9. Test error handling.
10. Activate the required workflows.

## Current Limitations

- Email delivery integration is not yet implemented.
- Actual notification delivery is not yet implemented.
- The data handler currently formats responses rather than performing external data operations.
- API authentication needs to be moved before handler execution.
- HTTP response routing requires further testing.
- The main gateway and three request handlers are inactive in the supplied exports. The error handler is active.

## Project Status

**Development Stage – Initial Implementation**

This project demonstrates a modular API gateway architecture using n8n, with request routing, sub-workflow execution, response formatting, error handling, and Google Sheets logging.

Further development will focus on implementing actual service integrations, improving authentication, and strengthening error handling.

---

**Project:** API Gateway Automation System  
**Platform:** n8n  
**Language:** JavaScript
<img width="991" height="631" alt="Screenshot 4" src="https://github.com/user-attachments/assets/a0ce1618-e3a1-4cb2-9402-e9ad03f74316" />
<img width="1205" height="937" alt="Screenshot 11" src="https://github.com/user-attachments/assets/689f4875-a1f6-4654-9ee4-7c09065640d4" />
<img width="1318" height="306" alt="Screenshot 12" src="https://github.com/user-attachments/assets/3e594ac2-8355-40a9-b8e7-196072b6adf0" />



