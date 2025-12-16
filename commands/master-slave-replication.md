

### **Pre-requisites:**

1. Two Ubuntu 24.04 servers (Master and Slave).
2. MariaDB installed on both servers.
3. Both servers must be able to communicate over the network.
4. Ensure that port `3306` is open between Master and Slave.

---

### **Step 1: Install MariaDB on Both Servers**

If MariaDB is not installed on both servers, you can install it using the following commands.

#### On both Master and Slave:

```bash
sudo apt update
sudo apt install mariadb-server mariadb-client
```

### **Step 2: Configure the Master Server**

#### 2.1. Edit the MariaDB Configuration on the Master

You need to configure the master server to enable binary logging and unique server IDs.

Edit the MariaDB configuration file (`/etc/mysql/mariadb.conf.d/50-server.cnf`):

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

Find the `[mysqld]` section and make the following changes:

```
[mysqld]
server-id = 1                   # Unique ID for the master
log_bin = /var/log/mysql/mariadb-bin  # Enable binary logging
binlog_format = mixed           # Use mixed binlog format for replication
bind-address = 0.0.0.0          # Allow connections from all IPs
```

Save and close the file (`Ctrl + X`, then `Y`, and `Enter`).

#### 2.2. Restart MariaDB on the Master

```bash
sudo systemctl restart mariadb
```

#### 2.3. Create a Replication User

On the master server, log in to MariaDB and create a user that the slave can use for replication.

```bash
sudo mysql -u root -p
```

Run the following SQL commands to create the replication user:

```sql
CREATE USER 'replica_user'@'%' IDENTIFIED BY 'replica_password';
GRANT REPLICATION SLAVE ON *.* TO 'replica_user'@'%';
FLUSH PRIVILEGES;
```

Note:

* Replace `'replica_password'` with a secure password for the replication user.
* `'%'` means the user can connect from any IP (you may restrict this to the IP of the Slave for added security).

#### 2.4. Get the Master Status

Before you can configure the slave, you need to note the binary log file name and position.

```sql
SHOW MASTER STATUS;
```

Make a note of the `File` and `Position` values. You will need these for the slave configuration.

---

### **Step 3: Configure the Slave Server**

#### 3.1. Edit the MariaDB Configuration on the Slave

Edit the MariaDB configuration file on the slave to configure a unique `server-id` and to disable binary logging.

```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```

Find the `[mysqld]` section and make the following changes:

```ini
[mysqld]
server-id = 2                   # Unique ID for the slave (must be different from master)
relay-log = /var/log/mysql/mariadb-relay-bin  # Enable relay log
log_bin = /var/log/mysql/mariadb-bin        # Enable binary logging (only if you want this slave to be capable of acting as a master)
read_only = 1                    # Mark slave as read-only
```

Save and close the file.

#### 3.2. Restart MariaDB on the Slave

```bash
sudo systemctl restart mariadb
```

#### 3.3. Configure Replication on the Slave

Log in to MariaDB on the slave server and run the following commands:

```bash
sudo mysql -u root -p
```

Run the following SQL commands:

```sql
CHANGE MASTER TO
    MASTER_HOST = 'master_ip',     # IP address of the master server
    MASTER_USER = 'replica_user',  # Replication user created on the master
    MASTER_PASSWORD = 'replica_password',  # Replication user's password
    MASTER_LOG_FILE = 'mariadb-bin.000001',  # Binary log file name from SHOW MASTER STATUS on the master
    MASTER_LOG_POS =  154;  # Position from SHOW MASTER STATUS on the master
```

Replace:

* `master_ip` with the IP address of the master server.
* `mariadb-bin.000001` with the file name from `SHOW MASTER STATUS` on the master.
* `154` with the position from `SHOW MASTER STATUS`.

#### 3.4. Start the Replication Process

Start the replication process on the slave by running:

```sql
START SLAVE;
```

#### 3.5. Check Slave Status

Check the slave’s replication status to ensure there are no errors:

```sql
SHOW SLAVE STATUS\G
```

Look for the following fields:

* `Slave_IO_Running: Yes`
* `Slave_SQL_Running: Yes`

If both are `Yes`, replication is working correctly.

---

### **Step 4: Test Replication**

Now, test if replication is working properly. On the master server, create a new database or table, and check if it appears on the slave.

#### On the master:

```sql
CREATE DATABASE test_replication;
USE test_replication;
CREATE TABLE example (id INT, name VARCHAR(100));
INSERT INTO example (id, name) VALUES (1, 'Alice');
```

#### On the slave:

```sql
SHOW DATABASES;  # Check if 'test_replication' appears
USE test_replication;
SHOW TABLES;     # Check if 'example' table exists
SELECT * FROM example;  # Check if data has been replicated
```

---

### **Step 5: Set Up Monitoring and Maintenance**

* Ensure that both the master and slave servers are monitored to catch replication issues early (e.g., using `mytop`, `pt-table-checksum` for consistency, or monitoring tools like Prometheus and Grafana).
* Set up automatic failover or a secondary slave if necessary for high availability.

---

### **Step 6: Optional (Set Up Firewall/Network Security)**

To secure your replication setup, you should configure firewalls and/or VPNs. Only allow the master and slave to communicate over port 3306, and consider using SSL for replication traffic.

---

### **Troubleshooting Tips:**

* If replication doesn’t start or catches errors, check the logs on both the master and slave servers. You can view the MariaDB logs by running:

  ```bash
  sudo tail -f /var/log/mysql/error.log
  ```

* If you encounter errors related to the replication position, you might need to reset the slave:

  ```sql
  STOP SLAVE;
  RESET SLAVE ALL;
  START SLAVE;
  ```

* You can also use `SHOW SLAVE STATUS\G` to troubleshoot and check the last error.

---

With this, you should have a functioning MariaDB master-slave replication setup on Ubuntu 24.04!

