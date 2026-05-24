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
