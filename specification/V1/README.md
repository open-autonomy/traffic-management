This document describes Version 1 of the Traffic Management Specification.

# Traffic Management Specification V1
This specification defines the messages and protocols for Autonomous Vehicles (AVs) to communicate with a Fleet Management System (FMS) to obtain the required permissions to enter zones with trafficPermission policies. It requesting permissions, response messages, and error handling to ensure safe and efficient traffic management within these zones.

# Messages

> [!IMPORTANT]
All messages described below must be embedded within the [top-level message header](MessageHeader.md) data structure. 

The following messages are defined in this specification for managing traffic permissions:
- [TrafficPermissionRequestV1](TrafficPermissionRequestV1.md): Message sent by an AV to request permission to enter a zone with a trafficPermission policy.
- [TrafficPermissionUpdateV1](TrafficPermissionUpdateV1.md): Message sent by the FMS to inform the AV of the status of its permission request, including approval or denial.
- [TrafficPermissionReleasedV1](TrafficPermissionReleasedV1.md): Message sent by the AV to notify the FMS that it has exited the zone and is releasing its traffic permission.
- [TrafficPermissionAcknowledgementV1](TrafficPermissionAcknowledgementV1.md): Message sent by the AV to acknowledge receipt of the TrafficPermissionUpdateV1 message.







