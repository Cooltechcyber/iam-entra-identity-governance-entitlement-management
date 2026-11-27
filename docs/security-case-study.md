# Project 6 — Security Case Study

## Problem
A security-reporting team needs temporary group membership without granting indefinite access. Manual access assignment can bypass consistent approval and make revocation difficult to demonstrate.

## Approach
A Microsoft Entra ID Entitlement Management access package was configured to govern membership in `SG-Security-Reports-Access`. A catalog organized the resource; the request policy restricted eligibility to a selected internal test user. A separate approver, a business justification requirement, and a 24-hour assignment lifetime supported least privilege and accountability.

## Test execution
- **Baseline:** Marcus Reed was not a member of the target group.
- **Request:** Marcus Reed submitted the access-package request using Microsoft My Access.
- **Approval:** Rocky Morton reviewed and approved the request; approval history recorded the decision.
- **Provisioning:** The access package showed **Delivered**, and group membership was verified.
- **Expiration:** The assignment view showed an end date of **November 28, 2026 at 7:14:30 AM** (as displayed by the portal).
- **Revocation:** **Not yet tested to completion.** Membership removal must be observed after expiration before reporting success.

## Controls demonstrated
| Control | Evidence | Limitation |
|---|---|---|
| Request eligibility | Requester scope and successful self-service request | Single lab requester |
| Separation of duties | Different requester and approver | Lab accounts only |
| Justification | Required requestor question and approver justification setting | Business need is simulated |
| Least privilege | Security group Member role | No downstream app authorization tested |
| Time limitation | 24-hour expiration configuration and assignment end time | Removal still pending |
| Traceability | Approval history, assignment status, group membership | Screenshots need review/redaction before public upload |

## Final validation plan
After expiration, inspect the assignment and group membership, capture the observed result, and update the README and this case study. If removal is delayed, investigate provisioning and audit events rather than treating the scheduled end time as proof of removal.

## Lessons learned
Configuring an access policy is distinct from validating its enforcement. Approval history demonstrates a governance decision; delivered status and group membership demonstrate provisioning; post-expiration membership and logs are required to demonstrate revocation.
