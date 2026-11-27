# Project 6 — Microsoft Entra ID Governance: Entitlement Management

**IAM Portfolio Lab | Access Packages, Approval Workflows, and Time-Limited Group Membership**

> **Status:** Access request, approval, and provisioning validated. **Automatic expiration and removal are pending verification.**

## Executive summary
This lab implements a governed, self-service access request workflow using Microsoft Entra ID Entitlement Management. A standard test user requests membership in a security reporting group through an access package. A separate designated approver reviews the request, and the package applies a 24-hour assignment expiration policy.

The security group is a **lab resource**; membership alone does not demonstrate access to real security reports or applications.

## Business scenario
An organization needs to limit security-reporting group membership to users with an approved business need, avoid standing access, and maintain evidence of decisions and assignments.

## Lab configuration

| Component | Configuration |
|---|---|
| Platform | Microsoft Entra ID P2 / Entitlement Management |
| Catalog | `IAM-Security-Access-Catalog` |
| Access package | `AP-Security-Reports-Access` |
| Managed resource | `SG-Security-Reports-Access` (Security group) |
| Resource role | Member (not Owner) |
| Eligible requester | Marcus Reed (test identity) |
| Designated approver | Rocky Morton (separate identity) |
| Request policy | Internal directory user; scoped to selected user |
| Self-service requests | Enabled |
| Requester justification | Required |
| Additional requestor question | Required long-text business requirement |
| Approval | One stage; specific approver; approver justification required |
| Approval deadline | 3 days |
| Assignment lifetime | 24 hours |
| User-selected timeline | Disabled |
| Extensions | Disabled |
| Access reviews | Not enabled for this exercise |

## Implementation
1. Created a dedicated enabled catalog, excluding external users.
2. Created an assigned-membership security group without pre-populating the requester.
3. Added the group to the catalog and selected its **Member** resource role.
4. Created an access package with a self-service request policy scoped to the test requester.
5. Required business justification and a one-stage approval by a separate designated approver.
6. Configured a 24-hour assignment duration and disabled extensions.
7. Submitted a request in Microsoft My Access as Marcus Reed.
8. Reviewed and approved the request as Rocky Morton.
9. Checked assignment delivery and verified group membership after approval.

## Test results

| Test | Expected | Observed | Result |
|---|---|---|---|
| Pre-request membership | Marcus absent from group | Confirmed absent | PASS |
| Self-service request | Eligible user can request package | Request submitted | PASS |
| Approval routing | Request reaches designated approver | Pending approval displayed | PASS |
| Approval decision | Authorized approver can approve | Approved in history | PASS |
| Assignment provisioning | Package delivers Member group role | Assignment status **Delivered**; Marcus found in group | PASS |
| Time-bound assignment | Expiration is set | Portal showed **Nov 28, 2026, 7:14:30 AM** (portal display time) | CONFIGURED |
| Automatic access removal | Group membership removed after expiration | Not yet observed | **PENDING** |

**Evidence standard:** Approval and a delivered assignment are not evidence that expiration-based removal has occurred. The final test will check both the access-package assignment and security-group membership after expiration and processing.

## Screenshot evidence

The following 15 screenshots were uploaded to the [`screenshots/`](screenshots/) directory. The final automatic removal screenshot is pending.

| # | Evidence |
|---|---|
| 01 | [01 — Identity Governance Catalog Created.png](screenshots/01%20%E2%80%94%20Identity%20Governance%20Catalog%20Created.png) |
| 02 | [02 — Security Group Created.png](screenshots/02%20%E2%80%94%20Security%20Group%20Created.png) |
| 03 | [03 — Catalog Resource Added.png](screenshots/03%20%E2%80%94%20Catalog%20Resource%20Added.png) |
| 04 | [04-access-package-resource-role.png](screenshots/04-access-package-resource-role.png) |
| 05 | [05 — Approval Workflow Configuration.png](screenshots/05%20%E2%80%94%20Approval%20Workflow%20Configuration.png) |
| 06 | [06-requestor-information.png](screenshots/06-requestor-information.png) |
| 07 | [07-access-package-lifecycle.png](screenshots/07-access-package-lifecycle.png) |
| 08 | [08-access-package-review.png](screenshots/08-access-package-review.png) |
| 09 | [09 — Access Package Created.png](screenshots/09%20%E2%80%94%20Access%20Package%20Created.png) |
| 10 | [10-before-access-assignment.png](screenshots/10-before-access-assignment.png) |
| 11 | [11-employee-access-request.png](screenshots/11-employee-access-request.png) |
| 12 | [12-pending-access-approval.png](screenshots/12-pending-access-approval.png) |
| 13 | [13-approved-access-request.png](screenshots/13-approved-access-request.png) |
| 14 | [14-security-group-membership-after-approval.png](screenshots/14-security-group-membership-after-approval.png) |
| 15 | [15-access-package-assignment-expiration.png](screenshots/15-access-package-assignment-expiration.png) |
| 16 | Automatic access removal — **pending verification** |

**Public portfolio note:** Review images for email addresses, tenant IDs, object IDs, tokens, and other sensitive identifiers; redact where needed.

## Security significance
- **Least privilege:** Assignment uses the group **Member** role, not Owner.
- **Separation of duties:** Requester and approver are distinct identities.
- **Governance:** Eligibility, required justification, and approval are centrally defined.
- **Limited duration:** Access has a configured expiration rather than an indefinite assignment.
- **Auditability:** Request and approval history plus assignment and membership evidence support validation.

## Remaining validation
After the portal-displayed expiration time:
1. Check the package assignment's status and end time.
2. Check whether Marcus Reed is absent from `SG-Security-Reports-Access`.
3. Allow for processing delay; if membership persists, investigate assignment processing and audit logs.
4. Capture and redact `16-automatic-access-removal.png` only when removal is verified.
5. Update the test-results table with actual observations and timestamps.

## Scope and limitations
This is a controlled home-lab implementation, not a production deployment. No actual protected reporting application was configured as a downstream resource. The automatic revocation outcome is not yet claimed.
