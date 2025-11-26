# Revoking Permission

In certain situations, the Fleet Management System (FMS) may need to revoke previously granted traffic permission for an Autonomous Vehicle (AV) to enter a zone governed by a `trafficPermission` policy. This revocation is communicated to the AV using the `TrafficPermissionUpdateV1` message with the status set to `"Revoked"`. Situations that may warrant revocation include safety concerns, changes in traffic conditions, or vehicle malfunctions.

## Revocation Flow

"The following sequence diagram illustrates a typical flow for revoking traffic permission:

```mermaid
sequenceDiagram
	participant FMS as Fleet Management System
	participant AV as Autonomous Vehicle

	AV ->>FMS: Send TrafficPermissionRequestV1 for ZoneId XYZ, WayId 1005
	FMS ->>AV: TrafficPermissionUpdateV1 (Status: Pending)
	AV ->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over FMS: Process request
	FMS ->>AV: TrafficPermissionUpdateV1 (Status: Granted)
	AV ->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Enters ZoneId XYZ via WayId 1005
	Note over FMS: Detects safety concern, decides to revoke permission
	FMS ->>AV: TrafficPermissionUpdateV1 (Status: Revoked, Reason: "Safety concerns due to unexpected oncoming traffic.")
	AV ->>FMS: Acknowledge receipt with TrafficPermissionAcknowledgementV1
	Note over AV: Performs best-effort stop
	AV ->> FMS: Indicate degraded state if applicable
```

> [!IMPORTANT]
> Upon receiving a `TrafficPermissionUpdateV1` message with the status `"Revoked"`, the Autonomous Vehicle (AV) must make every effort to avoid entering the zone. If the AV is already inside the zone, it should perform a best-effort stop as soon as it is safe to do so.