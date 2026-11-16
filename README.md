# Equipment Maintenance System

A full-stack web application for managing equipment repair requests. Customers submit requests and track their progress. Staff prepare quotes, coordinate repairs, and close completed jobs.

Built as a team project with Angular, Spring Boot, and PostgreSQL.

## Features

| Customer portal | Staff portal |
| --- | --- |
| Submit repair requests and view their status and history | Filter requests by date and status and prepare quotes |
| Approve or reject quotes and reopen rejected requests | Record repairs or redirect work to another staff member |
| Confirm payment for completed repairs | Finalize paid requests, manage categories and staff, and export revenue reports as PDFs |

The application records payment confirmations. It does not process payment transactions.

## Technical overview

- **Frontend:** Angular 21 and TypeScript.
- **Backend:** Java 25 and Spring Boot 4.1, with REST controllers, services for business rules, and Spring Data JPA repositories.
- **Database:** PostgreSQL.
- **Access control:** Server-side sessions identify customers and staff. The backend checks request ownership, staff permissions, and allowed status transitions. A request's history records actions such as quote rejection and reassignment.

## My contributions

I implemented the core backend workflow for repair requests, including creation, listing, details, filtering, and finalization. I also implemented the services and endpoints for quotes, repairs, reassignment, and payment confirmation.

I added a shared staff permission check and standardized API error responses. On the frontend, I contributed to the customer dashboard, the request form, and the request details screen. The final frontend integration was a team effort.

## Run locally

Install JDK 25, Node.js 22.12+ within the 22.x release line, npm, and PostgreSQL. Create a PostgreSQL database named `equipment_maintenance` or use an existing local database dedicated to this app.

### Backend

Set the following variables in your terminal or IDE run configuration. Replace the example database credentials and use an SMTP account or local SMTP test service.

| Variable | Example or purpose |
| --- | --- |
| `SERVER_PORT` | `8090` |
| `DB_URL` | `jdbc:postgresql://localhost:5432/equipment_maintenance` |
| `DB_USERNAME`, `DB_PASSWORD` | Local PostgreSQL credentials |
| `MAIL_HOST`, `MAIL_PORT` | SMTP server and port |
| `MAIL_USERNAME`, `MAIL_PASSWORD` | SMTP credentials |

From the repository root:

```bash
cd backend
./mvnw spring-boot:run
```

On Windows PowerShell, use `.\mvnw.cmd spring-boot:run` from the `backend` directory.

### Frontend

Open a second terminal at the repository root:

```bash
cd frontend
npm ci
npm start
```

Open [localhost:4200](http://localhost:4200). The frontend expects the API at `http://localhost:8090`. To explore the staff workflow, use a database with a staff account already provisioned.

