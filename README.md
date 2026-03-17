# Katisha Online Weekly Roadmap

<p align="center">
	<img src="https://img.shields.io/badge/Katisha%20Online-Engineering%20Roadmap-0A6EBD?style=for-the-badge&logo=googlemaps&logoColor=white" alt="Katisha Online banner" />
</p>

<p align="center">
	<img src="https://img.shields.io/badge/Phase-Foundation%20to%20Analytics-14532D?style=flat-square" alt="Phase badge" />
	<img src="https://img.shields.io/badge/Weeks-1%20to%209-1D4ED8?style=flat-square" alt="Weeks badge" />
	<img src="https://img.shields.io/badge/Stack-Node.js%20%7C%20PostgreSQL%20%7C%20Socket.io%20%7C%20immuDB-F97316?style=flat-square" alt="Stack badge" />
	<img src="https://img.shields.io/badge/Status-Planning%20in%20Progress-7C3AED?style=flat-square" alt="Status badge" />
</p>

<p align="center">
	🚍 📅 🔐 💳 📲 📡 📊
</p>

This repository contains a structured 9-week execution plan for building **Katisha Online**, a multi-tenant bus transport platform for passengers, operators, drivers, and super-admins.

## What This Plan Covers

- Secure multi-tenant identity and permissions (RBAC with inheritance).
- Operator trip scheduling, including recurring routes.
- Passenger search and booking flow with payment integration.
- Immutable accounting and transactional messaging.
- Fraud-resistant dynamic QR boarding and driver manifests.
- Real-time GPS tracking with WebSocket broadcasts.
- Operational dashboards and analytics (financial + geospatial).

## Week Files

| Week(s) | Focus Area | File |
| :--- | :--- | :--- |
| Week 1 | Core foundation, IAM, RBAC, tenant isolation | [week-i.md](./week-i.md) |
| Week 2 | Search, filters, calendar scheduling, recurrence | [week-ii.md](./week-ii.md) |
| Weeks 3-4 | Payments, booking state machine, immuDB, SMS | [week-iii-n-iv.md](./week-iii-n-iv.md) |
| Week 5 | Dynamic QR validation and driver operations | [week-v.md](./week-v.md) |
| Weeks 6-7 | Real-time GPS ingestion, WebSockets, ETA | [week-vi-n-vii.md](./week-vi-n-vii.md) |
| Weeks 8-9 | Dashboards, reporting, route intelligence | [week-viii-n-ix.md](./week-viii-n-ix.md) |

## Roadmap Summary

### Week 1: Foundation & Security
- Bootstrap Dockerized backend + Postgres/PostGIS.
- Define schema for users, agencies, roles, and permissions.
- Implement auth (`/auth/register`, JWT strategy, password hashing).
- Add CASL-based permission checks with inherited access levels (`manage`, `write`, `read`).
- Enforce strict agency scoping for all operator actions.

### Week 2: Search & Recurring Scheduling
- Build operator calendar week view and recurring trip templates.
- Generate trips automatically from recurrence rules.
- Deliver advanced trip search API with fuzzy, temporal, and categorical filters.
- Build responsive passenger search UI with live results and seat availability checks.

### Weeks 3-4: Financial Engine & Messaging
- Create booking lifecycle (`INITIATED` to `COMPLETED/FAILED`) with timeout cleanup.
- Integrate MTN MoMo and Airtel payment flows + secure callbacks.
- Record passenger debit, agency credit, and platform fee in immuDB.
- Add ledger verification and ticket delivery via Movetech SMS.

### Week 5: Dynamic QR & Driver Workflow
- Generate refreshing QR payloads using time-windowed secure signatures.
- Build driver-specific manifest pages and scanning flow.
- Validate signatures, timestamp freshness, payment state, and boarding status in real time.
- Return clear green/red boarding outcomes and prevent QR replay.

### Weeks 6-7: Live GPS & Fleet Tracking
- Create ingestion layer for tracker pings (UDP/TCP/HTTP pattern).
- Cache latest coordinates in Redis and validate tracker identity (IMEI).
- Use Socket.io rooms to broadcast only to relevant trip viewers.
- Build live map, reconnection handling, fleet command dashboard, and ETA calculation.

### Weeks 8-9: Dashboards & Advanced Analytics
- Launch passenger travel history and wallet/credit insights.
- Deliver agency operational dashboard with boarding progress and alerts.
- Build super-admin global KPIs and agency onboarding views.
- Add tamper-proof financial reports, reconciliation logic, and route heatmaps.
- Generate driver scorecards and occupancy trend analytics.

## Suggested Delivery Sequence

1. Complete platform security and schema baseline (Weeks 1-2).
2. Lock down payments and immutable accounting (Weeks 3-4).
3. Ship secure boarding and field tooling (Week 5).
4. Enable live operations and tracking (Weeks 6-7).
5. Finish with intelligence and decision-support dashboards (Weeks 8-9).

## Quick Notes

- Timezone-sensitive scheduling should consistently use Kigali/CAT handling.
- Multi-tenancy (`agency_id`) boundaries remain a non-negotiable rule.
- Real-time modules should optimize scoped broadcasts to avoid global fan-out.
- Financial outputs should always be cross-verifiable against immuDB state.
