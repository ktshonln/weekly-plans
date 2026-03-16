# 🚍 Katisha Online: Week 5 - Dynamic QR & Driver Operations

This week focuses on secure boarding and field operations. We implement "Rolling" QR codes for security and a real-time manifest for the drivers.

## 🎯 Objectives
- Implement **Dynamic (Refreshing) QR codes** to prevent ticket fraud.
- Build the **Driver Manifest** view for trip-specific passenger lists.
- Develop the **Real-time Validator** (Green/Red) logic.

## 🛠 Tech Stack & Dependencies
* **[Speakeasy](https://github.com/speakeasyjs/speakeasy):** For generating Time-based One-Time Password (TOTP) hashes to make the QR dynamic.
* **[html5-qrcode](https://github.com/mebjas/html5-qrcode):** For the Driver/Conductor’s camera-based scanning.
* **[Socket.io](https://socket.io/):** (Optional but recommended) To update the driver's manifest in real-time as people board.

---

## 📅 Week 5 Deliverables

### **1. Passenger: The "Rolling" QR Code (Day 1-2)**
- [ ] **Dynamic Logic:** Instead of a static ID, the QR contains: `TicketID` + `CurrentTimestamp` + `HMAC_Signature`. 
- [ ] **Frontend Refresh:** The QR code component must re-generate every 30 seconds (similar to a Google Authenticator code).
- [ ] **Security:** If a QR is scanned and the timestamp is older than 60 seconds, it is automatically marked as **Invalid (Red)**.

### **2. Driver: Trip Manifest View (Day 3-4)**
- [ ] **Assignment Logic:** Build a view where a logged-in Driver sees only the trips assigned to them for that day.
- [ ] **Manifest UI:** A list showing all passengers who have paid for that specific trip. 
    - *Columns:* Passenger Name, Seat Category, Payment Status, and Boarding Status (Checked-in vs. Pending).

### **3. Validation Engine (Online Only) (Day 5-7)**
- [ ] **The Scanner UI:** A simple "Scan" button on the Driver's dashboard that opens the camera.
- [ ] **Backend Real-time Check:**
    - **Step 1:** Verify the HMAC signature (ensure it's from Katisha).
    - **Step 2:** Check if the timestamp is fresh.
    - **Step 3:** Query Postgres/immuDB to see if `status === 'PAID'` and `boarded === false`.
- [ ] **The Feedback:** - 🟢 **Green:** "Access Granted" (Backend marks ticket as `boarded: true`).
    - 🔴 **Red:** "Access Denied" (Reasons: Expired QR, Already Used, or Wrong Trip).

---

## 🔑 Technical Logic: The "Refreshing" QR
To implement the refreshing QR without hitting your database every 30 seconds, use a **TOTP-style approach**:
1. The backend provides a "Secret Key" for that specific ticket upon purchase.
2. The Frontend uses that secret + the current time to generate a 6-digit code or a unique hash.
3. The QR displays this hash.
4. When the Driver scans it, the Backend recalculates the hash using the same secret and the current time. If they match, it's valid.
