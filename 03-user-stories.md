# User Stories and Acceptance Criteria

## Epic A – Customer payment experience

### US-01 Choose a payment method (FR-01) – Must
**As a** customer **I want** to pay with UPI, card, netbanking or wallet **so that** I can use what I prefer.
- **Given** I am at checkout, **when** I select Pay Now, **then** I see all enabled methods on the secure payment page.
- **Given** I am on mobile, **when** I choose UPI, **then** I can pay via my UPI app or by entering a UPI ID.

### US-02 Successful payment confirmation (FR-03, FR-04) – Must
**As a** customer **I want** a clear confirmation after paying **so that** I know my order is placed.
- **Given** payment succeeds, **when** I return to the store, **then** I see the order confirmation with order number and amount paid.
- **Given** the browser closes after payment, **when** the webhook arrives, **then** the order is still confirmed and I receive an email.

### US-03 Retry after failure (FR-05) – Must
**As a** customer **I want** to retry payment without rebuilding my cart **so that** a failed attempt doesn't lose my purchase.
- **Given** my payment failed, **when** I land on the failure page, **then** I see a plain-language reason and a Retry button with other methods.
- **Given** I retry successfully, **when** payment completes, **then** only one order exists for that cart.

### US-04 Save card for faster checkout (FR-11) – Could
**As a** returning customer **I want** to save my card securely **so that** future checkouts are faster.
- **Given** I tick "Save card" and consent, **when** payment succeeds, **then** a token is stored by the gateway and only the last 4 digits are shown in my account.

## Epic B – Order and payment integrity

### US-05 Verified payment before confirmation (FR-02, FR-03) – Must
**As a** store owner **I want** orders confirmed only after verified payment **so that** we never ship unpaid orders.
- **Given** an order is Pending payment, **when** the redirect returns but the signature is invalid, **then** the order is not confirmed and an alert is logged.

### US-06 Handle duplicate webhooks (FR-03) – Must
**As a** developer **I want** webhook processing to be idempotent **so that** gateway retries don't duplicate actions.
- **Given** the same event ID arrives twice, **when** the second is processed, **then** no further status change or email is triggered.

### US-07 Auto-expire unpaid orders (FR-06) – Must
**As a** store owner **I want** unpaid orders to expire **so that** stock isn't locked indefinitely.
- **Given** an order is Pending for 30 minutes, **when** the scheduled job runs, **then** it queries the gateway; if unpaid, the order becomes Cancelled and stock is released.
- **Given** the gateway reports payment succeeded, **when** the job runs, **then** the order is confirmed instead (fixes "paid but pending").

## Epic C – Refunds and finance

### US-08 Refund from the admin panel (FR-07) – Must
**As a** support agent **I want** to refund from the order page **so that** I don't switch to the gateway dashboard.
- **Given** a paid order, **when** I enter an amount not above the refundable balance and confirm, **then** the gateway refund is created, the order shows a refund note, and the customer is emailed.
- **Given** I enter more than the refundable amount, **when** I submit, **then** the system blocks it with an error (BR-04).

### US-09 Daily reconciliation (FR-09) – Must
**As a** finance manager **I want** a daily report of orders vs settlements **so that** I can close the books quickly.
- **Given** the settlement data for the day, **when** the report runs, **then** it lists matched orders, unmatched orders, unmatched settlements, refunds and fees.

### US-10 Troubleshooting logs (FR-10) – Should
**As a** support agent **I want** to search payment logs by order number **so that** I can resolve disputes quickly.
- **Given** an order number, **when** I search, **then** I see requests, responses and webhook events in time order.

## Epic D – Release

### US-11 Test mode and go-live (FR-12) – Must
**As a** project manager **I want** a sandbox mode and a go-live checklist **so that** the switch to live is safe.
- **Given** test mode is on, **when** I place a test order, **then** no real charge occurs and the order is labelled as test.
