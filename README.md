# Just-In-Time Access Application

## Overview

The Just-In-Time (JIT) Access App is an open-source tool designed to implement just-in-time privileged access to Google Cloud resources. This means that a limited set of users are granted temporary access to projects only when they need it, reducing the risk of unauthorized or accidental changes and enhancing security measures.

## What is Just-In-Time Privileged Access?

Just-in-time privileged access management is a strategy that provides users with elevated permissions for a limited amount of time, and only when necessary. Traditional access models may grant permanent access, increasing the risk of accidental or intentional misuse. With just-in-time access, users must explicitly activate their access and provide justification before being granted temporary privileges.

## Why Just-In-Time Access is Beneficial:

- **Risk Reduction**: By adhering to the principle of least privilege and limiting access to resources only when necessary, the risk of unauthorized and accidental modifications or deletions is significantly reduced.
- **Audit Trail**: The app creates an audit trail that records when and why privileges were activated, providing transparency and accountability.
- **Audits and Reviews**: Administrators can easily conduct audits and reviews of past activity to ensure compliance and security standards are met.

## How Just-In-Time Access Works:

### Activation Process:

1. **Select Project**: Users select the project they need to access.
2. **Choose Roles**: Users select one or more roles they require.
3. **Provide Justification**: Users enter a justification for their access request (e.g., a bug or case number).

### Approval Process (if required):

1. **Request Approval**: For roles that require multi-party approval, users select the role and peers to approve their request.
2. **Peer Approval**: Peers receive email notifications and can approve the request.
3. **Access Granted**: Once approved, users are granted temporary access to the project and notified via email.

## How to Use the App:

### For Users:

- Activate roles on demand by selecting the project, choosing roles, and providing justification.
- For roles requiring approval, follow the same process and select peers for approval.

### For Administrators:

- Grant eligible roles to users or groups by adding special IAM conditions.
- Monitor and audit access requests using Cloud Logging to ensure compliance and security standards are upheld.

## Current Project State:

The application was fully functional, and the CI/CD pipeline was complete. However, the latest deployed version utilized global load balancers, which conflicted with our organizational data residency policies, preventing its use in production.

The Custom Resource Definitions (CRDs) for regional load balancers can be found in:

- [http-lb.txt](acm-infra/load%20balancers/http/http-lb.txt)
- [https-lb.txt](acm-infra/load%20balancers/https/https-lb.txt)

The issue arose due to Identity-Aware Proxy (IAP) incompatibility when deploying regional external application load balancers. After further research, I confirmed that IAP does not support regional load balancers.

While investigating a potential solution, I came across the Privileged Access Management (PAM) service release notes and concluded that we should deprecate the JIT Access application in favor of PAM. I proposed this change to management and it was approved.

## Architecture Diagrams:

### Regional Load Balancers

![Architecture Diagram Regional Load Balancers](architecture-diagrams/regional%20lb/JIT%20Architecture%20Diagram%20-%20Regional.png)

### Global Load Balancers

![Architecture Diagram Global Load Balancers](architecture-diagrams/global%20lb/JIT%20Architecture%20Diagram%20-%20Global.png)

## Official Documentation:

- [Just-In-Time Access](https://googlecloudplatform.github.io/jit-access/)
- [Github Repository](https://github.com/GoogleCloudPlatform/jit-access)
- [Manage just-in-time privileged access to projects](https://cloud.google.com/architecture/manage-just-in-time-privileged-access-to-project)
