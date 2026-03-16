# 🚍 Katisha Online: Week 2 - Search Engine & Calendar Scheduling

This week focuses on the "Marketplace" logic: how Operators schedule their fleet and how Passengers discover those trips using advanced filtering.

## 🎯 Objectives
- Build a dynamic **Search & Filter** engine for passengers.
- Implement a **Calendar-based Scheduling** interface for operators.
- Enforce "Bus Availability" logic to prevent double-booking.

## 🛠 Tech Stack & Dependencies
* **[FullCalendar.io](https://fullcalendar.io/docs/react) (or similar):** For the Operator's Week-view calendar.
* **[date-fns](https://date-fns.org/):** For easy manipulation of dates and times in Node.js.
* **[PostgreSQL Gist Indexes](https://www.postgresql.org/docs/current/gist.html):** To speed up searches on origin/destination strings and timestamps.

## 🔑 Key Logic: The "Trip" Model
A **Trip** is an instance of a **Route**. 
- **Route:** (e.g., Kigali ➔ Rubavu).
- **Trip:** (e.g., Kigali ➔ Rubavu, Bus #RAA123, Departure: 2026-03-20 08:00, Price: 5000 RWF).

---

## 📅 Week 2 Deliverables

### **1. Operator: Calendar Scheduling (Day 1-3)**
- [ ] **Frontend:** Implement a **Week View** calendar using FullCalendar.
- [ ] **Interaction:** Clicking a time slot opens a modal to select a Bus, Route, and Price.
- [ ] **Backend:** Create `POST /trips` endpoint with validation logic to ensure the selected Bus isn't already assigned to another trip at that time.

### **2. Passenger: Advanced Search API (Day 4-5)**
- [ ] **Endpoint:** `GET /trips/search` with the following query params:
    - `origin` & `destination` (Partial string matching).
    - `date` (Specific day or range).
    - `startTime` & `endTime` (Filter for morning/afternoon/night).
    - `agencies` (Filter by specific bus companies).
- [ ] **Backend:** Optimize query with PostgreSQL indexes on the `origin` and `destination` columns.

### **3. Passenger: Results UI (Day 6-7)**
- [ ] **Frontend:** A "Search Results" page displaying available trips as cards.
- [ ] **Details:** Show Company Name (e.g., Trinity Express), departure time, estimated arrival, and remaining seats.
- [ ] **Filtering:** Sidebar for passengers to refine results by Price or Time without a full page reload.

---

## 📂 Useful Resources for Week 2
* **[FullCalendar React/Vue Component](https://fullcalendar.io/docs/initialize-es6):** Guide for setting up the week-view grid.
* **[Postgres ILIKE vs. Full Text Search](https://www.crunchydata.com/blog/postgres-full-text-search-vs-ilike):** Which one to use for your destination names.
* **[Handling Timezones in Node.js](https://moment.github.io/luxon/#/):** Crucial for ensuring "8:00 AM" in Kigali is recorded correctly in the DB.
* **[Another fronted resource](https://github.com/rasel-mahmud-dev/google-calendar-clone)
