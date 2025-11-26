# Zekt Provider Example Repository

## Purpose

This repository showcases example scenarios demonstrating how to interact with and utilize the **Zekt Provider GitHub Action** for sending event messages to the Zekt backend API.

## Overview

The Zekt Provider action enables seamless integration with GitHub Actions workflows, allowing you to:
- Send audit events to the Zekt backend
- Send infrastructure events to the Zekt backend
- Track and log provider service activities
- Maintain audit trails for compliance and monitoring

## Workflows Included

### 1. `zekt-provide-audit-event-msg.yaml`
**Purpose:** Demonstrates how to send audit event messages to the Zekt backend API.

**Workflow Type:** `workflow_dispatch` (manual trigger)

**Input Parameters:**
- `providerServiceName` - Identifier for the provider service (e.g., "Customer X")
- `providerServiceDescription` - Description of the audit event (e.g., "Tax transaction failed - request auditing")
- `providerAuditId` - Unique audit ticket ID (e.g., "334433359922")
- `providerAuditStatus` - Status of the audit (e.g., "Request", "Close")

**Key Steps:**
- Checks out repository code
- Constructs a JSON payload with audit event data
- Generates a unique step ID for tracking
- Sends the payload to Zekt backend via the `zekt-action`
- Logs the response from Zekt

---

### 2. `zekt-provide-infra-event-msg.yaml`
**Purpose:** Demonstrates how to send infrastructure event messages to the Zekt backend API.

**Workflow Type:** `workflow_dispatch` (manual trigger)

**Input Parameters:**
- `providerServiceName` - Identifier for the provider service (e.g., "InfraProvider X")
- `providerServiceDescription` - Description of the infrastructure event (e.g., "Web Server Deployed - take action")
- `providerInfraId` - Unique infrastructure ticket ID (e.g., "334433359922")
- `providerInfraStatus` - Status of the infrastructure (e.g., "Deployed")
- `providerInfraUrl` - URL to the deployed infrastructure resource
- `providerInfraResourceId` - ID of the deployed infrastructure resource

**Key Steps:**
- Checks out repository code
- Sets up Node.js runtime
- Constructs a JSON payload with infrastructure event data
- Generates a unique step ID for tracking
- Sends the payload to Zekt backend via the `zekt-action`
- Logs the response from Zekt

---

## How to Use

### Running a Workflow

1. Navigate to the **Actions** tab in your GitHub repository
2. Select either `zekt-provide-audit-event-msg` or `zekt-provide-infra-event-msg`
3. Click **Run workflow**
4. Fill in the required input parameters
5. Click **Run workflow** to trigger the workflow

### Example: Audit Event

```
providerServiceName: "Customer X"
providerServiceDescription: "Tax transaction failed - request auditing"
providerAuditId: "334433359922"
providerAuditStatus: "Request"
```

### Example: Infrastructure Event

```
providerServiceName: "InfraProvider X"
providerServiceDescription: "Web Server Deployed - take action"
providerInfraId: "334433359922"
providerInfraStatus: "Deployed"
providerInfraUrl: "https://example.com/infra/resource"
providerInfraResourceId: "resource-12345"
```

---

## Architecture

Each workflow:
1. **Accepts input parameters** via `workflow_dispatch` trigger
2. **Builds a dynamic JSON payload** using PowerShell
3. **Generates a unique tracking ID** for the event
4. **Sends the payload** to Zekt backend using the `zekt-action`
5. **Logs the results** for monitoring and debugging

---

## Dependencies

- **GitHub Actions Runner:** Ubuntu Latest
- **Zekt Action:** `zekt-dev-org/zekt-action@v1.0.0`
- **Runtime:** PowerShell for payload construction
- **Node.js:** 18 (for infra workflows)

---

## Event Message Format

Both workflows construct JSON payloads that are sent to the Zekt backend API. The payload structure includes:

**Audit Event Payload:**
```json
{
  "providerServiceName": "...",
  "providerServiceDescription": "...",
  "providerAuditId": "...",
  "providerAuditStatus": "..."
}
```

**Infrastructure Event Payload:**
```json
{
  "providerServiceName": "...",
  "providerServiceDescription": "...",
  "providerInfraId": "...",
  "providerInfraStatus": "...",
  "providerInfraUrl": "...",
  "providerInfraResourceId": "..."
}
```

---

## Troubleshooting

- **Action not found error:** Verify that the `zekt-action` repository is public and accessible, and that version `v1.0.0` is released
- **Workflow fails:** Check the workflow logs in the GitHub Actions tab for detailed error messages
- **Payload issues:** Review the PowerShell script output to ensure the JSON payload is correctly formatted

---

## Contributing

To add new provider scenarios or workflows, follow the same pattern:
1. Create a new `.yaml` file in `.github/workflows/`
2. Define workflow inputs using `workflow_dispatch`
3. Construct the appropriate payload
4. Send to Zekt backend via the action
5. Document the workflow and its purpose in this README

---

## License

This repository is provided as an example for demonstrating Zekt Provider integration patterns.
