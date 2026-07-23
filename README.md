# Student ERP on Docker

## Step 1: Update Packages and Install Docker

Update the instance packages and install Docker.

```bash
sudo apt update -y
sudo apt install docker.io -y
```

---

## Step 2: Install MySQL Client

Install the MySQL client.

```bash
sudo apt install mysql-client -y
```

---

## Step 3: Create Aurora MariaDB Database

1. Go to **AWS Console**.
2. Open **Aurora RDS**.
3. Select **MariaDB**.
4. Complete the required configuration.
5. Set the database password.
6. Assign the required Network/Security Group.
7. Wait until the database is available.

---

## Step 4: Clone the Repository

Clone the project repository on the EC2 instance.

```bash
git clone <repo-link>
```

---

# Database Setup

## Login to Database

```bash
mysql -h <endpoint> -u <username> -p
```

Enter the database password when asked.

---

## Create Database

```sql
CREATE DATABASE student_db;
```

---

## Create User and Grant Permission

```sql
GRANT ALL PRIVILEGES ON student_db.* TO 'username'@'localhost' IDENTIFIED BY 'your_password';
```

---

## Use Database

```sql
USE student_db;
```

---

## enter values

```sql
CREATE TABLE `students` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(255) DEFAULT NULL,
  `email` varchar(255) DEFAULT NULL,
  `course` varchar(255) DEFAULT NULL,
  `student_class` varchar(255) DEFAULT NULL,
  `percentage` double DEFAULT NULL,
  `branch` varchar(255) DEFAULT NULL,
  `mobile_number` varchar(255) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=80 DEFAULT CHARSET=latin1 COLLATE=latin1_swedish_ci;
```

---
## Exit Database

```sql
exit
```

---

# Backend Setup

## Go to Backend Directory

```bash
cd EasyCRUD/backend
```

---

## Connect Database with Backend

Open the application properties file.

```bash
nano src/main/resources/application.properties
```

Enter the Aurora MariaDB endpoint and other database details.

Finally, the database is connected to the backend.

---

## Create Dockerfile

Create a Dockerfile.

```bash
nano Dockerfile
```

> Ensure all Dockerfile steps are correct.

---

## Build Docker Image

```bash
docker build . -t <image-name>
```

---

## Run Backend Container

```bash
docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>
```

Backend setup is completed.

---

# Frontend Setup

## Connect Backend with Frontend

Open the `.env` file.

```bash
nano .env
```

Enter the **Backend EC2 Instance Public IP**.

---

## Create Dockerfile

```bash
nano Dockerfile
```

---

## Build Docker Image

```bash
docker build . -t <image-name>
```

---

## Run Frontend Container

```bash
docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>
```

Frontend setup is completed.

---

# Verify

Copy the **EC2 Instance Public IP** and paste it into your browser.

You will see the **Student Registration Form**.

Example:

```text
http://<EC2-Public-IP>:<port>
```
