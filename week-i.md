# 🚍 Katisha Online: Week 1 - Core Foundation & Security

This week establishes the "Single Source of Truth" for the entire platform. We are building a multi-tenant, secure infrastructure that serves both the Passenger and Operator (Bus Agency) sides of the software.

## 🛠 Tech Stack & Dependencies

### **Core Backend & IAM**
* **[Node.js](https://nodejs.org/):** Runtime environment.
* **[CASL (`@casl/ability`)](https://casl.js.org/):** Dynamic RBAC engine to handle "Can/Cannot" logic.
* **[Passport.js](https://www.passportjs.org/) + [passport-jwt](https://www.passportjs.org/packages/passport-jwt/):** Industry-standard authentication strategy.
* **[jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken):** For generating and verifying access tokens.
* **[Argon2](https://github.com/ranisalt/node-argon2):** Modern password hashing for secure storage.

### **Database & Schema**
* **[PostgreSQL](https://www.postgresql.org/):** Primary relational database.
* **[PostGIS](https://postgis.net/):** Extension for geographic data (required for Week 7-8 tracking).
* **[Prisma ORM](https://www.prisma.io/):** Type-safe database client (recommended for fast schema migrations).

### **DevOps & Tooling**
* **[Docker](https://www.docker.com/):** For containerizing the Node.js app and Postgres.
* **[Zod](https://zod.dev/):** For validating incoming request bodies and environment variables.

---

## 🔑 Permission Architecture: Inheritance Model

We are implementing a **Hierarchical RBAC**. Instead of assigning every single permission, we assign a "Top-Level" access type. The backend expands these automatically:

| Top-Level Permission | Implied (Inherited) Permissions |
| :--- | :--- |
| **`manage`** | `create`, `read`, `update`, `delete` |
| **`write`** | `read`, `update`, `create` |
| **`read`** | `view` (read-only access) |

**Multi-tenancy Rule:** All `Operator` actions must include an `agency_id` check. A user can only manage resources where `resource.agency_id === user.agency_id`.

---

## 📂 Reference Implementations & Resources

* **[Bulletproof Node.js Architecture](https://github.com/santiq/bulletproof-nodejs):** A gold standard for folder structure (Services, Controllers, Models).
* **[CASL + Express Integration](https://github.com/stalniy/casl-express-example):** A clean example of how to plug the authorization engine into your API routes.
* **[Node.js PostgreSQL Multi-tenant Guide](https://github.com/tmknom/example-multi-tenant-postgres):** Useful for visualizing how to isolate data between different bus agencies.
* **[JWT.io Debugger](https://jwt.io/):** Essential tool for testing the payloads of your generated tokens.

---

## 📅 Week 1 Deliverables

### **1. Infrastructure (Day 1-2)**
- [ ] Initialize `docker-compose.yml` with Node and Postgres/PostGIS.
- [ ] Setup Prisma/SQL schema for `Users`, `Agencies`, `Roles`, and `Permissions`.

### **2. Identity & Access (Day 3-5)**
- [ ] Implement `POST /auth/register` (Passenger/Operator signup logic).
- [ ] Build the **Permission Expander** utility to handle Read/Write inheritance.
- [ ] Create a `checkAbility` middleware using CASL to protect sensitive routes.

### **3. Frontend & UI Gate (Day 6-7)**
- [ ] Build Login/Signup forms for Passengers.
- [ ] Create a "Staff Portal" login for Operators.
- [ ] Implement **Route Guards** to prevent unauthorized URL access (e.g., Passengers hitting `/agency/dashboard`).
