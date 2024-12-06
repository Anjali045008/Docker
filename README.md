
# Firebird Installation on Docker

## Objective:
The objective of this project is to demonstrate how to install **Firebird Database** (version 3.0), an open-source relational database management system (RDBMS), on **Docker**. The tutorial walks through the steps of setting up Firebird, creating a database, inserting data, and performing basic SQL operations.

---

## Introduction to Firebird:

**Firebird** is an open-source relational database management system (RDBMS) that offers many ANSI SQL features. It is widely used due to its lightweight nature, multi-platform support, and rich feature set. Firebird can be embedded into applications and provides high performance for both small and large-scale applications.

Key Features of Firebird:
- **ACID compliance**: Ensures reliable transaction processing.
- **Multi-platform support**: Works on Linux, Windows, and macOS.
- **Full ANSI SQL-92 compliance** with some additional extensions.
- **Embeddable**: Can be embedded directly into applications.

In this project, we will use **Docker** to deploy **Firebird** in a container, which simplifies the installation and management process.

---

## Learning Objectives:
By the end of this tutorial, you will be able to:
1. Install **Firebird** on **Docker**.
2. Use the **isql-fb** command-line tool to interact with the database.
3. Create a new database and manage data using SQL.
4. Understand basic Docker commands to manage containers.
5. Learn how to stop and remove Docker containers and volumes.

---

## Prerequisites:
Before proceeding with this tutorial, ensure that you have the following:
- **Docker** installed on your machine. Follow the installation guide from the [official Docker website](https://docs.docker.com/get-docker/).
- Basic understanding of **SQL** and **Docker** commands.
- Familiarity with **Firebird** or other RDBMS systems is helpful but not required.

---

## Steps to Install Firebird on Docker:

### 1. **Pull the Firebird Docker Image:**
   To begin, pull the official Firebird image from Docker Hub:
   ```bash
   docker pull jacobalberty/firebird
   ```

### 2. **Run Firebird in Docker:**
   Start a new Firebird container with the necessary environment variables. This will set up the Firebird database with a `SYSDBA` password and expose port 3050 to the host:
   ```bash
   docker run -d --name firebird -e FIREBIRD_SYSDBA_PASSWORD=anjali -p 3050:3050 -v firebird_data:/firebird/data jacobalberty/firebird
   ```

   Explanation of parameters:
   - `-d`: Run the container in detached mode.
   - `--name firebird`: Name the container as `firebird`.
   - `-e FIREBIRD_SYSDBA_PASSWORD=anjali`: Set the password for the Firebird `SYSDBA` user.
   - `-p 3050:3050`: Map port 3050 in the container to port 3050 on the host machine.
   - `-v firebird_data:/firebird/data`: Use a Docker volume to persist Firebird data.

### 3. **Check if Firebird is Running:**
   Once the container is up and running, you can check the status of the container by running:
   ```bash
   docker ps
   ```

   This will list the running containers. Look for your `firebird` container in the output.

### 4. **Connect to Firebird Database:**
   You can connect to Firebird using `isql-fb`, the command-line utility. To install the Firebird utilities (e.g., `isql-fb`), you would need to use a Linux-based system (e.g., WSL on Windows) or connect to the Firebird container directly.

   Run the following commands to connect to Firebird (from within the container or using WSL on Windows):
   ```bash
   apt update
   apt install firebird3.0-utils  # Install Firebird utilities
   isql-fb -user SYSDBA -password anjali -host localhost -port 3050
   ```

### 5. **Create a Database and Insert Data:**
   After connecting to the Firebird database, you can create a new database, define tables, and insert some data:
   ```sql
   CREATE DATABASE '/firebird/data/class.fdb' USER 'SYSDBA' PASSWORD 'anjali';

   CONNECT '/firebird/data/class.fdb' USER 'SYSDBA' PASSWORD 'anjali';

   CREATE TABLE employees (
       id INT PRIMARY KEY,
       name VARCHAR(50),
       department VARCHAR(50),
       salary DECIMAL(10, 2)
   );

   INSERT INTO employees (id, name, department, salary) VALUES (1, 'Anjali', 'Marketing', 100000.00);
   INSERT INTO employees (id, name, department, salary) VALUES (2, 'Anurag', 'IT', 60000.00);
   INSERT INTO employees (id, name, department, salary) VALUES (3, 'Vishal', 'Finance', 70000.00);

   SELECT * FROM employees;
   ```

### 6. **Stop and Remove the Firebird Container:**
   When you're done, you can stop and remove the container using the following commands:
   ```bash
   docker stop firebird
   docker rm firebird
   ```
## video

https://github.com/user-attachments/assets/a84655f3-fd35-47a1-af05-9dbb08665a84

---

## Conclusion:
In this tutorial, we successfully installed **Firebird 3.0** on **Docker**, created a new database, defined a table, and inserted sample data. This approach simplifies database management by leveraging Docker’s containerization capabilities, making it easier to deploy, scale, and manage Firebird instances.

---

## Future Improvements:
1. **Docker Compose**: Automate the Firebird container setup and other services using **Docker Compose**.
2. **Backup and Restore**: Implement methods for backing up and restoring Firebird databases inside Docker.
3. **Firebird GUI Tools**: Integrate Firebird management tools like **Flamerobin** or **DBeaver** for a more user-friendly experience.
4. **Security Enhancements**: Strengthen the security of Firebird containers by enforcing stricter password policies and limiting container access.
5. **Scalability**: Explore Docker Swarm or Kubernetes for scaling Firebird containers in a distributed environment.

---

## References:
- [Firebird Official Website](https://firebirdsql.org/)
- [Docker Documentation](https://docs.docker.com/)
- [Firebird SQL Documentation](https://firebirdsql.org/en/reference-manuals/)

---
