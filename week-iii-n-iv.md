# 🚍 Katisha Online: Weeks 3-4 - Financial Engine & Messaging

This phase builds the "Trust Layer" of Katisha Online. We integrate real-world mobile money gateways and secure all financial movements in an immutable ledger (immuDB).

## 🎯 Objectives
- Implement a **Booking Pipeline** (Pending -> Paid -> Confirmed).
- Integrate **MoMo (MTN)** and **Airtel Africa** payment gateways.
- Setup **immuDB** for tamper-proof accounting of agency and passenger funds.
- Integrate **Movetech Solutions SMS API** for real-time ticket delivery.

## 🛠 Tech Stack & Dependencies
* **[immuDB Node.js SDK](https://github.com/codenotary/immudb-node-sdk):** For the immutable ledger.
* **[Axios](https://axios-http.com/):** For communicating with MoMo, Airtel, and Movetech APIs.
* **[BullMQ](https://docs.bullmq.io/):** (Recommended) To handle payment callbacks and SMS retries asynchronously.
* **[crypto](https://nodejs.org/api/crypto.html):** For verifying gateway webhooks/hashes.

---

## 📅 Week 3: Payment Gateways & Booking Logic

### **1. The Booking State Machine (Day 1-3)**
- [ ] **Logic:** Create a `Bookings` table in Postgres with states: `INITIATED`, `PAYMENT_PENDING`, `COMPLETED`, `FAILED`.
- [ ] **Timeout Logic:** Implement a "Cleanup Job" that expires bookings if payment isn't received within 10 minutes.

### **2. Payment Integrations (Day 4-7)**
- [ ] **MTN MoMo:** Implement the "Request to Pay" flow.
- [ ] **Airtel Africa:** Integrate the Merchant Payment API.
- [ ] **Webhooks:** Create a secure `/api/payments/callback` endpoint to receive successful payment confirmations from the providers.

---

## 📅 Week 4: Immutable Ledgers & Messaging

### **1. immuDB Account Management (Day 1-4)**
- [ ] **Setup:** Deploy an immuDB instance (Docker).
- [ ] **The Ledger Service:** Build a service that, upon a successful payment, simultaneously:
    1. Records a **Debit** to the Passenger's digital wallet/payment history.
    2. Records a **Credit** to the Agency’s account.
    3. Records the **Katisha Fee** in a separate ledger.
- [ ] **Verification:** Build a script to verify the cryptographic "State" of the ledger to ensure no records were altered.

### **2. Messaging & Ticket Delivery (Day 5-7)**
- [ ] **Movetech SMS:** Integrate the SMS API to send a "Booking Confirmed" message including: *Route, Time, Bus Plate, and a unique Ticket ID.*
- [ ] **Frontend UI:** Build a "My Bookings" page for passengers and a "Sales Dashboard" for operators showing their immuDB-verified balance.

---

## 📂 Useful Resources for Weeks 3 & 4
* **[immuDB - Getting Started](https://docs.immudb.io/master/develop/node.js.html):** How to connect your Node.js backend to the immutable store.
* **[MTN MoMo API Documentation](https://momodeveloper.mtn.com/):** Specifically the "Collection" widget for Rwanda.
* **[Airtel Africa Developer Portal](https://developers.airtel.africa/):** For standardizing the payment flow across regions.
* **[Movetech Solutions SMS API](https://movetechsolutions.com/):** Documentation for sending transactional SMS.
