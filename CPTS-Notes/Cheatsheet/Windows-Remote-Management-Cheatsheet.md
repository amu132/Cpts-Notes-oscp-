# Windows Remote Management Cheatsheet

## RDP
| Command | Use |
|---------|-----|
| nmap -sV -sC <IP> -p3389 --script rdp* | Full RDP scan |
| ./rdp-sec-check.pl <IP> | Security check |
| xfreerdp /u:user /p:pass /v:<IP> | Connect (Linux) |

## WinRM
| Command | Use |
|---------|-----|
| nmap -sV -sC <IP> -p5985,5986 | Scan |
| evil-winrm -i <IP> -u user -p pass | Connect + shell |

## WMI
| Command | Use |
|---------|-----|
| wmiexec.py user:pass@<IP> "command" | Remote command execution |

## Ports
| Port | Service |
|------|---------|
| 3389 | RDP |
| 5985 | WinRM HTTP |
| 5986 | WinRM HTTPS |
| 135 | WMI (initial) |
