## 🅿️ UTD Parking Management System

A full-cycle relational database project built for the University of Texas at Dallas campus parking infrastructure. Designed and implemented across five phases — from schema design to NoSQL migration — this system handles real-world parking operations including permit management, violation tracking, EV charging, and payment processing.

---

## 📌 Overview

Managing campus parking at scale requires more than spreadsheets. This system models the full lifecycle of a UTD parking operation: who's parked where, under what permit, and what happens when rules are broken. Built with MySQL and validated against real constraint logic, then extended into MongoDB for document-based access patterns.

---

## 🗂️ Project Phases

| Phase        | Description |
|--------------|-------------|
| I | ERD design, relational schema, normalization planning |
| II | SQL implementation — tables, constraints, data population |
| III | Testing — CRUD validation, constraint checks, performance benchmarks |
| IV| NoSQL migration to MongoDB (Insert, Get, Update via PyMongo) |
| V | Documentation, stored procedures, user guide |

---

## 🧱 Database Schema

10 normalized tables (3NF):

| Table | Purpose |
|-------|---------|
| users | Students, Faculty, Staff, Visitors with UTD email enforcement |
| vehicle | Registered vehicles with type validation |
| permit | Active/Expired/Suspended permits with date constraints |
| parking_area | Zone-based capacity tracking |
| parking_spot | Individual spots with color-coded permit types|
| temporary_permit | Short-term access permits |
| parking_violation | Citations with fine tracking |
| appeal | Violation dispute workflow |
| ev_charging_station | EV spot availability and status |
| transaction | Payment records per permit |

---

## ⚙️ Key Features

- Constraint enforcement — UTD email domain (@utdallas.edu), vehicle types, permit status values, fine amounts
- Cascading deletes — removing a user automatically cleans up their vehicles, permits, and violations
- 13+ indexes — strategically placed on foreign keys and frequently filtered columns
- 5 views — active permits, parking availability by zone, violation statistics, EV station status, recent transactions
- Stored procedures — add_new_vehicle_and_permit, process_violation, plus 9 automated data population procedures
- Role-based access control — parking_admin, parking_user, and parking_officer roles with scoped permissions
- MongoDB layer — JSON document schema mirroring relational data; Insert, Get, and Update operations via PyMongo

---

## 🔍 Sample Queries

-- Check real-time parking availability by zone
SELECT * FROM parking_availability_view WHERE Available_Spots > 0;

-- Register a new vehicle and issue a permit in one call
CALL add_new_vehicle_and_permit(1001, 'TX12345', 'Toyota Camry', 'Sedan', 'Student');

-- Issue a violation by license plate
CALL process_violation('TX00001', 'Parked in unauthorized zone', 50.00);

-- View all active permits with user info
SELECT * FROM active_permits_view;

---

## 📊 Performance Benchmarks

| Query Type | Response Time |
|------------| --------------|
| User lookup |	< 0.1s |
| Permit validation | < 0.1s |
| Vehicle registration | < 0.2s |
| Parking availability |	< 0.5s |
| Violation reports |	< 0.8s	|
| Statistical analysis |	< 1.0s |
| 100 concurrent users |	< 2s avg |

---

## 🚀 Getting Started

MySQL — run the full schema:
bash
mysql -u root -p < schema/Schema_Creation.sql

This creates the database, all tables, indexes, views, stored procedures, and populates 100 sample records.

MongoDB — run the NoSQL layer:

bashpip install pymongo

python nosql/insert.py                             # bulk load JSON data into MongoDB
python nosql/get.py <UTD_Net_ID>                   # fetch a user document
python nosql/update.py <UTD_Net_ID> <new_email>    # update a user's email

---
 
## 📁 Repository Structure

```
utd-parking-management-system/
├── schema/
│   └── Schema_Creation.sql       # Full schema: tables, indexes, views, procedures, test queries
├── nosql/
│   ├── insert.py                 # Bulk insert JSON data into MongoDB
│   ├── get.py                    # Retrieve user document by UTD_Net_ID
│   └── update.py                 # Update user email by UTD_Net_ID
└── README.md

```

## 👥 Team

Group 5 — ITSS 4380.001 Advanced Database Management, Spring 2025

| Member | Role | 
|--------|------|
| Anh Pham | 	Documentation Lead |
| Farell Febriano |	Design Consistency Lead	|
| Neha Paladugu |	Requirements Lead	|
| Shubham Ralli |	Schema Design Lead |
| Damini Putti |	Deliverables Lead	|
| Hibah Yaseen |	Quality Assessor |
