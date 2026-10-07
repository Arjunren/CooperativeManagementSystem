# Cooperative Management System

## Overview
Java API for cooperative members, savings accounts, deposits, withdrawals, ledger history, and financial summaries.

## Features
Revocable login sessions; Admin, Teller, and Member roles; member/account creation; transactional ledger operations; overdraft and duplicate-reference protection; member-owned balances; reporting.

## Technology Stack
Java 21, Javalin 7.2.3, JDBC, H2 2.5.250, JUnit 6.1.3, Maven 3.9.16, Docker.

## Requirements / Installation / Running
Install Java 21+ and Maven 3.9.16+. Run `mvn clean package` then `java -jar target/cooperative-management-system-1.0.0.jar`. The migration runs automatically.

## Environment Variables
Configure the values in `.env.example`; do not use its sample database password in production.

## Database Setup
`src/main/resources/db/migration.sql` contains the idempotent schema. Seed accounts are created on first launch.

## Running Tests
Run `mvn verify`. Four tests cover deposits, withdrawals, insufficient funds, and idempotent references.

## Default Development Accounts
`admin`, `teller`, and `member`, password `ChangeMe123!` (development only).

## API Endpoints
`POST /api/auth/login`, `POST /api/members`, `GET /api/accounts`, `POST /api/accounts/{id}/movements`, `GET /api/ledger`, `GET /api/dashboard`.

## Folder Structure
`Infrastructure` handles DB/auth/passwords, `AccountService` owns transactions, `Main` provides routes, resources contain migrations, and tests cover business rules.

## Security Notes
PBKDF2 password hashing, hashed expiring bearer tokens, server-side roles/ownership, parameterized JDBC, transaction locks, and database constraints protect account data. Use HTTPS and PostgreSQL for production.

## Known Limitations
H2 is local-demo storage. Loan amortization, interest accrual, accounting exports, MFA, and multi-branch support are outside scope.

## License
MIT
