### High-Level Requirement
Objective: Design a profile update system that supports multiple countries, allowing the software to be used and deployed globally.

Key Features:

Multi-Country Support: The system should be capable of handling profile updates for users from various countries.
Global Deployment: Ensure the software can be deployed and function seamlessly in multiple countries.

### Detailed Functional Requirements

| Requirement | Description |
|-------------|-------------|
| **User Facing Flow** | The system should be designed for user-facing interactions. |
| **Attributes** | The profile includes attributes such as Salutation, Last Name, First Name, Sex, Date of Birth (DOB), Profile Photo, Address (simple format), Aadhar number/SSN number, and custom attributes. |
| **Approval Mechanism** | - Attributes like Salutation and Profile Photo can be updated instantly using OTP or similar MFA mechanisms without approval. <br> - Attributes such as Name, Sex, DOB, etc., require approval and additional document uploads. |
| **Notifications** | Users should be notified of updates via email or SMS. |
| **Scope** | The system is limited to a desktop application. |
| **Approval Levels** | Only one level of approval is required. |
| **Immutable Attributes** | Attributes like SSN/Aadhar number cannot be modified. |
| **Attribute Size** | The size of attributes may vary by country. |

### Detailed Non-Functional Requirements

| Requirement | Description |
|-------------|-------------|
| **Population Consideration** | The system should consider the population of a country like India, approximately 1 billion. |
| **Profile Updates** | The system should handle around 10 million profile updates per 24 hours, which is 1/10th of a billion. |
| **Instantaneous Updates** | 20% of the 10 million updates (~2 million) do not require approval and should be instantaneous. |
| **Approval Required Updates** | 80% of the 10 million updates (~8 million) require approval and, on average, need two attachment uploads. The maximum attachment size permitted is 25 MB. |
| **Synchronous Update Response Time** | For profiles that can be updated synchronously, the p95 response time should be approximately 1 second. |
| **Asynchronous Update Response Time** | The p95 response time for capturing asynchronous update requests should be approximately 1 second. |
| **Notification Latency** | The latency to notify the end user of profile updates should be approximately 1 second. |
| **Data Sovereignty** | The system must address data sovereignty issues. |
| **Data Security** | Data at rest and in transit must be secured. |
| **High Availability (HA)** | High availability is desirable, with a target of 99.9%. |
| **System Security** | The system should be secure, with proper request sanitization, authentication, and authorization. |
| **Observability and Quality** | Observability and quality must be fundamental aspects of the system. |
| **CI/CD Integration** | Continuous Integration (CI) and Continuous Deployment (CD) must be deeply integrated into the system. |
| **Testing** | Unit test cases and integration test cases should be inherent properties of the system. |

### Architecture/Solution
![Architecture & Solution Approach](./ARCHITECHTURE.MD)