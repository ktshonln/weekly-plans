# 🚍 Katisha Online: Week 2 - Search Engine & Recurring Calendar Scheduling

This week focuses on the "Marketplace" logic: how Operators schedule their fleet (including recurring daily/weekly routes) and how Passengers discover those trips.

## 🎯 Objectives
- Build a dynamic **Search & Filter** engine for passengers.
- Implement a **Calendar-based Scheduling** interface for operators.
- Develop the **Recurring Trip Engine** for automated schedule generation.

## 🛠 Tech Stack & Dependencies
* **[FullCalendar.io](https://fullcalendar.io/):** For the Operator's Week-view calendar interface.
* **[RRule.js](https://github.com/jakubroztocil/rrule):** The industry standard for handling recurrence rules (i.e., "Every 2nd Tuesday") in JavaScript.
* **[node-cron](https://www.npmjs.com/package/node-cron):** To run a background job that generates trips from templates.
* **[date-fns-tz](https://date-fns.org/docs/Time-Zones):** Essential for handling the Kigali (CAT) timezone accurately.

---

## 📅 Week 2 Deliverables

### **1. Operator: Calendar & Recurrence (Day 1-3)**
- [ ] **Calendar UI:** Implement a **Week View** where clicking a slot opens a "New Trip" modal.
- [ ] **Recurrence Modal:** Add a "Repeat" toggle. Options: *Daily, Weekly (choose days), Monthly.*
- [ ] **Backend Schema:** Create a `TripTemplates` table to store these rules.
- [ ] **The Generator:** Build a service that takes a `TripTemplate` and populates the `Trips` table for the next 14 days.

### **2. Passenger: Advanced Search API (Day 4-5)**
- [ ] **Advanced Query:** Implement `GET /trips/search` with:
    - **Fuzzy Search:** Destination/Origin names (using `ILIKE` or Postgres `pg_trgm`).
    - **Temporal Filtering:** Date range and specific time-of-day slots.
    - **Categorical Filtering:** Multi-select for Bus Companies (Agencies).
- [ ] **Efficiency:** Create a composite index in Postgres on `(origin, destination, departure_time)`.

### **3. Passenger: Results UI (Day 6-7)**
- [ ] **Frontend Search:** Build the search bar and filter sidebar.
- [ ] **Real-time Results:** Use a "Live Search" feel where results update as the user tweaks filters.
- [ ] **Availability Logic:** Ensure search results only show trips where `available_seats > 0`.

---

## 📂 Useful Resources for Week 2
* **[Postgres Trigram Indexes for Search](https://about.gitlab.com/blog/2016/03/11/trigram-indexes-in-postgresql/):** How to make searching for "Kig" vs "Kigali" lightning fast.
* **[RRule Demo](https://jakubroztocil.github.io/rrule/):** Use this to test how recurrence strings look before implementing them in your code.
* **[Handling Recurring Events in SQL](https://stackoverflow.com/questions/512504/database-design-for-recurring-events):** A deep dive into why storing "Templates" is better than storing infinite future dates.
* **[Another fronted resource](https://github.com/rasel-mahmud-dev/google-calendar-clone)
