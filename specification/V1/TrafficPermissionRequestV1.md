# TrafficPermissionRequestV1

This message is sent by an Autonomous Vehicle (AV) to request permission from the Fleet Management System (FMS) to enter a zone that is governed by a `trafficPermission` policy. The request includes details about the AV, the zone it wishes to enter, and the road segment it intends to use to enter the zone.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | Truck approaching zone with `trafficPermission` policy | `TrafficPermissionUpdateV1` message |


## Message Attributes

The `TrafficPermissionRequestV1` message consists of the following properties:

| Key | Value | Format | Required | Description |
| --- |:---:|:---:|:---:| --- |
| `"ZoneId"` | ZoneId | UUID | True | The UUID identifying the zone with the `trafficPermission` policy that the AV is requesting permission to enter. |
| `"WayId"` | WayId | Integer | True | The Way ID identifying the road segment (way) that the AV intends to use to enter the zone. (see ISO23725) |

### TrafficPermissionRequestV1 Example

An example `TrafficPermissionRequestV1` message enclosed in the top-level message header data structure:

```JSON
{
    "Protocol": "Open-Autonomy",
    "Version": 1,
    "Timestamp": "2021-09-01T12:00:00Z",
    "EquipmentId": "e4de3723-a315-4506-b4e9-537088a0eabf",
	"TrafficPermissionRequestV1": {
		"ZoneId": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
		"WayId": 1005
	}
}
```

