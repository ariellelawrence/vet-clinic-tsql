# Vet Clinic Database

A relational database for managing a veterinary clinic — tracking pet owners, veterinarians, and appointments. Built with **Microsoft SQL Server (T-SQL)**.

---

## Schema

| Table | Description |
|---|---|
| `OWNER` | Pet owners with contact info |
| `PET` | Pets linked to their owners |
| `VET` | Veterinarians and their specialties |
| `APPOINTMENT` | Clinic visits linking a pet to a vet |
| `APPOINTMENT_LOG` | Audit log auto-populated by trigger |

**ERD Overview:**
```
OWNER ──< PET ──< APPOINTMENT >── VET
                      │
               APPOINTMENT_LOG
```

---

## Features

### Analytical Queries
- **Query 1** — Vets with more than 2 appointments (`GROUP BY` + `HAVING`)
- **Query 2** — All pets and their appointments, including pets with none (`LEFT JOIN`)
- **Query 3** — All vets and their appointments, including vets with none (`RIGHT JOIN`)
- **Query 4** — Owners with at least one pet diagnosed as healthy (correlated subquery)

### Audit Trigger
`trg_LogAllAppointments` fires after every `INSERT` or `UPDATE` on `APPOINTMENT` and writes a timestamped record to `APPOINTMENT_LOG`.

### Stored Procedure
`GetAppointmentsByPet` accepts a `@PET_ID` parameter and returns all appointments for that pet.

```sql
EXEC GetAppointmentsByPet @PET_ID = 4;
```

---

## Getting Started

1. Open the script in **SQL Server Management Studio (SSMS)** or **Azure Data Studio**
2. Create a new database and set it as the active context
3. Run `vet_clinic.sql` in full — tables, data, queries, trigger, and stored procedure are all included

> **Note:** Sample data uses fictional characters for readability.

---

## Tech Stack

- Microsoft SQL Server
- T-SQL (triggers, stored procedures, constraints, identity columns)
