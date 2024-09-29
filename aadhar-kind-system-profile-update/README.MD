### About Aadhar kind of system
Aadhar kind of system is back bone of the country to identify the person's identity living in the country. Each country can have their own fields apart from uniquely identifying fields. The scale of the userbase can start from few thousands to billion.

### Assumptions
Assume your software is already deployed and functioning for multiple countries and users are already onboard.
Initial onboarding is done via system admin or some back channel.


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
| **Immutable Attributes** | Attributes like SSN/Aadhar number cannot be modified. |

### Detailed Non-Functional Requirements

| Requirement | Description |
|-------------|-------------|
| **Population Consideration** | The system should consider the population of a country like India, approximately 1 billion. |
| **Profile Updates** | The system should handle around 10 million profile updates per 24 hours, which is 1/10th of a billion. |
| **Instantaneous Updates** | 20% of the 10 million updates (~2 million) do not require approval and should be instantaneous. |
| **Approval Required Updates** | 80% of the 10 million updates (~8 million) require approval and, on average, need two attachment uploads. The maximum attachment size permitted is 25 MB. |
| **Synchronous Update Response Time** | For profiles that can be updated synchronously, the p95 response time should be approximately 500 ms. |
| **Update Request Submission Time(with attachments of 25 MB size)** | The p95 response time for capturing update requests should not be more than 1 second. |
 **Data Security** | Data at rest and in transit must be secured. |
| **High Availability (HA)** | High availability is desirable, with a target of 99.9%. |
| **System Security** | The system should be secure, with proper request sanitization, authentication, and authorization. |
| **Quality** | Observability and quality must be fundamental aspects of the system. |

### Architecture/Solution
[Architecture & Solution Approach](./ARCHITECHTURE.MD)