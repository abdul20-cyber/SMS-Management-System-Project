Backend (FastAPI)
File Structure:

bash
Copy code
/backend
├── main.py
└── requirements.txt
1. requirements.txt:

plaintext
Copy code
fastapi
uvicorn
2. main.py:

python
Copy code
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
from typing import List

app = FastAPI()

operators = []
metrics = []

class Operator(BaseModel):
    country: str
    operator: str

class SMSMetric(BaseModel):
    country: str
    sms_sent: int

@app.post("/operators/", response_model=Operator)
def create_operator(operator: Operator):
    operators.append(operator)
    return operator

@app.get("/operators/", response_model=List[Operator])
def get_operators():
    return operators

@app.post("/metrics/", response_model=SMSMetric)
def create_metric(metric: SMSMetric):
    metrics.append(metric)
    return metric

@app.get("/metrics/{country}", response_model=List[SMSMetric])
def get_metrics(country: str):
    country_metrics = [m for m in metrics if m.country == country]
    if not country_metrics:
        raise HTTPException(status_code=404, detail="Metrics not found")
    return country_metrics

@app.get("/")
def read_root():
    return {"message": "Welcome to the SMS Management API"}
Frontend (React)
File Structure:

java
Copy code
/frontend
├── src
│   ├── App.js
│   └── index.js
├── public
│   └── index.html
└── package.json
1. package.json:

json
Copy code
{
  "name": "sms-management-app",
  "version": "1.0.0",
  "dependencies": {
    "react": "^18.0.0",
    "react-dom": "^18.0.0",
    "axios": "^0.21.1"
  },
  "scripts": {
    "start": "react-scripts start"
  }
}
2. App.js:

javascript
Copy code
import React, { useEffect, useState } from 'react';
import axios from 'axios';

function App() {
  const [operators, setOperators] = useState([]);
  const [newOperator, setNewOperator] = useState({ country: '', operator: '' });

  useEffect(() => {
    async function fetchOperators() {
      const response = await axios.get('/operators');
      setOperators(response.data);
    }
    fetchOperators();
  }, []);

  const addOperator = async () => {
    const response = await axios.post('/operators', newOperator);
    setOperators([...operators, response.data]);
    setNewOperator({ country: '', operator: '' });
  };

  return (
    <div>
      <h1>SMS Management</h1>
      <h2>Operators</h2>
      <ul>
        {operators.map((op, index) => (
          <li key={index}>{op.country} - {op.operator}</li>
        ))}
      </ul>
      <input
        type="text"
        placeholder="Country"
        value={newOperator.country}
        onChange={(e) => setNewOperator({ ...newOperator, country: e.target.value })}
      />
      <input
        type="text"
        placeholder="Operator"
        value={newOperator.operator}
        onChange={(e) => setNewOperator({ ...newOperator, operator: e.target.value })}
      />
      <button onClick={addOperator}>Add Operator</button>
    </div>
  );
}

export default App;
3. index.js:

javascript
Copy code
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
4. public/index.html:

html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SMS Management App</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
Running the Application
Backend:

Install FastAPI:
bash
Copy code
pip install -r requirements.txt
Run the server:
bash
Copy code
uvicorn main:app --reload
Frontend:

Navigate to the frontend directory and install dependencies:
bash
Copy code
cd frontend
npm install
Start the React app:
bash
Copy code
npm start
Access the Application
Backend: API at http://localhost:8000.
Frontend: App at http://localhost:3000.
