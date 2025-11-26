# TrafficPermissionReleasedV1

This message is sent by an Autonomous Vehicle (AV) to notify the Fleet Management System (FMS) that it has exited a zone with a trafficPermission policy and is releasing its previously granted traffic permission.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | AV exiting zone with `trafficPermission` policy | None |

## Message Attributes
The `TrafficPermissionReleasedV1` message consists of the following properties:

| Key | Value | Format | Required | Description |
| --- |:---:|:---:|:---:| --- |
| `"ZoneId"` | ZoneId | UUID | True | The UUID identifying the zone with the `trafficPermission` policy that the AV is exiting. |
| `"WayId"` | WayId | Integer | True | The Way ID identifying the road segment (way) that the AV used to exit the zone. (see ISO23725) |

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