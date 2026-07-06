# MSSQL Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| locate mssqlclient | Client path find karo |
| sudo nmap --script ms-sql-info,ms-sql-empty-password -sV -p1433 <IP> | Basic MSSQL scan |
| msf6 > use auxiliary/scanner/mssql/mssql_ping | Metasploit ping scan |

## Connection
| Command | Use |
|---------|-----|
| python3 mssqlclient.py Administrator@<IP> -windows-auth | Windows Auth connect |
| python3 mssqlclient.py user@<IP> | SQL Auth connect |

## Inside Shell
| Command | Use |
|---------|-----|
| select name from sys.databases | List databases |

## Port
| Port | Service |
|------|---------|
| 1433 | MSSQL |
