# Student ERP Deployment on Docker

## Prerequisites

- Ubuntu EC2 Instance
- Docker installed
- Aurora RDS (MariaDB)
- Git installed
- MySQL Client
- Student ERP source code (GitHub Repository)

---

# Step 1: Update Packages and Install Docker

```bash
sudo apt update -y
sudo apt install docker.io -y
```

---

# Step 2: Install MySQL Client

```bash
sudo apt install mysql-client -y
```

---

# Step 3: Create Aurora RDS Database

1. Go to **AWS Console**.
2. Open **RDS**.
3. Click **Create Database**.
4. Select **MariaDB**.
5. Complete the required configuration.
6. Set the database password.
7. Attach the required Network/Security Group.
8. Create the database.

---

# Step 4: Clone the Project Repository

```bash
git clone <repository-url>
```

---

# Step 5: Login to MariaDB

```bash
mysql -h <RDS-endpoint> -u <username> -p
```

Enter the password when prompted.

---

# Step 6: Create Database

```sql
CREATE DATABASE student_db;
```

---

# Step 7: Create User and Grant Privileges

```sql
GRANT ALL PRIVILEGES ON student_db.* TO 'username'@'%' IDENTIFIED BY 'your_password';

FLUSH PRIVILEGES;
```

> **Note:** Replace `username` and `your_password` with your own database credentials.

---

# Step 8: Use Database

```sql
USE student_db;
```

---

# Step 9: Exit Database

```sql
exit
```

---

# Backend Setup

## Step 1: Navigate to Backend Directory

```bash
cd EasyCRUD/backend
```

---

## Step 2: Configure Database Connection

Open the application properties file.

```bash
nano src/main/resources/application.properties
```

Update the following database details:

- Aurora RDS Endpoint
- Database Name
- Database Username
- Database Password

Save the file.

---

## Step 3: Create Dockerfile

```bash
nano Dockerfile
```

Add the required Dockerfile configuration.

---

## Step 4: Build Docker Image

```bash
docker build -t <image-name> .
```

---

## Step 5: Run Backend Container

```bash
docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>
```

The backend service is now running.

---

# Frontend Setup

## Step 1: Navigate to Frontend Directory

```bash
cd ../frontend
```

---

## Step 2: Configure Backend URL

Open the environment file.

```bash
nano .env
```

Set the backend URL using your EC2 Public IP and backend port.

Example:

```text
VITE_API_URL=http://<EC2-Public-IP>:<backend-port>
```

Save the file.

---

## Step 3: Create Dockerfile

```bash
nano Dockerfile
```

Add the required Dockerfile configuration.

---

## Step 4: Build Docker Image

```bash
docker build -t <image-name> .
```

---

## Step 5: Run Frontend Container

```bash
docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>
```

The frontend service is now running.

---

# Verify Deployment

Copy the **Public IP Address** of your EC2 instance.

Open a web browser and visit:

```text
http://<EC2-Public-IP>:<frontend-port>
```

If the deployment is successful, the **Student Registration Form** will be displayed.2. Open **RDS**.
3. Click **Create Database**.
4. Select **MariaDB**.
5. Complete the required configuration.
6. Set the database password.
7. Attach the required Network/Security Group.
8. Create the database.

---

# Step 4: Clone the Project Repository

```bash
git clone <repo-link>
```

---

# Step 5: Login to MariaDB

```bash
mysql -h <RDS-endpoint> -u <username> -p
```

Enter the password when prompted.

---

# Step 6: Create Database

```sql
CREATE DATABASE student_db;
```

---

# Step 7: Create User and Grant Privileges

```sql
GRANT ALL PRIVILEGES ON student_db.* TO 'username'@'%' IDENTIFIED BY 'your_password';

FLUSH PRIVILEGES;
```

> **Note:** Replace `username` and `your_password` with your own values.

---

# Step 8: Use Database

```sql
USE student_db;
```

---

# Step 9: Exit Database

```sql
exit
```

---

# Backend Setup

## Step 1: Go to Backend Directory

```bash
cd EasyCRUD/backend
```

---

## Step 2: Connect Backend with Database

Open the application properties file.

```bash
nano src/main/resources/application.properties
```

Update the database details:

- Aurora RDS Endpoint
- Database Name
- Username
- Password

Save the file.

Backend is now connected with the database.

---

## Step 3: Create Dockerfile

```bash
nano Dockerfile
```

Write the required Dockerfile.

---

## Step 4: Build Docker Image

```bash
docker build . -t <image-name>
```

---

## Step 5: Run Backend Container

```bash
docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>
```

Backend setup completed.

---

# Frontend Setup

## Step 1: Go to Frontend Directory

```bash
cd ../frontend
```

---

## Step 2: Connect Frontend with Backend

Open the environment file.

```bash
nano .env
```

Enter the Backend EC2 Instance Public IP and required backend port.

Save the file.

---

## Step 3: Create Dockerfile

```bash
nano Dockerfile
```

Write the required Dockerfile.

---

## Step 4: Build Docker Image

```bash
docker build . -t <image-name>
```

---

## Step 5: Run Frontend Container

```bash
docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>
```

Frontend setup completed.

---

# Verify Deployment

Copy the **Public IP** of the EC2 instance.

Open a browser and access:

```text
http://<EC2-Public-IP>:<frontend-port>
```

If everything is configured correctly, the **Student Registration Form** will be displayed.
````
