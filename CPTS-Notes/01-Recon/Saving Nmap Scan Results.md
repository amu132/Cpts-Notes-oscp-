

# Saving Nmap Scan Results

## What is it?

Nmap allows scan results to be saved in multiple formats for later analysis, reporting, and documentation. Saving results is important during penetration tests to avoid repeating scans and to keep evidence of findings.

## When to use?

* During every engagement or lab assessment.
* When documenting discovered services and ports.
* When creating reports for clients.
* When comparing results from multiple scans.
* When importing scan results into other tools.

## Commands

```bash
# Save results in Normal format
nmap 10.129.2.28 -oN target.nmap

# Save results in Grepable format
nmap 10.129.2.28 -oG target.gnmap

# Save results in XML format
nmap 10.129.2.28 -oX target.xml

# Save results in all formats
nmap 10.129.2.28 -p- -oA target
```

```bash
# Convert XML output to HTML report
xsltproc target.xml -o target.html
```

## Key Options/Flags

| Flag | Meaning                                     |
| ---- | ------------------------------------------- |
| -oN  | Save output in normal human-readable format |
| -oG  | Save output in grepable format              |
| -oX  | Save output in XML format                   |
| -oA  | Save output in all formats                  |
| -p-  | Scan all 65535 TCP ports                    |

## Output Files

| File         | Purpose                            |
| ------------ | ---------------------------------- |
| target.nmap  | Human-readable scan results        |
| target.gnmap | Easy filtering with grep, awk, cut |
| target.xml   | Tool integration and reporting     |
| target.html  | Browser-friendly report            |

## My Lab Notes

* `.nmap` is best for manual review.
* `.gnmap` is useful for quick parsing and automation.
* `.xml` can be imported into other security tools.
* Always use `-oA` during CPTS/OSCP labs to preserve evidence.
* HTML reports can be generated using `xsltproc`.

## References

* HTB Module: Nmap Fundamentals
* Tool docs: https://nmap.org/book/output.html

## MITRE

T1595 - Active Scanning
