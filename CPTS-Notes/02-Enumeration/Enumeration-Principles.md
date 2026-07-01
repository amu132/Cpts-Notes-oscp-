# Enumeration Principles

## What is it?
Enumeration = active (scans) + passive (third-party) methods se information gather karna.
OSINT = sirf passive — enumeration se alag process hai.
Enumeration ek loop hai — jo milta hai usse aur deeper jaate hain.

Sources: Domains, IPs, accessible services, aur bahut kuch.

## When to use?
Har pentest ka starting point — target ki infrastructure samajhne ke liye.
Services aur protocols identify karne ke liye.
Brute-force se pehle — samjho phir attack karo.

## Core Mindset
❌ Wrong approach: SSH/RDP mila → seedha brute-force karo
✅ Right approach: Pehle samjho infrastructure kaisi hai, phir plan banao

> "Our goal is not to get at the systems but to find all the ways to get there."

## 3 Enumeration Principles
| No. | Principle |
|-----|-----------|
| 1 | There is more than meets the eye — consider all points of view |
| 2 | Distinguish between what we see and what we do not see |
| 3 | There are always ways to gain more information — understand the target |

## Key Questions to Always Ask
- What can we see?
- What reasons can we have for seeing it?
- What image does what we see create for us?
- What do we gain from it?
- How can we use it?
- What can we NOT see?
- What reasons can there be that we do not see?
- What image results from what we do not see?

## My Lab Notes
- Enumeration = loop — ek cheez milti hai toh aur deeper jaao
- Brute-force = noisy — blacklist ho sakte ho, avoid karo jab tak zaruri na ho
- Technical understanding > exploitation skills — samjho pehle
- Jo nahi dikh raha woh bhi important ho sakta hai

## References
- HTB Module: Footprinting — Section 1 (Enumeration Principles)

## MITRE
T1592 - Gather Victim Host Information
T1589 - Gather Victim Identity Information
T1590 - Gather Victim Network Information
