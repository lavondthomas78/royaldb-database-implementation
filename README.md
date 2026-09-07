# RoyalDB Database Implementation

## PostgreSQL Relational Database, Security & Administration

RoyalDB is a functioning PostgreSQL relational database designed and implemented for Royal Technology Solutions, a simulated managed IT services and cybersecurity organization.

The database centralizes customer, location, device, contract, service ticket, technician, and technician-assignment data that would otherwise be distributed across spreadsheets, email, and separate systems.

This project demonstrates the complete database lifecycle from relational data modeling and SQL implementation through integrity enforcement, role-based access control, least-privilege security, backup, recovery, and validation.

## Project Objectives

RoyalDB was designed to provide Royal Technology Solutions with a centralized and structured source of operational data while reducing redundancy, improving data consistency, and supporting secure access.

The implementation focuses on:

- Centralizing customer, location, device, contract, ticket, and technician information
- Establishing relational connections between operational data
- Enforcing data integrity through primary keys, foreign keys, unique constraints, and CHECK constraints
- Supporting service-ticket tracking and technician assignments
- Implementing role-based access control and least-privilege permissions
- Protecting database availability through tested backup and recovery procedures
- Providing a scalable relational foundation for future applications, dashboards, reporting, and automation

## Database Architecture

RoyalDB is implemented in PostgreSQL using a relational architecture consisting of seven core tables:

CUSTOMER — Stores customer and organization information.

LOCATION — Represents customer locations and maintains the relationship between each location and its customer.

DEVICE — Tracks IT assets and associates each device with a customer location.

CONTRACT — Stores customer service agreements and service-level information.

TICKET — Records service requests, priorities, status, creation dates, and optional device associations.

TECHNICIAN — Stores technician information, skill levels, and employment status.

TICKET_ASSIGNMENT — Resolves the many-to-many relationship between tickets and technicians while tracking individual assignment status.

## Relational Design

The database uses primary keys, foreign keys, and defined relationships to maintain referential integrity across operational data.

A customer can have multiple locations, contracts, and service tickets.

Each location belongs to one customer and can contain multiple devices.

A service ticket belongs to one customer and may optionally reference a specific device, allowing RoyalDB to support both device-related incidents and service requests such as Microsoft 365 or VPN issues.

Technicians can be assigned to multiple tickets, and tickets can involve multiple technicians. The TICKET_ASSIGNMENT bridge table resolves this many-to-many relationship.

## Data Integrity & Validation

RoyalDB uses database-level constraints to protect the accuracy and consistency of stored data.

Primary and foreign keys enforce entity relationships and prevent invalid references between related records.

CHECK constraints restrict controlled values such as ticket priority, ticket status, device status, contract status, service level, technician status, skill level, and assignment status.

Date constraints prevent invalid conditions such as contract end dates occurring before start dates or ticket resolution and closure dates occurring before ticket creation.

Validation testing included intentional attempts to insert invalid data. PostgreSQL successfully rejected an unsupported ticket priority and a nonexistent customer reference, demonstrating that the implemented integrity controls were functioning as designed.

## Role-Based Access Control & Least Privilege

RoyalDB implements role-based access control (RBAC) using PostgreSQL group roles and separate login accounts to restrict database access according to job responsibilities.

Three non-login group roles were created:

royaldb_dba — Database administration role.

royaldb_tech — Technician role with operational access required for service-ticket work.

royaldb_readonly — Read-only role for users who require access to database information without modification privileges.

Least-privilege testing verified that the read-only account could successfully query authorized data but could not perform updates. The technician account could update ticket information while attempts to modify protected customer data were denied.

These tests demonstrate that database permissions were not only configured but also validated using accounts with different authorization levels.

## SQL Implementation & Testing

RoyalDB was implemented using PostgreSQL and SQL to create the database schema, establish relationships, enforce constraints, populate sample operational data, and validate database functionality.

The implemented database contains seven relational tables and test data representing customers, locations, devices, contracts, technicians, service tickets, and technician assignments.

SQL JOIN queries were used to retrieve related customer, ticket, and device information while preserving tickets that do not reference a specific device.

Additional queries validated the TICKET_ASSIGNMENT bridge table and demonstrated that a single ticket can be assigned to multiple technicians.

The completed implementation was validated against the live PostgreSQL database rather than relying solely on conceptual models or design documentation.

## Backup & Recovery

RoyalDB includes a tested backup and recovery process designed to protect database availability and verify recoverability.

A full PostgreSQL backup was created using the custom backup format and stored in the RoyalDB backup directory.

The backup archive was validated using PostgreSQL restore utilities to confirm that the backup could be read successfully.

Recovery testing was performed by restoring the backup into a separate database named royaldb_restore_test rather than overwriting the production RoyalDB database.

Post-restore validation confirmed that the restored database contained the expected tables and matching record counts across the seven core entities.

This process demonstrated both successful database backup and verified recovery rather than relying on backup creation alone.

## Technologies & Tools

PostgreSQL 18

pgAdmin 4

SQL

Windows Server 2025

PowerShell

Role-Based Access Control (RBAC)

Relational Database Design

Primary and Foreign Key Constraints

CHECK and UNIQUE Constraints

Database Backup and Recovery

Oracle VirtualBox

Royalty.Local Active Directory Lab Environment

## Implementation Results

The completed RoyalDB implementation contains seven operational relational tables with validated sample data.

CUSTOMER — 3 records

LOCATION — 3 records

DEVICE — 4 records

CONTRACT — 3 records

TECHNICIAN — 3 records

TICKET — 5 records

TICKET_ASSIGNMENT — 4 records

Validation confirmed successful relational JOIN operations, optional device associations for service tickets, many-to-many technician assignments, enforcement of CHECK and foreign-key constraints, and role-based access restrictions.

Backup and recovery testing restored RoyalDB into a separate test database, where record counts across all seven tables matched the source database.

The completed project demonstrates an operational PostgreSQL database with relational integrity, security controls, tested access permissions, and verified recoverability.

## Project Scope & Future Enhancements

RoyalDB currently provides the operational relational database backend for a centralized IT service-management environment. The implemented scope includes customer, location, device, contract, ticket, technician, and technician-assignment data management together with database security, integrity controls, and backup and recovery.

The current project focuses on database architecture and administration rather than development of a graphical end-user application.

Future enhancements could include:

- Web-based service-ticket submission and management
- Technician and management dashboards
- REST API integration
- Automated ticket notifications and escalation workflows
- Reporting and analytics
- Active Directory or centralized identity integration
- Expanded auditing and security monitoring
- High-availability and automated backup strategies

 ## Troubleshooting & Lessons Learned

RoyalDB provided hands-on experience troubleshooting database implementation, permissions, integrity constraints, and backup operations.

During implementation, SQL queries were validated against the physical PostgreSQL schema, including correcting queries to use the implemented snake_case column names.

Constraint testing demonstrated how database-level controls protect data integrity by rejecting invalid values and nonexistent foreign-key references.

Role-based access testing reinforced the importance of validating permissions from the perspective of each user role rather than assuming privileges were configured correctly.

Backup testing also demonstrated that creating a backup is only part of a recovery strategy. A backup should be readable, restorable, and validated after recovery. RoyalDB was therefore restored into a separate test database and its table record counts were compared with the source.

The project reinforced the importance of testing database functionality, security, and recoverability independently before considering an implementation complete.

## Repository Contents

This repository includes the SQL implementation, database documentation, and validation evidence used to demonstrate the RoyalDB design and implementation.

**SQL** — PostgreSQL schema creation, relational constraints, sample data, validation queries, and security implementation.

**Documentation** — Database implementation and administration documentation describing the RoyalDB architecture, security controls, and operational procedures.

**Evidence** — Screenshots demonstrating the implemented schema, relational queries, integrity-constraint enforcement, RBAC testing, backup validation, and successful database recovery.

## Implementation Evidence

Screenshots in the [Evidence Guide](evidence/README.md) provide visual validation of the implemented and tested RoyalDB environment.

## Project Summary

RoyalDB demonstrates the design, implementation, security, administration, and recovery of a functioning PostgreSQL relational database. The project progresses from relational data modeling into an operational database with seven interconnected tables, enforced data integrity, validated SQL queries, role-based access control, least-privilege permissions, and tested backup and recovery.

The project was implemented within the Royalty.Local enterprise home-lab environment and serves as the database foundation for the fictional Royal Technology Solutions organization.

## Author

**LaVon Thomas**  
B.S. Computer Information Systems — Cybersecurity  
Post University

