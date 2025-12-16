# TrafficPermissionUpdateV1

This message is sent by the Fleet Management System (FMS) to inform an Autonomous Vehicle (AV) of the status of its permission request to enter a zone governed by a `trafficPermission` policy. The update includes whether the permission is pending, has been granted or rejected, or if the permission has been revoked.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `FMS`  | Receipt of `TrafficPermissionRequestV1` message or revocation of previously granted permission | `TrafficPermissionAcknowledgementV1` message |

## Message Attributes
The `TrafficPermissionUpdateV1` message consists of the following properties:
| Key | Value | Format | Required | Description |
| --- |:---:|:---:|:---:| --- |
| `"EventId"` | EventId | UUID | True | A UUID used to correlate this update with an acknowledgement message from the AV. |
| `"ZoneId"` | ZoneId | UUID | True | The UUID identifying the zone with the `trafficPermission` policy that the AV requested permission to enter. |
| `"WayId"` | WayId | Integer | True | The Way ID identifying the road segment (way) that the AV intended to use to enter the zone. (see ISO23725) This will be set to `null` if the WayID in the `TrafficPermissionRequestV1` message received from the AV was `null`. |
| `"Status"` | | string | Enum | True | The status of the permission request. Possible values are: <br> - `"Pending"`: The request is being processed. <br> - `"Granted"`: The AV is granted permission to enter the zone. <br> - `"Released"`: The permissions granted the AV have been released. <br> - `"Rejected"`: The AV is denied permission to enter the zone. <br> - `"Revoked"`: Previously granted permission has been revoked. |
| `"Reason"` | | string | False | An optional description providing additional context for the status, especially in cases of rejection or revocation. |

> [!IMPORTANT]
> Permission status of `"Revoked"` indicates that the AV must make avoid entering the zone, or make a best-effort stop if already inside the zone.

### TrafficPermissionUpdateV1 Example
An example `TrafficPermissionUpdateV1` message enclosed in the top-level message header data structure indicating that permission has been granted:

```JSON
{
	"Protocol": "Open-Autonomy",
	"Version": 1,
	"Timestamp": "2021-09-01T12:05:00Z",
	"EquipmentId": "e4de3723-a315-4506-b4e9-537088a0eabf",
	"TrafficPermissionUpdateV1": {
		"EventId": "123e4567-e89b-12d3-a456-426614174000",
		"ZoneId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
		"Status": "Granted",
	}
}
```

An example `TrafficPermissionUpdateV1` message enclosed in the top-level message header data structure indicating that permission has been rejected with a reason:

```JSON
{
	"Protocol": "Open-Autonomy",
	"Version": 1,
	"Timestamp": "2021-09-01T12:05:00Z",
	"EquipmentId": "e4de3723-a315-4506-b4e9-537088a0eabf",
	"TrafficPermissionUpdateV1": {
		"EventId": "123e4567-e89b-12d3-a456-426614174000",
		"ZoneId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
		"Status": "Revoked",
		"Reason": "Safety concerns due to unexpected oncoming traffic."
	}
}
```
