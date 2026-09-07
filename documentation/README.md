# RoyalDB Project Documentation

This directory contains supporting technical documentation for the RoyalDB PostgreSQL database implementation.

RoyalDB was developed as a complete relational database project for Royal Technology Solutions, a simulated managed IT services and cybersecurity organization. The documentation covers the progression from database requirements and relational modeling through SQL implementation, security administration, validation, backup, and recovery.

## Master Documentation

The primary technical document in this directory is:

**RoyalDB Database Implementation and Administration Documentation**

This document provides a consolidated overview of the implemented RoyalDB environment, including:

- Project purpose and business requirements
- PostgreSQL database architecture
- Seven-table relational schema
- Entity relationships and business rules
- Primary and foreign key implementation
- Data-integrity constraints
- SQL implementation and validation
- Role-Based Access Control (RBAC)
- Least-privilege security
- Backup and recovery procedures
- Implementation testing and troubleshooting
- Operational and administrative considerations

## Related Repository Resources

### SQL Implementation

The [`sql`](../sql/) directory contains the PostgreSQL implementation and validation scripts used to build and test RoyalDB.

### Implementation Evidence

The [`evidence`](../evidence/) directory contains screenshots demonstrating the live PostgreSQL environment, relational queries, constraint enforcement, RBAC, least-privilege testing, role membership, and database recovery validation.

## Project Scope

The current implementation focuses on the relational database backend and database administration. A graphical service-ticketing application is outside the current project scope.

The implemented database provides a foundation for future development such as web-based ticket management, dashboards, APIs, reporting, automation, centralized identity integration, and expanded security monitoring.
