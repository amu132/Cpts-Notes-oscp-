# Windows Remote Management Protocols (RDP, WinRM, WMI)

## What is it?
Windows servers remotely manage karne ke protocols.
3 main components: RDP (GUI), WinRM (CLI/PowerShell), WMI (system management interface).
Windows Server 2016+ mein remote management by default enabled.

## When to use?
Port 3389 (RDP), 5985/5986 (WinRM), 135 (WMI) open mile toh.
Credentials mile toh — direct access try karo.

---

# RDP (Remote Desktop Protocol)

## Key Concepts
- Port 3389 (TCP, kabhi UDP bhi)
- TLS/SSL support (Vista+) — but self-signed certs default
- NLA (Network Level Authentication) — default security check
- Application layer protocol — GUI transmit karta hai

## Commands

# Nmap RDP scan
nmap -sV -sC 10.129.201.248 -p3389 --script rdp*

# Packet trace (careful — mstshash=nmap cookie EDR detect kar sakta hai)
nmap -sV -sC 10.129.201.248 -p3389 --packet-trace --disable-arp-ping -n

# RDP Security Check tool
git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check
./rdp-sec-check.pl 10.129.201.248

# Connect via xfreerdp
xfreerdp /u:cry0l1t3 /p:"P455w0rd!" /v:10.129.201.248

## My Lab Notes
- Nmap NSE se NLA support, product version, hostname sab milta hai
- `mstshash=nmap` cookie EDR/threat hunters detect kar sakte hain — hardened networks mein risky
- Self-signed cert = certificate warning aayega, connect karte waqt "Y" confirm karo
- rdp-sec-check.pl unauthenticated protocol/encryption support check karta hai

---

# WinRM (Windows Remote Management)

## Key Concepts
- SOAP based, TCP port 5985 (HTTP), 5986 (HTTPS)
- Windows Server 2012+ mein default enabled
- WinRS (Windows Remote Shell) — arbitrary commands execute karta hai
- PowerShell remoting isi pe depend karta hai

## Commands

# Nmap WinRM scan
nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n

# PowerShell se check (from Windows)
Test-WsMan <hostname>

# Evil-WinRM — Linux se connect
evil-winrm -i 10.129.201.248 -u Cry0l1t3 -p P455w0rD!

## My Lab Notes
- Zyada common HTTP (5985) hi milta hai, HTTPS (5986) kam
- Evil-WinRM = pentesters ka go-to tool credentials milne ke baad
- Credentials mile toh direct shell access mil jaata hai

---

# WMI (Windows Management Instrumentation)

## Key Concepts
- Microsoft ka CIM implementation — WBEM ka part
- Read/write access almost sab settings pe — most critical interface
- Initial connection TCP 135, phir random port pe move ho jaata hai
- PowerShell, VBScript, WMIC se access hota hai

## Commands

# WMIexec.py (Impacket) — remote command execution
/usr/share/doc/python3-impacket/examples/wmiexec.py Cry0l1t3:"P455w0rD!"@10.129.201.248 "hostname"

## My Lab Notes
- Port 135 pe initial handshake, phir dynamic port pe shift
- wmiexec.py credentials ke saath command execution deta hai — bahut useful post-enum

## References
- HTB Module: Footprinting — Windows Remote Management Section
- rdp-sec-check: https://github.com/CiscoCXSecurity/rdp-sec-check
- evil-winrm: https://github.com/Hackplayers/evil-winrm

## MITRE
T1021.001 - Remote Services: RDP
T1021.006 - Remote Services: WinRM
T1047 - Windows Management Instrumentation
T1078 - Valid Accounts
