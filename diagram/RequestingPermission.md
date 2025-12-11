# Requesting Permission
Vehicles that wish to enter a zone governed by a `trafficPermission` policy must first request permission from the Fleet Management System (FMS) using the `TrafficPermissionRequestV1` message. The FMS will then respond with a `TrafficPermissionUpdateV1` message indicating whether the permission request is pending, granted, rejected, or revoked.

> [!IMPORTANT]
> All systems shall implement idempotency when managing traffic permissions.

## Typical Traffic Permission Request Flow

The following sequence diagram illustrates a typical flow for requesting and receiving traffic permission:

```mermaid
sequenceDiagram
	participant AV as Autonomous Vehicle
	participant FMS as Fleet Management System

	AV->>FMS: Send TrafficPermissionRequestV1 for ZoneId XYZ, WayId 1005
	Note over FMS: Process request and determine safe conditions
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Granted)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Enters ZoneId XYZ via WayId 1005
	Note over AV: Exits ZoneId XYZ
	AV->>FMS: Send TrafficPermissionReleasedV1 for ZoneId XYZ
	Note over FMS: Releases permission for AV to ZoneId XYZ
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Released)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
```

## Waiting for Traffic Permissions

A common scenario involves an Autonomous Vehicle (AV) requesting permission to enter a zone but needing to wait until conditions are safe. In this case, the FMS may initially respond with a `TrafficPermissionUpdateV1` message indicating that the request is `"Pending"`. Once conditions are deemed safe, the FMS will send another `TrafficPermissionUpdateV1` message with the status `"Granted"`.

```mermaid
sequenceDiagram
	participant AV as Autonomous Vehicle
	participant FMS as Fleet Management System

	AV->>FMS: Send TrafficPermissionRequestV1 for ZoneId XYZ, WayId 1005
	Note over FMS: Process request but traffic conditions not safe
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Pending)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Waits at entry point of ZoneId XYZ
	Note over FMS: Traffic conditions become safe
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Granted)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Enters ZoneId XYZ via WayId 1005
```

## Releasing Traffic Permission before Entry
If an Autonomous Vehicle (AV) decides not to enter a zone after requesting permission but before actually entering, it should send a `TrafficPermissionReleasedV1` message to the Fleet Management System, as shown below:

```mermaid
sequenceDiagram
	participant AV as Autonomous Vehicle
	participant FMS as Fleet Management System
	AV->>FMS: Send TrafficPermissionRequestV1 for ZoneId XYZ, WayId 1005
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Pending)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over FMS: Process request
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Granted)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Decides not to enter ZoneId XYZ
	AV->>FMS: Send TrafficPermissionReleasedV1 for ZoneId XYZ
	Note over FMS: Releases permission for AV to ZoneId XYZ
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Released)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
```

The AV may also release permissions prior to receiving a grant, for example if conditions change while waiting.

```mermaid
sequenceDiagram
	participant AV as Autonomous Vehicle
	participant FMS as Fleet Management System
	AV->>FMS: Send TrafficPermissionRequestV1 for ZoneId XYZ, WayId 1005
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Pending)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Decides not to enter ZoneId XYZ
	AV->>FMS: Send TrafficPermissionReleasedV1 for ZoneId XYZ
	Note over FMS: Releases permission for AV to ZoneId XYZ
	FMS->>AV: TrafficPermissionUpdateV1 (Status: Released)
	AV->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
```