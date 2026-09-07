# RoyalDB SQL Implementation

This directory contains the PostgreSQL SQL scripts used to implement, secure, and validate the RoyalDB relational database.

RoyalDB was implemented using PostgreSQL 18 on Windows Server 2025 and consists of seven interconnected relational tables supporting customer, location, device, contract, service-ticket, technician, and technician-assignment data.

## SQL Components

The SQL implementation includes:

- Database schema and table creation
- Primary and foreign key relationships
- CHECK and UNIQUE constraints
- Sample operational data
- Multi-table relational JOIN queries
- Ticket-to-technician many-to-many relationship validation
- Role-Based Access Control (RBAC)
- Least-privilege permissions
- Data-integrity validation tests
- Database administration and verification queries

## Core Tables

- `customer`
- `location`
- `device`
- `contract`
- `ticket`
- `technician`
- `ticket_assignment`

## Security

RoyalDB uses PostgreSQL group roles to separate database responsibilities:

- `royaldb_dba` — database administration
- `royaldb_tech` — operational service-ticket access
- `royaldb_readonly` — read-only access

Separate login accounts are assigned to these roles so permissions can be managed according to the principle of least privilege.

## Validation

The implementation was tested against the live PostgreSQL database. Validation included successful relational queries, intentional CHECK and foreign-key constraint violations, role-membership verification, and least-privilege testing.

Intentional error-generating tests are documented as validation procedures and are not implementation failures.

## Backup and Recovery

Backup and recovery procedures were also validated by restoring RoyalDB into a separate `royaldb_restore_test` database and comparing the recovered table record counts with the source database.

See the repository's [Implementation Evidence](../evidence/README.md) for screenshots demonstrating the live database implementation and validation results.
