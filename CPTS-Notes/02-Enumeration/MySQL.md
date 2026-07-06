# MySQL

## What is it?
MySQL = open-source SQL relational database, Oracle maintain karta hai.
Client-server model — MySQL server (data storage) + clients (queries).
LAMP/LEMP stack ka core component — WordPress jaisi CMS use karti hai.
MariaDB = MySQL ka fork (same original developer ne banaya).

## When to use?
Port 3306 open mile toh.
Weak/empty root password check karo.
Web app se linked ho toh — credentials web config files mein mil sakte hain.

## Commands

# Nmap MySQL scan (all scripts)
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*

# Connect (no password)
mysql -u root -h 10.129.14.132

# Connect with password (NO space after -p)
mysql -u root -pP4SSw0rd -h 10.129.14.128

# Inside MySQL shell
show databases;
use <database>;
show tables;
show columns from <table>;
select * from <table>;
select * from <table> where <column> = "<string>";
select version();

## Key Databases
| Database | Purpose |
|----------|---------|
| information_schema | Metadata — ANSI/ISO standard |
| mysql | User accounts, privileges |
| performance_schema | Performance monitoring |
| sys | Management views, host summary |

## Dangerous Settings
| Setting | Risk |
|---------|------|
| user/password in config | Plaintext credentials leak ho sakte hain |
| admin_address | Admin interface expose ho sakta hai |
| debug | Verbose error info — attack surface badhta hai |
| sql_warnings | Extra info leak errors mein |
| secure_file_priv | File import/export control |

## Key Config Files
| File | Use |
|------|-----|
| /etc/mysql/mysql.conf.d/mysqld.cnf | Main MySQL config |

## My Lab Notes
- Nmap NSE scripts (mysql-brute, mysql-enum) false positives de sakte hain — MANUALLY verify karo
- Empty root password bahut common hai forgotten/test servers mein
- -p flag ke baad space nahi dena — -pPassword sahi hai, -p Password galat
- show databases; ke baad hamesha information_schema aur mysql check karo — user data yahan hoti hai
- Web app se linked MySQL mile toh — config files (wp-config.php jaisi) mein credentials dhundho

## References
- HTB Module: Footprinting — MySQL Section
- MySQL Reference Manual

## MITRE
T1046 - Network Service Discovery
T1552.001 - Unsecured Credentials: Credentials In Files
T1078 - Valid Accounts
