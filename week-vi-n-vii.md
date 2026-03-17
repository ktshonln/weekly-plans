# 🚍 Katisha Online: Weeks 6-7 - Real-Time GPS & WebSockets

This phase moves Katisha into the "Live" era. We build a high-concurrency pipeline that pushes location updates from the bus hardware directly to the passenger's screen.

## 🎯 Objectives
- Build a **UDP/TCP or HTTP Listener** for GPS hardware pings.
- Implement **Socket.io** for real-time browser/app updates.
- Create the **"Live Manifest"** for operators to track their fleet.

## 🛠 Tech Stack & Dependencies
* **[Socket.io](https://socket.io/):** For the bi-directional communication between server and passengers.
* **[Redis](https://redis.io/):** To act as a "State Store" for the latest bus coordinates.
* **[Leaflet.js](https://leafletjs.com/) or [Mapbox GL JS](https://www.mapbox.com/):** For rendering the live map.
* **[PostGIS](https://postgis.net/):** To store historical "Breadcrumbs" for trip replays.

---

## 📅 Week 6: The Ingestion & Broadcast Layer

### 1. The Ingestion Engine (Day 1-3)
- [ ] **The "Ping" Listener:** Build a dedicated microservice (or route) that accepts GPS data from trackers.
- [ ] **Redis State Store:** Every ping immediately updates a Redis key: `bus:location:{bus_id}`.
- [ ] **Validation:** Verify the Tracker's IMEI against your `Buses` table to ensure only authorized devices can push data.

### 2. The WebSocket Server (Day 4-7)
- [ ] **Room Logic:** Use Socket.io "Rooms." When a passenger opens a trip, they join a room named `trip_{trip_id}`.
- [ ] **The Emitter:** When a new GPS ping arrives, the server broadcasts that coordinate *only* to the passengers in that specific `trip_{trip_id}` room.
- [ ] **Performance:** Ensure you aren't broadcasting to everyone—only to those "watching" that bus.

---

## 📅 Week 7: Live UI & ETA Engine

### 1. Passenger: Live Map UI (Day 1-4)
- [ ] **Map Integration:** Render a map on the "My Booking" page.
- [ ] **Smooth Interpolation:** Use a "Marker Slide" plugin so the bus icon moves smoothly from Point A to Point B instead of teleporting.
- [ ] **Connection Recovery:** Implement "Reconnection" logic so if the passenger goes through a tunnel, the map catches up immediately.

### 2. Operator: Fleet Dashboard (Day 5-7)
- [ ] **Fleet Overview:** A map showing all active buses for that specific agency.
- [ ] **Live Statistics:** Display current speed, heading, and distance to the next station.
- [ ] **ETA Logic:** A backend service that calculates: `(Remaining_Distance / Average_Speed)` to provide a "Minutes to Arrival" estimate.

---

## 📂 Useful Resources for Weeks 6-7
* **[Socket.io - Using Rooms](https://socket.io/docs/v4/rooms/):** Essential for segregating traffic so users only get updates for the bus they booked.
* **[Leaflet Realtime Plugin](https://github.com/perliedman/leaflet-realtime):** A great tool for updating GeoJSON layers automatically.
* **[Geofencing with PostGIS](https://postgis.net/workshops/postgis-intro/geometries.html):** How to trigger an alert when the bus is 1km away.
