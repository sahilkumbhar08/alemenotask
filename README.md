Credit Approval System
Overview
A Django-based credit approval system with RESTful APIs for customer registration, loan eligibility checking, loan creation, and loan viewing. The application uses PostgreSQL as the database and Celery for background tasks to ingest data from Excel files. The entire application is dockerized.
Setup Instructions

Clone the repository:
git clone <repository-url>
cd credit_approval_system


Create data directory and add Excel files:Create a data/ directory in the project root and place customer_data.xlsx and loan_data.xlsx files there.

Build and run with Docker:
docker-compose up --build


Ingest initial data:Run the following commands in a new terminal:
docker-compose exec web python manage.py shell
>>> from credit_approval.tasks.ingest_data import ingest_customer_data, ingest_loan_data
>>> ingest_customer_data.delay()
>>> ingest_loan_data.delay()


Run tests (optional):
docker-compose exec web python manage.py test



API Endpoints

POST /register: Register a new customer
POST /check-eligibility: Check loan eligibility
POST /create-loan: Create a new loan
GET /view-loan/<loan_id>: View loan details
GET /view-loans/<customer_id>: View all loans for a customer

Notes

The application uses compound interest for monthly installment calculations.
Credit score is calculated based on past loans, on-time payments, current year activity, and loan volume.
The application is dockerized with PostgreSQL and Redis for Celery tasks.
