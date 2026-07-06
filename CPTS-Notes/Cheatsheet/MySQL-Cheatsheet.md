# MySQL Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| sudo nmap <IP> -sV -sC -p3306 --script mysql* | Full scan |
| mysql -u root -h <IP> | Connect no password |
| mysql -u root -p<password> -h <IP> | Connect with password |

## Inside MySQL Shell
| Command | Use |
|---------|-----|
| show databases; | List DBs |
| use <db>; | Select DB |
| show tables; | List tables |
| show columns from <table>; | List columns |
| select * from <table>; | Dump table |
| select version(); | MySQL version |

## Port
| Port | Service |
|------|---------|
| 3306 | MySQL |
