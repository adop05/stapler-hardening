## Port 21 - FTP
Nmap revealed that the FTP service was allowing anonymous logins, meaning that threat actors could connect to the server and read or modify files without any credential validation.
**Exploit**: Connected to the server via terminal to confirm that anonymous logins were possible.
![Anonymous Login Exploitation](port21-ftp/anonymous_login_exploitation.png)
**Solution**: Edited /etc/vsftpd.conf, Changed anonymous_enable=YES to NO, and then restarted service.
![Anonymous Login Solution](port21-ftp/anonymous_login_solution.png)
**Validation**: Attempted to connect to the server via the terminal again, this time receiving error 530, showcasing that the vulnerability was patched.
![Anonymous Login Validation](port21-ftp/validation_of_solution.png)

