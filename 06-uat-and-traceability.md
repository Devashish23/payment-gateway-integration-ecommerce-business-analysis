# UAT Cases, Traceability and Go-Live

## UAT test cases (sandbox)
| ID | Scenario | Steps (summary) | Expected result | Req |
|----|----------|-----------------|-----------------|-----|
| TC-01 | Successful UPI payment | Place order, pay via sandbox UPI success | Order Processing, email sent | FR-01, FR-03 |
| TC-02 | Successful card payment | Pay with sandbox test card | Order Processing | FR-01 |
| TC-03 | Failed card payment | Use failure test card | Failure page with reason and Retry | FR-05 |
| TC-04 | Retry after failure | Retry with UPI after failure | One order only, paid | FR-05 |
| TC-05 | Browser closed after payment | Pay, close tab before redirect | Webhook confirms order | FR-03 |
| TC-06 | Duplicate webhook | Replay the same webhook | No duplicate email or status change | FR-03 |
| TC-07 | Invalid webhook signature | Send tampered payload | Rejected and logged | FR-03 |
| TC-08 | Pending order expiry | Leave order unpaid 30 min | Cancelled, stock released | FR-06 |
| TC-09 | Paid-but-pending recovery | Simulate missed webhook, run job | Job queries gateway, confirms order | FR-06 |
| TC-10 | Full refund | Refund full amount from admin | Refund recorded, email sent | FR-07 |
| TC-11 | Partial refund and over-refund | Refund part, then exceed balance | Partial works, excess blocked | FR-07 |
| TC-12 | Reconciliation report | Run for a day with mixed outcomes | Matched and exception lists correct | FR-09 |
| TC-13 | Amount mismatch | Tamper amount in the callback | Order On hold, alert raised | FR-04 |
| TC-14 | Mobile checkout | Complete flow on a mobile browser | Usable, no layout issues | NFR-05 |

## Requirements Traceability Matrix
| Objective | Requirement | User story | Test case |
|-----------|-------------|------------|-----------|
| BO-1 Success rate | FR-01, FR-05 | US-01, US-03 | TC-01 to TC-04, TC-14 |
| BO-2 No paid-but-pending | FR-02, FR-03, FR-04, FR-06 | US-02, US-05, US-06, US-07 | TC-05 to TC-09, TC-13 |
| BO-3 Refund effort | FR-07, FR-08 | US-08 | TC-10, TC-11 |
| BO-4 Reconciliation | FR-09, FR-10 | US-09, US-10 | TC-12 |
| Release safety | FR-12 | US-11 | Go-live checklist |

## Go-live checklist
- [ ] Merchant account approved and live API keys issued
- [ ] Live keys stored securely and not in the code repository
- [ ] Webhook URL registered with the live secret; signature verification enabled
- [ ] All Must-priority UAT cases passed in sandbox
- [ ] One small real transaction and refund completed in production
- [ ] Customer emails and refund policy page updated
- [ ] Reconciliation report validated by Finance
- [ ] Rollback plan agreed (re-enable previous payment method)
- [ ] Monitoring: alerts on webhook failures and abnormal failure rates

## Risk register
| ID | Risk | Likelihood | Impact | Mitigation |
|----|------|------------|--------|------------|
| R-1 | Merchant approval delayed | Medium | High | Start documents early; build in sandbox meanwhile |
| R-2 | Plugin conflicts with existing theme/plugins | Medium | Medium | Test on staging; keep rollback plan |
| R-3 | Webhook not reachable (firewall/cache) | Medium | High | Whitelist endpoint, exclude from caching, monitor delivery |
| R-4 | Higher fees than assumed | Low | Medium | Confirm pricing in writing before selection |
| R-5 | Festive-season traffic spike | Medium | High | Load test checkout; go live at least two weeks before |
