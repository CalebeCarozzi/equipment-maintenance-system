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

## How a repair request works

1. A customer submits a request with the equipment, the problem, and a category.
2. Staff prepare a quote. The customer can approve it, reject it with a reason, or reopen a rejected request.
3. Staff record the repair and instructions for the customer, or redirect the request to another staff member.
4. The customer confirms payment, and staff close the request.

The backend validates each status change. Customers can only access their own requests, and while a request is marked as redirected, only the receiving staff member can access it through staff request views. The request history tracks changes throughout the process.
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

