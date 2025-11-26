# Request Rejection

In scenarios where an Autonomous Vehicle (AV) requests permission to enter a zone but the Fleet Management System (FMS) determines that the request cannot be granted, the FMS will respond with a `TrafficPermissionUpdateV1` message indicating that the request has been rejected.

## Request Rejection Flow

The following sequence diagram illustrates a typical flow for a request rejection:

```mermaid
sequenceDiagram
	participant AV as Autonomous Vehicle
	participant FMS as Fleet Management System
	AV->>FMS: Send TrafficPermissionRequestV1 for ZoneId XYZ, WayId 1005
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Rejected, Reason: "Zone pending deletion.")
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Does not enter ZoneId XYZ
```