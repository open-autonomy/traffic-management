# TrafficPermissionAcknowledgementV1

This message is sent by an Autonomous Vehicle (AV) to acknowledge receipt of a `TrafficPermissionUpdateV1` message from the Fleet Management System (FMS). It confirms that the AV has received and processed the update regarding its traffic permission status.

| Sender | Triggered by | Triggers |
| --- | --- | --- |
| `AHS`  | Receipt of `TrafficPermissionUpdateV1` message | None |

## Message Attributes
The `TrafficPermissionAcknowledgementV1` message consists of the following properties:
| Key | Value | Format | Required | Description |
| --- |:---:|:---:|:---:| --- |
| `"EventId"` | EventId | UUID | True | The UUID used to correlate this acknowledgement with the corresponding `TrafficPermissionUpdateV1` message. This should match the `EventId` provided in the `TrafficPermissionUpdateV1` message. |

### TrafficPermissionAcknowledgementV1 Example
An example `TrafficPermissionAcknowledgementV1` message enclosed in the top-level message header

```JSON
{
	"Protocol": "Open-Autonomy",
	"Version": 1,
	"Timestamp": "2021-09-01T12:06:00Z",
	"EquipmentId": "e4de3723-a315-4506-b4e9-537088a0eabf",
	"TrafficPermissionAcknowledgementV1": {
		"EventId": "123e4567-e89b-12d3-a456-426614174000"
	}
}
```