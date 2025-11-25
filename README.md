# Flask-Based Student Registration Web Application

---
## Project Overview
A simple Flask web application that allows users to register students via a web form. Submitted data is stored in a MySQL database and can be retrieved/displayed. The project demonstrates form handling, backend logic, database connectivity, version control (Git/GitHub), and automated deployment using Jenkins.

 ## Architectural diagram
![screenshot](./screenshot/diagram.png)
---

## Technology Stack
- **Frontend:** HTML, CSS  
- **Backend:** Python (Flask 2.3.2)  
- **Database:** MySQL  
- **CI/CD:** Jenkins (with socat for port forwarding)  
- **Version Control:** Git & GitHub

---

## Repository (forked)
- Original: `https://github.com/swati-zampal/stud-reg-flask-app.git`  
- Fork: `https://github.com/Smolke9/stud-reg-flask-app.git`
![screenshot](./screenshot/7.jpg)
---

## Features
- Student registration form (`/`)  
- View registered students (`/students`)  
- Stores records in MySQL (`studentdb` → `students` table)  
- Runs on `0.0.0.0:5000` by default (Jenkins + socat expose to other port, e.g., 5050)  
- Automated Jenkins pipeline with stages for clone, venv creation, install, run, and health check

---

## Step 1 Installation (Local / Development)
1. Install Python 3.8+  
2. Create and activate a virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate   # macOS / Linux
venv\Scripts\activate      # Windows
```
3. Install dependencies:
```bash
pip install -r requirements.txt
# requirements.txt should include:
# Flask==2.3.2
# install mysql
# mysql-connector-python
```
## Step 2  Table Schema (MySQL)
Create database:
```sql
CREATE DATABASE studentdb;
USE studentdb;
```

Create students table:
```sql
CREATE TABLE students (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255),
  phone VARCHAR(50),
  course VARCHAR(100),
  address TEXT,
  contact VARCHAR(100)
);
```

---

4. Configure your MySQL credentials (update `app.py` or use environment variables).  
5. Run the Flask app:
```bash
export FLASK_APP=app.py
flask run --host=0.0.0.0 --port=5000
```
6. Open: `http://localhost:5000/` (or `http://<server-ip>:5050/` if using socat port forwarding).

---

## Step 3 Jenkins CI/CD Pipeline (high-level)
The provided `Jenkinsfile` automates deployment with these stages:

Install Jenkins
1. Install Jenkins server.
2. Install Git Plugin via Manage Jenkins → Manage Plugins.
•	Manage Jenkins → Manage Plugins → Available → Git Plugin 
•	Git
•	Pipeline
•	SSH Agent
•	Ansible (optional)
•	Python plugin


## Step 4: Install socat
Install socat on Jenkins agent using:
sudo apt-get install socat

**Notes:**
- On Jenkins agents, install `socat` (e.g., `sudo apt-get install socat`) to forward ports.
- Ensure Jenkins has access to required credentials and network to reach MySQL (or use a cloud-hosted DB).

---

## Application Structure
```
.
├── app.py            # Main Flask app
├── requirements.txt
├── Jenkinsfile
└── templates/
    ├── register.html
    └── students.html
```

---

## Usage
- **Register:** Fill the form at `/` to add a student.  
- **View Students:** Visit `/students` to list registered students.
## Step 5 Jenkins Pipeline Stages
8.1 Clone GitHub Repo – pulls latest code.
![](./screenshot/3.jpg)
8.2 Create Virtual Environment – isolates dependencies
8.3 Install Dependencies – Flask + MySQL connector.
8.4 Run Flask App – starts on port 5000.
![](./screenshot/4.jpg)
8.5 Verify Access and Jenkins Deploy Success – curl health check ensures app is running.
A curl command is executed to perform a final health check. A successful
response confirms that the entire deployment chain, from the Flask app to the
socat port forwarding, is working correctly
![](./screenshot/6.jpg)
---

## Step 6 On port 5000 page available 
![](./screenshot/output.jpg)
## Troubleshooting
- If Jenkins health-check `curl` fails:
  - Confirm Flask started successfully on the agent.
  - Check `socat` port forwarding is running and listening.
  - Verify DB credentials and network connectivity.
- If MySQL connection errors occur, verify user, host, and password, and that MySQL server is accessible from the app host.

---

## Conclusion
This project demonstrates:
- Clear separation of frontend, backend, and DB layers.  
- Best practices with Git/GitHub.  
- Automated CI/CD through Jenkins for reliable deployments.  
- A solid foundation for scaling and enhancements.

---

## Contact
**Suraj Molke**  
Email: `smolke9@gmail.com`  
LinkedIn: https://www.linkedin.com/in/suraj-molke-4656002a6/  
GitHub: https://github.com/Smolke9

---

## License
This repository does not include a license file in the PDF. Add a license such as MIT if you want to make the project open source.

