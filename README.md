## Port 21 - FTP

Nmap revealed that the FTP service was allowing anonymous logins, meaning that threat actors could connect to the server and read or modify files without any credential validation.

**Exploit**: Connected to the server via terminal to confirm that anonymous logins were possible.

![Anonymous Login Exploitation](port21-ftp/anonymous_login_exploitation.png)

**Solution**: Edited /etc/vsftpd.conf, changed "anonymous_enable=YES" to "anonymous_enable=NO", and then restarted service.

![Anonymous Login Solution](port21-ftp/anonymous_login_solution.png)

**Validation**: Attempted to connect to the server via the terminal again, this time receiving error 530, showcasing that the vulnerability was patched.

![Anonymous Login Validation](port21-ftp/validation_of_solution.png)


## Port 139 - SMB

Enumeration of SMB revealed that network shares were misconfigured to allow guest access.

**Exploit**: Once connected to the SMB server, I was able to look at files inside two different directories without any credential validation.

![SMB Exploitation](port139-smb/smb_exploitation.png)

**Solution**: Edited /etc/samba/smb.conf, changed "guest ok = yes" to "guest ok = no", and then restarted service.

![SMB Solution](port139-smb/smb_solution.png)

**Validation**: Attempted to look inside the same directories, and I received a denial error.

![SMB Solution Validation](port139-smb/smb_solution_validation.png)

## Port 3306 - MySQL

Enumeration revealed that the mySQL database was misconfigured to listen on all network interfaces (0.0.0.0), exposing it to external routing.

**Exploit**: Attempted to connect to the MySQL database. Received error "Access denied for user 'root'@'10.0.0.100'" confirming it was listening to external traffic instead of dropping them.

![MySQL Exploitation](port3306-MySQL/mysql_exploitation.png)

**Solution**: Edited the `mysqld.cnf` configuration file to enforce segmentation by changing "bind-address = 0.0.0.0" to "bind-address = 127.0.0.1" and then restarted service.

![MySQL Solution](port3306-MySQL/mysql_solution.png)

**Validation**: Attempted to connect to the database again and received error "Can't connect to server..." error, confirming the mySQL database is now ignoring external requests and strictly bound to localhost.

![MySQL Validation](port3306-MySQL/mysql_validation.png)

