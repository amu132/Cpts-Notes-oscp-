# MSSQL - Microsoft SQL Server

## What is it?
MSSQL = Microsoft ka closed-source SQL relational database.
Windows OS ke liye originally banaya — .NET framework ke saath strong native support.
Linux/MacOS versions bhi hain, but Windows targets pe zyada milega.

## When to use?
Port 1433 open mile toh — Windows environment mein common.
Credentials mile toh — mssqlclient.py se connect karo.
sa account weak/default creds check karo.

## MSSQL Clients
| Client | Note |
|--------|------|
| SSMS (SQL Server Management Studio) | GUI tool, admin machines pe saved creds mil sakte hain |
| mssqlclient.py (Impacket) | Pentesters ke liye best — pre-installed pentesting distros mein |
| mssql-cli | Command line client |
| SQL Server PowerShell | PowerShell based |
| HeidiSQL, SQLPro | Other GUI clients |

## Default System Databases
| Database | Purpose |
|----------|---------|
| master | Sabhi system info track karta hai SQL instance ke liye |
| model | Template — naye database iske structure follow karte hain |
| msdb | SQL Server Agent jobs/alerts schedule karta hai |
| tempdb | Temporary objects store karta hai |
| resource | Read-only, system objects |

## Commands

# Locate mssqlclient on system
locate mssqlclient

# Nmap MSSQL script scan (comprehensive)
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248

# Metasploit mssql_ping
msf6 auxiliary(scanner/mssql/mssql_ping) > set rhosts 10.129.201.248
msf6 auxiliary(scanner/mssql/mssql_ping) > run

# Connect with Impacket mssqlclient.py (Windows Auth)
python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth

# Inside mssqlclient shell — list databases
SQL> select name from sys.databases

## Dangerous Settings
| Setting | Risk |
|---------|------|
| No encryption enforced by default | Traffic plaintext interceptable |
| Self-signed certificates | Spoofable |
| Named pipes enabled | Extra attack surface |
| Weak/default sa credentials | Admin forget to disable — easy access |

## Authentication Types
- **Windows Authentication** = underlying OS (local SAM ya domain controller AD) login process karta hai
- Account compromise ho jaaye toh — privilege escalation + lateral movement across domain possible!

## My Lab Notes
- Port 1433 = default MSSQL port
- SSMS client-side app hai — server pe hi nahi, admin/dev machines pe bhi mil sakta hai saved creds ke saath
- Nmap script scan se hostname, instance name, version, named pipes — sab milta hai ek scan mein
- sa account = MySQL ke root jaisa — weak/empty password common vulnerability
- Windows Auth compromised account = pura domain risk mein aa sakta hai
- mssqlclient.py -windows-auth flag zaroor use karo jab AD environment ho

## References
- HTB Module: Footprinting — MSSQL Section
- Microsoft Docs: System Databases

## MITRE
T1046 - Network Service Discovery
T1078 - Valid Accounts
T1021.002 - Remote Services (lateral movement risk)
T1552.001 - Unsecured Credentials: Credentials In Files
