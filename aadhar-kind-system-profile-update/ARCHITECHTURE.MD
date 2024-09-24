### High Level Estimations

| Metric                        | Calculation                                                                 | Result                  |
|-------------------------------|-----------------------------------------------------------------------------|-------------------------|
| Profile Update Requests       | 10 million requests per day                                                 | ~100 requests/sec       |
| Direct Update Requests        | 20% of total requests                                                       | 20 requests/sec         |
| Approval Requests             | 80% of total requests                                                       | 80 requests/sec         |
| Storage for Attachments       | 8 million requests * 25 MB * 2 uploads                                      | 400,000 GB/day          |
| Storage with Replication      | 400,000 GB/day * replication factor of 3                                     | 1,200,000 GB/day        |
| Request Metadata Storage      | 10 million requests * 1 KB                                                  | 10,000 GB/day           |
| Metadata Storage with Replication | 10,000 GB/day * replication factor                                        | 10,000 GB/day * replication factor |

### High Level Profile Update Flow
![Profile Update Flow](./flow-profile-update.svg)

### High Level Diagram/Components
![High Level Diagram](./high-level-component.svg)

### System Setup and Configuration

#### UI Hosting:
- Leveraging Static Web Hosting capability of Azure.
- All images, CSS, HTML, etc., are served from Azure.

#### High Availability Web Application:
- Built to handle incoming requests from the API Gateway.

#### Network Configuration:
- Setup is configured in a private subnet.
- NSG (Network Security Group) rules are configured for ingress and egress traffic.

#### Application Server:
- Receives and sanitizes and validates incoming requests.
- Scans attached documents via a scan service.
- Pushes request data to the database and blob storage.

#### Multi-Factor Authentication (MFA):
- Utilizes Twilio to send SMS PINs for an extra layer of authentication.

#### Workflow System:
- Leverages a home-grown/BPMN-based workflow system.
- Supports synchronous and asynchronous operations.
- Sends notifications upon completion of operations.


### API Definition(supports chunking)

| Field           | Value                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------|
| **API URI**     | `PATCH /api/v1/profile/internalID`                                                          |
| **Request Header** | `Content-Type: multipart/form-data`                                                      |
| **Request Body**   |                                                                                          |
|                 | `--boundary`                                                                                |
|                 | `Content-Disposition: form-data; name="json"`                                               |
|                 |                                                                                             |
|                 | `{`                                                                                         |
|                 | `  "firstName": "John",`                                                                    |
|                 | `  "lastName": "Doe",`                                                                      |
|                 | `  "maritalStatus": "Single",`                                                              |
|                 | `  "description": "Profile update",`                                                        |
|                 | `  "timestamp": "2023-10-01T12:34:56Z"`                                                     |
|                 | `}`                                                                                         |
|                 | `--boundary`                                                                                |
|                 | `Content-Disposition: form-data; name="attachment1"; filename="document1.pdf"`              |
|                 | `Content-Type: application/pdf`                                                             |
|                 |                                                                                             |
|                 | `<binary data>`                                                                             |
|                 | `--boundary`                                                                                |
|                 | `Content-Disposition: form-data; name="attachment2"; filename="image1.png"`                 |
|                 | `Content-Type: image/png`                                                                   |
|                 |                                                                                             |
|                 | `<binary data>`                                                                             |
|                 | `--boundary--`                                                                              |

### API Response
| Status Code | Description                        | Response Body                                                                 |
|-------------|------------------------------------|-------------------------------------------------------------------------------|
| 200 OK      | Synchronous Operation              | `{ "Status": "Success", "request": "/api/v1/requests/2000" }`                 |
| 202 Accepted| Asynchronous Operation             | `{ "Status": "InProgress", "request": "/api/v1/requests/2000" }`              |
| 400 Bad Request | Client Validation Error        | `{ "Status": "Rejected", "error": "some exception" }`                                    |


### Handling Scaling Requirement
