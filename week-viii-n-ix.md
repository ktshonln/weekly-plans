# 🚍 Katisha Online: Weeks 8-9 - Dashboards & Advanced Analytics

This phase focuses on the "Information Layer." We are transforming raw database entries (Postgres), immutable logs (immuDB), and GPS streams into professional dashboards for Passengers, Operators, and Katisha Admins.

## 🎯 Objectives
- Provide Passengers with a clear view of their **Travel History** and **Credit Balance**.
- Give Bus Agencies a **Real-time Fleet Dashboard** and **Audit-Ready Financials**.
- Implement **Geospatial Analytics** to track driver behavior and route popularity.

## 🛠 Tech Stack & Dependencies
* **[Chart.js](https://www.chartjs.org/) / [Recharts](https://recharts.org/):** For rendering revenue and passenger trends.
* **[ExcelJS](https://github.com/exceljs/exceljs):** To generate downloadable financial reports for agencies.
* **[Leaflet.heat](https://github.com/Leaflet/Leaflet.heat):** To visualize route popularity via heatmaps.
* **[immuDB Node.js SDK](https://docs.immudb.io/):** For querying the immutable transaction ledger.

---

## 📅 Week 8: Operational Dashboards (Real-Time Views)

### 1. Passenger Hub (The "My Katisha" View)
- [ ] **Booking Management:** A list of upcoming and past trips with statuses (Paid, Boarded, Cancelled).
- [ ] **The "Wallet" UI:** Display the passenger's current "Travel Credit" balance (from the Week 4 No-Refund policy).
- [ ] **Quick Action:** A "Reschedule" button that uses Travel Credit to book a new trip in one click.

### 2. Agency Fleet Command
- [ ] **Live Overview:** A dashboard showing:
    - Total buses currently on the road.
    - Real-time boarding progress (e.g., "Kigali-Musanze 08:00: 32/40 Boarded").
- [ ] **Alerts Panel:** Real-time notifications for speeding buses or late departures based on GPS data.

### 3. Katisha Super-Admin
- [ ] **Global Dashboard:** Total daily revenue, active agencies, and system-wide passenger volume.
- [ ] **Agency Onboarding:** UI for the Katisha team to verify and activate new bus companies.

---

## 📅 Week 9: Analytics & Financial Intelligence (The "Big Picture")

### 1. Audit-Ready Financials (immuDB Integration)
- [ ] **Revenue Reports:** Generate daily/weekly/monthly statements for agencies.
- [ ] **Tamper-Proof Verification:** A "Verify" badge on reports that checks the immuDB state to prove the data hasn't been altered.
- [ ] **Reconciliation Logic:** Automate the calculation of: `(Total Ticket Sales) - (Katisha Commissions) = (Agency Payout)`.

### 2. Geospatial & Performance Analytics
- [ ] **Route Heatmaps:** Identify the most popular pickup/drop-off points to optimize scheduling.
- [ ] **Driver Safety Scorecards:** Use GPS "pings" to calculate average speed and identify frequent speeding incidents.
- [ ] **Occupancy Trends:** Visualize which days of the week have the highest "Empty Seat" rates to help agencies adjust pricing or capacity.

---

## 📂 Useful Resources for Weeks 8-9
* **[Building Dashboards with Node.js](https://blog.logrocket.com/building-dashboard-node-js-react-chart-js/):** Best practices for data aggregation.
* **[PostGIS Spatial Aggregates](https://postgis.net/docs/manual-3.1/postgis_usage.html#Spatial_Aggregates):** How to turn thousands of GPS points into route heatmaps efficiently.
* **[Financial Reporting Patterns](https://www.freecodecamp.org/news/how-to-build-a-financial-reporting-system/):** Logic for building robust reconciliation engines.
