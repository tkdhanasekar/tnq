Setting up **Master-Master Replication** for MariaDB on Ubuntu 24.04 involves configuring two servers to replicate to each other, meaning both servers act as masters and slaves simultaneously. This setup can be useful for high availability, load balancing, or redundancy.

Below is a step-by-step guide to set up **Master-Master Replication** on two MariaDB servers:

---

### **Pre-requisites:**

1. Two Ubuntu 24.04 servers with MariaDB installed (Server 1 and Server 2).
2. Both servers need to be able to communicate over the network.
3. Both servers should have a unique `server-id` for identification.
4. The MariaDB version on both servers should be the same (ideally).
5. **Port `3306`** must be open between both servers.

---

### **Step 1: Install MariaDB on Both Servers**

If MariaDB is not installed on both servers, install it with the following commands:

#### On both Master and Slave servers:

```bash
sudo apt update
sudo apt install mariadb-server mariadb-client
```

---

### **Step 2: Configure the Master-Master Replication on Server 1 (Master 1)**

#### 2.1. Edit the MariaDB Configuration File

Edit the MariaDB configuration file on **Server 1** to enable binary logging, set a unique server ID, and configure other replication parameters.

```bash
sudo vim /etc/mysql/mariadb.conf.d/50-server.cnf
```

In the `[mysqld]` section, make the following changes:

```ini
[mysqld]
server-id = 1                # Unique ID for Server 1 (must be different for each server)
log_bin = /var/lib/mysql/mariadb-bin  # Enable binary logging
binlog_format = mixed        # Mixed binlog format for better compatibility
bind-address = 0.0.0.0       # Allow connections from all IPs
auto_increment_increment = 2 # Set to 2 for Master-Master, avoid auto-increment conflicts
auto_increment_offset = 1    # Set to 1 for Master 1, 2 for Master 2
```
:wq!
Save and Exit
* `server-id = 1`: This is unique for each server, set to 1 on Master 1.
* `auto_increment_increment = 2` and `auto_increment_offset = 1`: These settings prevent conflicts in auto-incremented primary keys by ensuring the two masters don’t generate the same ID at the same time.



#### 2.2. Restart MariaDB on Server 1

```bash
sudo systemctl restart mariadb
```

#### 2.3. Create a Replication User on Master 1

Log in to MariaDB on **Server 1** and create a user for replication:

```bash
sudo mariadb -u root -p
```

Run the following SQL commands to create the replication user:

```sql
CREATE USER 'replica_user'@'%' IDENTIFIED BY 'replica_password';
GRANT REPLICATION SLAVE ON *.* TO 'replica_user'@'%';
FLUSH PRIVILEGES;
```

#### 2.4. Get the Binary Log Coordinates

To configure replication, you need the binary log file name and position.

```sql
SHOW MASTER STATUS;
```

Make a note of the `File` and `Position` values. These will be used on the Slave (Server 2).

---

### **Step 3: Configure the Master-Master Replication on Server 2 (Master 2)**

#### 3.1. Edit the MariaDB Configuration File on Server 2

Repeat the process for Server 2. Edit the MariaDB configuration file `/etc/mysql/mariadb.conf.d/50-server.cnf` on **Server 2**:

```bash
sudo vim /etc/mysql/mariadb.conf.d/50-server.cnf
```

In the `[mysqld]` section, make the following changes:

```ini
[mysqld]
server-id = 2                # Unique ID for Server 2
log_bin = /var/lib/mysql/mariadb-bin
binlog_format = mixed
bind-address = 0.0.0.0
auto_increment_increment = 2 # Set to 2 for Master-Master
auto_increment_offset = 2    # Set to 2 for Master 2
```
:wq! save and exit
* `server-id = 2`: Set this to 2 for Server 2.
* `auto_increment_offset = 2`: This ensures unique auto-increment IDs for Server 2.



#### 3.2. Restart MariaDB on Server 2

```bash
sudo systemctl restart mariadb
```

#### 3.3. Create the Replication User on Server 2

Log in to MariaDB on **Server 2** and create a replication user:

```bash
sudo mariadb -u root -p
```

Run the following SQL commands:

```sql
CREATE USER 'replica_user'@'%' IDENTIFIED BY 'replica_password';
GRANT REPLICATION SLAVE ON *.* TO 'replica_user'@'%';
FLUSH PRIVILEGES;
```

#### 3.4. Get the Binary Log Coordinates from Server 2

Run the following to get the binary log file and position from **Server 2**:

```sql
SHOW MASTER STATUS;
```

Note down the `File` and `Position` values, which you will need for configuring the replication on Server 1.

---

### **Step 4: Configure Server 1 (Master 1) to Replicate from Server 2**

#### 4.1. Log in to MariaDB on Server 1

```bash
sudo mariadb -u root -p
```

Run the following command to tell **Server 1** to replicate from **Server 2**:

```sql
CHANGE MASTER TO MASTER_HOST = 'master_server2_IP', MASTER_USER = 'replica_user', MASTER_PASSWORD = 'replica_password', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 805;
```

* Replace `'Server2_IP'` with the actual IP of **Server 2**.
* Replace `mysql-bin.000001` and `***` with the binary log file and position from **Server 2**.

#### 4.2. Start Replication on Server 1

```sql
START SLAVE;
```

Check the slave status to make sure replication is running:

```sql
SHOW SLAVE STATUS\G
```

Look for `Slave_IO_Running: Yes` and `Slave_SQL_Running: Yes`. If both are `Yes`, replication is working.

---

### **Step 5: Configure Server 2 (Master 2) to Replicate from Server 1**

#### 5.1. Log in to MariaDB on Server 2

```bash
sudo mariadb -u root -p
```

Run the following command to tell **Server 2** to replicate from **Server 1**:

```sql
CHANGE MASTER TO MASTER_HOST = 'master_server1_IP', MASTER_USER = 'replica_user', MASTER_PASSWORD = 'replica_password', MASTER_LOG_FILE = 'mysql-bin.000001', MASTER_LOG_POS = 805;
```

* Replace `'Server1_IP'` with the actual IP of **Server 1**.
* Replace `mysql-bin.000001` and `***` with the binary log file and position from **Server 1**.

#### 5.2. Start Replication on Server 2

```sql
START SLAVE;
```

Check the slave status:

```sql
SHOW SLAVE STATUS\G
```

If `Slave_IO_Running: Yes` and `Slave_SQL_Running: Yes` are both `Yes`, replication is working properly.

---

### **Step 6: Test Replication**

#### Test 1: Create a Table on Server 1 and Check Server 2

Create a test table on **Server 1**:

```sql
CREATE DATABASE test_replication;
USE test_replication;
CREATE TABLE test_table (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255));
INSERT INTO test_table (name) VALUES ('Alice');
```

Check if the table and data are replicated to **Server 2**:

```sql
USE test_replication;
SELECT * FROM test_table;
```

#### Test 2: Create a Table on Server 2 and Check Server 1

Create a test table on **Server 2**:

```sql
CREATE DATABASE test_replication;
USE test_replication;
CREATE TABLE test_table (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(255));
INSERT INTO test_table (name) VALUES ('Bob');
```

Check if the table and data are replicated to **Server 1**:

```sql
USE test_replication;
SELECT * FROM test_table;
```

---

### **Step 7: Monitor and Maintain**

* Monitor the replication process using `SHOW SLAVE STATUS\G` on both servers.
* Use tools like `pt-table-checksum` and `pt-table-sync` from Percona Toolkit to ensure data consistency across both servers.
* Consider setting up monitoring and alerting (e.g., using Prometheus and Grafana) to track replication status.

---

### **Troubleshooting Tips:**

* If `


SHOW SLAVE STATUS\G` shows errors, check the MariaDB logs for more detailed information.

```bash
sudo tail -f /var/log/mysql/error.log
```

* To reset the slave configuration, you can run the following:

  ```sql
  STOP SLAVE;
  RESET SLAVE ALL;
  START SLAVE;
  ```

---

With this setup, **Master-Master Replication** between **Server 1** and **Server 2** will be up and running! Both servers will replicate changes to each other in real-time.

