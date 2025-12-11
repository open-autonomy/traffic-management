# TrafficPermissionReleasedV1

This message is sent by an Autonomous Vehicle (AV) to notify the Fleet Management System (FMS) that it has either exited or no longer requires permission to enter a zone with a trafficPermission policy and is releasing its permission request.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | The AV exits a zone with `trafficPermission` policy | None |
| `AHS`  | The AV no longer needs to enter a zone with `trafficPermission` policy | None |

> [!NOTE]
> The TrafficPermissionReleasedV1 message can be sent while the permission request is still pending or after permission has been granted.

## Message Attributes
The `TrafficPermissionReleasedV1` message consists of the following properties:

| Key | Value | Format | Required | Description |
| --- |:---:|:---:|:---:| --- |
| `"ZoneId"` | ZoneId | UUID | True | The UUID identifying the zone with the `trafficPermission` policy that the AV is exiting. |
| `"WayId"` | WayId | Integer | True | The Way ID identifying the road segment (way) that the AV used to enter the zone. (see ISO23725) |

### TrafficPermissionReleasedV1 Example
An example `TrafficPermissionReleasedV1` message enclosed in the top-level message header data structure

```JSON
{
	"Protocol": "Open-Autonomy",
	"Version": 1,
	"Timestamp": "2021-09-01T12:30:00Z",
	"EquipmentId": "e4de3723-a315-4506-b4e9-537088a0eabf",
	"TrafficPermissionReleasedV1": {
		"ZoneId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
		"WayId": 1005
	}
}
```