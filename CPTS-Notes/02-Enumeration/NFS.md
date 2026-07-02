# NFS - Network File System

## What is it?
NFS = Network File System, Sun Microsystems ne banaya.
SMB jaisa purpose — remote filesystem ko local jaisa access karna.
Linux/Unix systems ke beech use hota hai — SMB clients se directly communicate nahi kar sakta.

NFSv3 = client computer authenticate karta hai
NFSv4 = user authenticate karta hai (SMB jaisa), Kerberos support, single port 2049

Authentication mechanism NFS mein nahi hai — RPC protocol pe depend karta hai.
UNIX UID/GID matching se authorization hoti hai — client/server mismatch ho sakta hai (risk).

## When to use?
Port 111 (rpcbind) aur 2049 (nfs) open mile toh.
Trusted internal networks mein common — misconfigurations exploit karo.

## NFS Versions
| Version | Features |
|---------|----------|
| NFSv2 | Older, UDP based |
| NFSv3 | Variable file size, better errors, not backward compatible |
| NFSv4 | Kerberos, firewall friendly, single port 2049, stateful, ACLs |
| NFSv4.1 | pNFS extension, session trunking/multipathing |

## Commands

```bash
# Nmap NFS/RPC scan
sudo nmap 10.129.14.128 -p111,2049 -sV -sC

# NFS specific NSE scripts
sudo nmap --script nfs* 10.129.14.128 -sV -p111,2049

# Show available NFS shares
showmount -e 10.129.14.128

# Mount NFS share
mkdir target-NFS
sudo mount -t nfs 10.129.14.128:/ ./target-NFS/ -o nolock

# List contents with usernames/groups
ls -l mnt/nfs/

# List contents with UID/GID (root_squash check ke liye useful)
ls -n mnt/nfs/

# Unmount
cd ..
sudo umount ./target-NFS
```

## NFS Export Options (/etc/exports)
| Option | Description |
|--------|-------------|
| `rw` | Read + write permissions |
| `ro` | Read only |
| `sync` | Synchronous transfer (slow but safe) |
| `async` | Asynchronous transfer (fast) |
| `secure` | Port 1024 se upar use nahi honge |
| `insecure` | Port 1024 se upar bhi use honge |
| `no_subtree_check` | Subdirectory tree check disable |
| `root_squash` | Root ki files anonymous UID/GID ko assign hoti hain |

## Dangerous Settings
| Option | Risk |
|--------|------|
| `rw` | Read+Write — files modify ho sakte hain |
| `insecure` | Non-privileged ports use ho sakte hain |
| `nohide` | Nested mounted filesystems bhi expose hote hain |
| `no_root_squash` | Root ki files root hi rehti hain — privilege escalation risk! |

## Key Config Files
| File | Use |
|------|-----|
| `/etc/exports` | NFS shares export table |

## NSE Scripts Output
- `nfs-ls` — files with permissions, UID/GID, size
- `nfs-showmount` — available exports
- `nfs-statfs` — filesystem stats
- `rpcinfo` — running RPC services list

## My Lab Notes
- `showmount -e <IP>` se pehle available exports dekho, phir mount karo
- Mount karne ke baad `ls -n` use karo — UID/GID dikhta hai jo username se zyada useful hai privesc ke liye
- `no_root_squash` set hai toh — SUID shell upload karo root UID ke saath → privilege escalation!
- SSH access + NFS write access = SUID shell trick use karo dusre user ke files read karne ke liye
- SSH keys (`id_rsa`) directly mil sakti hain NFS share mein — direct login possible
- `-o nolock` use karo mount karte waqt — lock issues avoid karne ke liye
- Kaam ho jaye toh hamesha unmount karo — cleanup zaroori hai

## References
- HTB Module: Footprinting — NFS Section
- RFC 8881 (NFSv4.1)

## MITRE
T1021 - Remote Services
T1552.004 - Unsecured Credentials: Private Keys
T1078.003 - Valid Accounts: Local Accounts
T1548.001 - Abuse Elevation Control: Setuid/Setgid
