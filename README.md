markdown
# SMS Management System

## Overview
The SMS Management System is a full-stack application designed to control SMS sending programs and monitor related metrics. It features a real-time dashboard for insights and secure management of SMS sessions.

## Features
- Manage SMS program sessions effectively.
- Real-time metrics dashboard to visualize SMS statistics.
- Country-operator management with CRUD operations.
- Alerts via Telegram for critical events.
- Secure JWT authentication for user access.

## Project Structure
/sms-management |-- /frontend # React frontend | |-- /src | |-- /public | |-- package.json | |-- README.md # Frontend documentation |-- /backend # FastAPI backend | |-- /app | |-- main.py # Main FastAPI application | |-- models.py # Database models | |-- routes.py # API routes | |-- utils.py # Utility functions | |-- requirements.txt # Python dependencies | |-- README.md # Backend documentation |-- docker-compose.yml # For Docker deployment |-- README.md # Main project documentation

markdown

## Getting Started

### Prerequisites
- Docker and Docker Compose
- Node.js and npm
- Python 3.7 or later

### Backend Setup
1. Navigate to the `backend` directory.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
Run the FastAPI server:
bash
uvicorn app.main:app --reload
Frontend Setup
Navigate to the frontend directory.
Install dependencies:
bash
npm install
Start the React app:
bash
npm start
Docker Deployment
To run the application using Docker, navigate to the root directory and execute:

bash
docker-compose up --build
This command builds and starts both the backend and frontend services, as well as MongoDB and MySQL containers.

API Endpoints
Login: POST /login
Authenticate a user and obtain a JWT.
Start Session: POST /sessions/start
Initiate an SMS session by specifying the country and operator.
Database Design
MongoDB Schema (for configurations)
Collection: countryOperators
Fields: country, operator, high_priority, session_details
MySQL Schema (for metrics)
sql
CREATE TABLE sms_metrics (
    id INT AUTO_INCREMENT PRIMARY KEY,
    country VARCHAR(100),
    operator VARCHAR(100),
    sms_sent INT,
    success_rate DECIMAL(5,2),
    errors INT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
);
Monitoring and Alerts
Use a Prometheus client to expose metrics from your FastAPI app.
Configure Prometheus to scrape your metrics endpoint.
Contributing
Contributions are welcome! Please follow these steps:

Fork the repository.
Create a new branch: git checkout -b feature/YourFeature
Commit your changes: git commit -m "Add some feature"
Push to the branch: git push origin feature/YourFeature
Open a Pull Request.
License
This project is licensed under the MIT License. See the LICENSE file for details.

Contact
For questions or feedback, please reach out at syedabasith6@gmail.com
