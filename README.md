# Oracle Database Docker Setup

This guide will help you set up Oracle Database using Docker. 

## Prerequisites

- Docker and Docker Compose should be installed on your machine. If not, download and install Docker from [here](https://www.docker.com/get-started) and follow the installation instructions for your OS.

## Steps

### 1. **Install Docker**

- Download and install Docker from the official website: [Docker Get Started](https://www.docker.com/get-started).
- Follow the installation instructions for your operating system.

### 2. **Run Oracle Database Using Docker Compose**

- When you pull this repo
```bash
    cd oracle-docker
```
- Use the following command to start the Oracle container:
```bash
    docker-compose up
```

### 3. **Access Oracle DB Using SQLPlus**

- Once the container is running, access Oracle Database using the SQLPlus command-line interface:
```bash
    sqlplus / as sysdba
```
- Execute the following commands to unlock the system account and set a new password:
    ```sql
    ALTER USER system ACCOUNT UNLOCK;
    ALTER USER system IDENTIFIED BY 123456;
    ```

### 4. **Access Oracle DB Using SQL Developer**

- Open SQL Developer and configure the connection with the following parameters:
    - **Connection Name**: (Choose any name for the connection)
    - **Username**: system
    - **Role**: default
    - **Password**: 123456 (you can change it)
    - **Hostname**: localhost
    - **Port**: 1521
    - **Service Name**: FREEPDB1

### 5. **Check Oracle DB Health Using SQL Developer**

- Run the following queries in SQL Developer to check the health of your Oracle Database:
    ```sql
    SELECT * FROM dual;
    SELECT instance_name, status FROM v$instance;
    SELECT username, account_status FROM dba_users;
    ```

### 6. **Create and Test Table in Oracle DB**

- Create a test table and insert sample data:
    ```sql
    CREATE TABLE test_table (
        id NUMBER PRIMARY KEY,
        name VARCHAR2(50)
    );

    INSERT INTO test_table (id, name) VALUES (3, 'Test User 3');
    COMMIT;

    SELECT * FROM test_table;
    ```

### 7. **Create new user**
- Create a new user:

    ```sql
    ALTER SESSION SET CONTAINER=FREEPDB1;
    CREATE USER remmani IDENTIFIED BY 123456;
    ```

---

By following these steps, you will have Oracle Database running in a Docker container on your system.