# NFS Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| `sudo nmap <IP> -p111,2049 -sV -sC` | RPC/NFS scan |
| `sudo nmap --script nfs* <IP> -sV -p111,2049` | NFS detailed scripts |
| `showmount -e <IP>` | Available exports dikhao |

## Mounting
| Command | Use |
|---------|-----|
| `mkdir target-NFS` | Mount point banao |
| `sudo mount -t nfs <IP>:/ ./target-NFS/ -o nolock` | NFS share mount karo |
| `ls -l mnt/nfs/` | Username/group ke saath list |
| `ls -n mnt/nfs/` | UID/GID ke saath list |
| `sudo umount ./target-NFS` | Unmount karo |

## Privilege Escalation Check
| Setting | Meaning |
|---------|---------|
| `no_root_squash` | SUID shell trick possible — privesc! |
| `root_squash` | Root files edit nahi kar sakta even as root |

## Ports
| Port | Service |
|------|---------|
| 111 | rpcbind |
| 2049 | NFS |
