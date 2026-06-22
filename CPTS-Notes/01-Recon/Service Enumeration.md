


# Service Enumeration

## What is it?

Service Enumeration is the process of identifying running services, applications, versions, banners, and operating system information on open ports.

Accurate service versions help us:

- Search for known vulnerabilities.
    
- Find public exploits.
    
- Identify the target operating system.
    
- Perform deeper enumeration.
    

## When to use?

- After discovering open ports.
    
- Before vulnerability assessment.
    
- Before searching for exploits.
    
- During initial enumeration of any target.
    

## Commands

```bash
# Service version detection
nmap -sV <target>

# Full port scan with service detection
sudo nmap -p- -sV <target>

# Verbose output
sudo nmap -p- -sV -v <target>

# Show scan progress every 5 seconds
sudo nmap -p- -sV --stats-every=5s <target>
```

```bash
# Packet tracing for banner analysis
sudo nmap -p- -sV -Pn -n --disable-arp-ping --packet-trace <target>
```

```bash
# Manual banner grabbing
nc -nv <target> <port>

# Example SMTP
nc -nv 10.129.2.28 25
```

```bash
# Capture traffic while grabbing banners
sudo tcpdump -i eth0 host <your_ip> and <target_ip>
```

## Key Options/Flags

|Flag|Meaning|
|---|---|
|-sV|Service version detection|
|-p-|Scan all TCP ports|
|-v|Verbose output|
|-vv|More verbose output|
|--stats-every=5s|Show scan progress every 5 seconds|
|-Pn|Skip host discovery|
|-n|Disable DNS resolution|
|--disable-arp-ping|Disable ARP discovery|
|--packet-trace|Display sent/received packets|

## Banner Grabbing

Many services reveal information immediately after a TCP connection is established.

Example:

```text
220 inlane ESMTP Postfix (Ubuntu)
```

Information obtained:

|Field|Value|
|---|---|
|Service|SMTP|
|Software|Postfix|
|Operating System|Ubuntu|
|Hostname|inlane|

Sometimes Nmap displays only partial information.

Manual banner grabbing using Netcat may reveal:

- Hostnames
    
- Software versions
    
- OS details
    
- Internal naming conventions
    

## TCP Handshake Observed in Tcpdump

### Step 1 - SYN

```text
Client -> Server
Flags [S]
```

Connection request.

### Step 2 - SYN/ACK

```text
Server -> Client
Flags [S.]
```

Server accepts connection.

### Step 3 - ACK

```text
Client -> Server
Flags [.]
```

Connection established.

### Step 4 - PSH/ACK

```text
Server -> Client
Flags [P.]
```

Server sends banner data.

Example:

```text
220 inlane ESMTP Postfix (Ubuntu)
```

### Step 5 - ACK

```text
Client -> Server
Flags [.]
```

Banner successfully received.

## My Lab Notes

- Always perform quick port discovery first.
    
- Run full port scans in the background.
    
- Use `-sV` on discovered ports.
    
- `-v` shows open ports immediately during scanning.
    
- Press `Spacebar` during Nmap scans to view progress.
    
- `--stats-every=5s` is useful for long scans.
    
- Manual banner grabbing often reveals more information than Nmap output.
    
- SMTP, FTP, SSH, POP3, IMAP, and Telnet frequently expose banners.
    
- Use `tcpdump` when learning how services communicate.
    

## Common Enumeration Workflow

```bash
# 1. Find ports
nmap -p- --min-rate 1000 <target>

# 2. Enumerate services
nmap -sV -sC -p <ports> <target>

# 3. Manual banner grabbing
nc -nv <target> <port>

# 4. Research versions
searchsploit <service>
```

## References

- HTB Module: Nmap Fundamentals
    
- Nmap Service Detection Documentation
    
- Tcpdump Documentation
    

## MITRE

T1595 - Active Scanning