# Automation Gateway

An n8n workflow automation system that acts as a central entry point for receiving, validating, routing, and processing automation requests through dedicated sub-workflows.

## Project Overview

The Automation Gateway provides a structured way to handle different request types through a single workflow. It receives incoming requests, validates the required information, identifies the appropriate processing route, and delegates tasks to the relevant sub-workflows.

## Workflow Architecture

1. **Request Reception:** Receives incoming requests through a webhook.
2. **Validation:** Checks request information and required fields.
3. **Request Routing:** Identifies the request type and selects the appropriate handler.
4. **Sub-workflow Execution:** Delegates processing to the relevant workflow.
5. **Error Handling:** Routes failures through an error-handling process.
6. **Response Management:** Returns the appropriate execution response.

## Technologies Used

- n8n
- Webhooks
- JSON
- JavaScript
- API Integration
- Workflow Automation

## Key Features

- Centralized request processing.
- Conditional request routing.
- Modular sub-workflow architecture.
- Input validation.
- Error handling and execution monitoring.

## Repository Contents

- `automation-gateway.json` - Exported n8n workflow.

## Setup

1. Import the JSON file into your n8n instance.
2. Configure the required credentials and integrations.
3. Review and configure webhook settings.
4. Activate the workflow.
5. Test using sample requests.

**Note:** Credentials and environment-specific configurations are not included in the exported workflow.

## Project Purpose

Built to demonstrate modular workflow design, request routing, validation, and centralized automation management using n8n.
<img width="991" height="631" alt="Screenshot 4" src="https://github.com/user-attachments/assets/a0ce1618-e3a1-4cb2-9402-e9ad03f74316" />
<img width="537" height="278" alt="Screenshot 9" src="https://github.com/user-attachments/assets/ce849bb9-588f-4563-9244-78aca721c2b2" />
<img width="995" height="148" alt="Screenshot 10" src="https://github.com/user-attachments/assets/7ffa79b4-ea53-48c8-896e-5166e46c5f1d" />
