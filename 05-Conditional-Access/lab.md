# Lab 05 – Conditional Access and MFA

## Objective

Implement and validate a Microsoft Entra Conditional Access policy that requires Multifactor Authentication (MFA) for a dedicated test user, while documenting the end-to-end deployment, troubleshooting, validation and remediation process.

## Scenario

A dedicated test user was created to access Azure administrative resources. To improve identity security and align with Zero Trust principles, a Conditional Access policy was implemented to require MFA before access to administrative resources is granted.

During implementation, several real-world challenges were encountered, including licensing requirements, tenant alignment issues, user visibility problems and Security Defaults conflicts. These issues were investigated and documented as part of the lab.

## Azure Services Used

- Microsoft Entra ID
- Conditional Access
- Microsoft Entra Suite Trial
- Microsoft 365 Admin Center
- Multifactor Authentication (MFA)
- Microsoft Entra Sign-in Logs
- What If Policy Evaluation Tool

---

## Phase 1 – Initial Setup and Issue Identification

A dedicated test user named `AZ500 CA Test User` was created for the Conditional Access implementation.

While attempting to create the Conditional Access policy, Microsoft Entra displayed a licensing requirement indicating that the tenant did not have sufficient licensing to use Conditional Access.

To satisfy this requirement, a Microsoft Entra Suite trial subscription was activated.

---

## Challenge Encountered

Following activation of the Microsoft Entra Suite trial, an attempt was made to assign the license to the original test user.

Unexpectedly, the user could not be located within the Microsoft 365 Admin Center license assignment interface.

Further investigation identified that different tenant domains were involved during the lab implementation process.

This introduced a potential tenant alignment issue between:

- The original test user account.
- The tenant hosting the Microsoft Entra Suite trial subscription.

---

## Troubleshooting Activities Performed

The following troubleshooting activities were completed:

1. Verified successful creation of the test user in Microsoft Entra ID.
2. Confirmed the user account was enabled.
3. Attempted Conditional Access configuration.
4. Identified Microsoft Entra Premium licensing requirements.
5. Activated Microsoft Entra Suite trial licensing.
6. Attempted license assignment.
7. Confirmed the user did not appear in the licensing assignment interface.
8. Reviewed user licensing information.
9. Investigated account and tenant relationships.
10. Performed tenant alignment validation.
11. Identified potential tenant mismatch and synchronization dependencies.

---

## Troubleshooting Workflow

The troubleshooting process is documented in the attached investigation flowchart.

![Conditional Access Troubleshooting Workflow](screenshots/07-conditional-access-lab-troubleshooting.png)

---

## Root Cause Analysis

Although a single definitive root cause could not be confirmed, the investigation identified two likely contributing factors.

| Potential Root Cause | Description |
|---|---|
| Tenant / Directory Misalignment | The original test user and Microsoft Entra Suite trial subscription were associated with different tenant contexts. |
| Synchronization Delay | Microsoft Entra ID and Microsoft 365 licensing services may not have completed synchronization when license assignment was attempted. |

---

## Investigation Outcome

The investigation highlighted that successful Conditional Access implementation depends on more than policy creation alone.

Key dependencies include:

- Licensing availability
- Correct tenant alignment
- User provisioning
- Microsoft 365 synchronization
- Identity administration

To continue the implementation, a new test user was created within the same tenant that hosted the Microsoft Entra Suite subscription.

---

## Phase 2 – Remediation and Recovery

A new test user was created within the licensed tenant environment.

The following remediation activities were completed:

1. Created a replacement test user within the licensed tenant.
2. Assigned Microsoft Entra Suite licensing.
3. Verified successful license assignment.
4. Confirmed license visibility within Microsoft Entra ID.
5. Continued Conditional Access implementation using the licensed test account.

This approach eliminated tenant alignment concerns and allowed the project to proceed.

---

## Phase 3 – Conditional Access Policy Configuration

- Conditional Access requires Microsoft Entra Premium licensing.
- Microsoft cloud security features can depend on licensing and tenant configuration.
- User creation in Microsoft Entra ID does not always immediately guarantee visibility in Microsoft 365 licensing services.
- Tenant alignment is important when assigning licenses and implementing identity security controls.
- Troubleshooting and evidence collection are important parts of security implementation work.

Phase 3 – Conditional Access Policy Configuration

A Conditional Access policy named:

CA-LAB-Require-MFA-Test-User

was created.

Configuration Summary
Setting	Value
Users	Specific Test User
Target Resource	Microsoft Admin Portals
Grant Control	Require Multifactor Authentication
Conditions	None
Session Controls	None
Initial Deployment Mode	Report-only

---

## Phase 2 – Remediation Plan

To continue the lab, a new test user will be created in the same tenant where the Microsoft Entra Suite trial subscription was activated.

The new test user will then be assigned a Microsoft Entra Suite license and used to complete the Conditional Access MFA policy implementation.

Planned remediation steps:

1. Create a new test user in the licensed tenant.
2. Assign Microsoft Entra Suite license to the new test user.
3. Confirm license assignment.
4. Create Conditional Access policy.
5. Scope the policy to the new test user only.
6. Require MFA for Microsoft Azure Management.
7. Test sign-in behaviour.
8. Validate Conditional Access result in sign-in logs.

Session Controls

No session controls were configured.

The objective of the lab was to demonstrate MFA enforcement using Conditional Access. Session controls were intentionally left unconfigured to keep the policy focused on authentication requirements.

## Policy Deployment Strategy

The Conditional Access policy was initially deployed in Report-only mode.

This allowed policy behaviour to be evaluated without impacting users. Once validation was completed using the What If tool and sign-in logs, the policy was transitioned to Enforced mode.

This approach aligns with Microsoft recommended Conditional Access deployment practices and reduces the risk of unintended authentication disruptions.

Target Resource: Microsoft Admin Portals

Reason:
Microsoft Admin Portals was selected as the protected cloud application because it provides access to administrative interfaces including Microsoft Entra Admin Center and Microsoft 365 Admin Center.

Requiring MFA for administrative access aligns with Zero Trust security principles and helps reduce the risk of unauthorized privileged access.

### Conditional Access What If Evaluation

The What If tool presented a different resource catalog than the Conditional Access policy creation wizard.

While the policy was configured to protect Microsoft Admin Portals, the What If interface did not expose the same application name. The closest available administrative application, Microsoft Office 365 Portal, was used for simulation purposes.

Final validation was performed using actual sign-in testing and Microsoft Entra sign-in logs.

## Security Defaults Conflict

When attempting to change the Conditional Access policy from Report-only mode to Enabled, Microsoft Entra returned an error indicating that Security Defaults must first be disabled.

### Observation

Security Defaults and Conditional Access cannot be used simultaneously to enforce authentication controls.

### Root Cause

The tenant had Security Defaults enabled.

### Impact

Conditional Access policies could not be enforced despite successful policy creation and What If validation.

### Resolution

Security Defaults must be disabled before Conditional Access policies can be enabled.

### Evidence

18-security-defaults-conflict.png

## Security Defaults Remediation

To enable Conditional Access enforcement, Security Defaults were disabled.

Reason selected:

- My organization is planning to use Conditional Access

This change allows Conditional Access policies to become the primary authentication and authorization control mechanism for the tenant.

Evidence:

- 19-security-defaults-disabled.png

