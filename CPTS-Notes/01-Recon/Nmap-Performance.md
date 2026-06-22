# Nmap - Performance

## What is it?
Scan speed optimize karna — large networks ya low bandwidth pe kaam aata hai.
RTT timeout, retries, rate, aur timing templates se control karte hain.

## When to use?
- Large network scan karna ho jaldi mein
- White-box pentest mein bandwidth pata ho
- CTF/labs mein time bachana ho
- Black-box mein cautious rehna ho (T1/T2)

## Commands

```bash
# Default scan (baseline)
sudo nmap 10.129.2.0/24 -F

# Optimized RTT timeout
sudo nmap 10.129.2.0/24 -F --initial-rtt-timeout 50ms --max-rtt-timeout 100ms

# Reduce retries (faster but may miss ports)
sudo nmap 10.129.2.0/24 -F --max-retries 0

# Min rate scan (300 packets/sec)
sudo nmap 10.129.2.0/24 -F --min-rate 300 -oN tnet.minrate300

# Timing template — insane
sudo nmap 10.129.2.0/24 -F -T 5 -oN tnet.T5

# Check found open ports from saved file
cat tnet.default | grep "/tcp" | wc -l
```

## Key Options/Flags
| Flag | Meaning |
|------|---------|
| `--initial-rtt-timeout` | Initial RTT timeout set karo |
| `--max-rtt-timeout` | Maximum RTT timeout set karo |
| `--max-retries 0` | Retry band karo — faster but miss kar sakta hai |
| `--min-rate <num>` | Minimum packets per second |
| `-T <0-5>` | Timing template |

## Timing Templates
| Template | Name | Use |
|----------|------|-----|
| -T0 | Paranoid | IDS evasion, bahut slow |
| -T1 | Sneaky | IDS evasion, slow |
| -T2 | Polite | Bandwidth bachao |
| -T3 | Normal | Default |
| -T4 | Aggressive | Fast network pe |
| -T5 | Insane | Bahut fast, results miss ho sakte hain |

## My Lab Notes
- RTT timeout kam karne se hosts miss ho sakte hain — carefully use karo
- `--max-retries 0` = fast but risky, important ports skip ho sakte hain
- `--min-rate 300` = same results, 3x faster — white-box mein use karo
- T5 fast hai but production network mein IDS trigger kar sakta hai
- Black-box mein T2/T3 safe, white-box mein T4 chalega

## References
- HTB Module: Network Enumeration with Nmap — Section 8 (Performance)
- Timing Templates: https://nmap.org/book/performance-timing-templates.html
- Performance: https://nmap.org/book/man-performance.html

## MITRE
T1595.001 - Active Scanning: Scanning IP Blocks
