# Private Network Project

This project demonstrates the setup of a private two-tier architecture using CentOS VMs in VirtualBox. It includes a web server and a database server connected over a host-only network, simulating real-world application deployment with internal communication.

---

# 🖥️ Private Network Project

> A two-tier architecture using **VirtualBox** with **CentOS** VMs: one as a **Web Server** and the other as a **Database Server**, connected via a private/internal network. The web server hosts a PHP application that connects to a MySQL/MariaDB database running on the second VM.

---

## 🔧 Project Setup Steps

### 1. Download and Install VirtualBox
- Get the latest version from: [https://www.virtualbox.org](https://www.virtualbox.org)
- Install it on your system.

### 2. Download CentOS ISO
- Visit: [https://www.centos.org](https://www.centos.org)
- Prefer **CentOS 7 Minimal ISO** for performance and simplicity.

---

## 💡 Create Virtual Machines

### 3. Create VM 1: Web Server
- Name: `WebServer`
- Type: Linux → Red Hat (64-bit)
- RAM: 2GB  
- HDD: 20GB (dynamically allocated)

### 4. Create VM 2: Database Server
- Name: `DBServer`
- Type: Linux → Red Hat (64-bit)
- RAM: 2GB  
- HDD: 20GB

---

## 📀 Install CentOS on Both VMs

### 5. Attach CentOS ISO
- Go to **Settings > Storage** on both VMs
- Attach the CentOS ISO as boot disk

### 6. Install CentOS
- Boot into ISO and install CentOS on both machines
- Set hostname:
  - WebServer → `webserver.local`
  - DBServer → `dbserver.local`

---

## 🌐 Configure Network

### 7. Set Network Type (Internal or Host-Only)
- In VirtualBox → Settings → Network for both VMs:
  - **Adapter 1**: Enable → Attached to: **Internal Network**
  - Name: `intnet` (same for both)

### Install Apache (Both VMs)
- sudo yum install httpd -y
- sudo systemctl enable httpd
- sudo systemctl start httpd
### Install PHP (Only on WebServer)
- sudo yum install php php-mysql -y

### Install sql (Only on DBServer)
  - Install MySQL Server in DB Server
  - Command : dnf -y install mysql-server 

### Database Setup
- mysql -u root -p
- CREATE DATABASE webapp;
- CREATE USER 'udc123'@'%' IDENTIFIED BY 'root@123';
- GRANT ALL PRIVILEGES ON udc.* TO 'udc123'@'%';

  



## 📸 Screenshots

This section includes screenshots demonstrating the configuration and connectivity between the Web Server and Database Server in a virtualized environment.

---

### 1. Network Adapter Settings – Web Server  
Shows the web server's network interface configured with a **Host-Only Adapter**, ensuring isolated communication between VMs.  
![Network Settings Screenshot](https://i.postimg.cc/tCCbRCBY/Screenshot-2025-07-29-125320.png)

---

### 2. Database Server – Network IP Address in Configuration  
Displays the private IP address of the database server used in PHP configuration for MySQL connection.  
![Database Server IP in Config](https://i.postimg.cc/mrMfpcg6/Screenshot-2025-07-29-125655.png)

---

### 3. Web Server – PHP Configuration File (config.php)  
Shows the `config.php` file on the web server with the database server's IP used for the connection.  
![PHP Config File](https://i.postimg.cc/7L7h1Z8q/Screenshot-2025-07-29-131300.png)



---

### 4. Database Server – IP Address via ifconfig  
Displays the IP address assigned to the database server by running `ifconfig`. This matches the IP used in the PHP config.  
![ifconfig Output](https://i.postimg.cc/L66qdSfV/Screenshot-2025-07-29-130513.png)

---

### 5. Web Server – ping to Database Server  
Demonstrates that the web server can **successfully ping** the database server, indicating proper network connectivity.  
![Ping Success](https://i.postimg.cc/CxRz14cB/Screenshot-2025-07-29-130711.png)

---

### 6. Web Application – Successful Database Connection  
Shows the web application running successfully and fetching data from the database server, confirming a valid connection.  
![Web App Output](https://i.postimg.cc/L85ZPS8s/Screenshot-2025-07-29-130409.png)

---

### 7. Database Server – MySQL Service Running  
Shows that the **MySQL service is active and listening** on the expected port, ready to handle incoming connections.  
![MySQL Status](https://i.postimg.cc/L4vX3W7g/Screenshot-2025-07-29-131445.png)

---

> ✅ **Conclusion:**  
These screenshots validate the successful setup of a two-VM environment where the web server and database server communicate using a private network. The PHP application can connect to MySQL using the internal IP, and services are running as expected.

