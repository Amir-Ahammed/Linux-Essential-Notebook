# How To Install MySQL on Ubuntu 20.04

MySQL is an open-source database management system, commonly installed as part of the popular LAMP (Linux, Apache, MySQL, PHP/Python/Perl) stack. It implements the relational model and uses Structured Query Language (better known as SQL) to manage its data.

### Step 1 — Installing MySQL

* Update the package
  ```
  sudo apt update
  ```
* Install the mysql-server package:
  ```
  sudo apt install mysql-server
  ```
* Ensure that the server is running:
  ```
  sudo systemctl start mysql.service
  ```

### Step 2 — Configuring MySQL

* Open up the MySQL prompt:
  ```
  sudo mysql
  ```
* Change the root user’s authentication method (`mysql_native_password`):
  ```
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
  ```
* After making this change, exit the MySQL prompt:
  ```
  exit
  ```
* Connect to the MySQL server as the root user:
  ```
  mysql -u root -p
  ```
