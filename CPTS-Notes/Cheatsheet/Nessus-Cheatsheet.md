# Nessus Cheatsheet

## Access
| Info | Value |
|------|-------|
| Web console | https://<IP>:8834 |

## Scan Types Quick Reference
| Type | Use |
|------|-----|
| Host Discovery | Live hosts/ports |
| Basic Network Scan | Standard vuln scan |
| Advanced Scan | Full custom |
| Web Application Tests | Web-focused |

## Credentialed Scan Auth
| OS | Method |
|----|--------|
| Linux | SSH password/key/Kerberos |
| Windows | Password/Kerberos/NTLM/LM hash |

## Report Export
| Format | Use |
|--------|-----|
| PDF/HTML | Client-facing summary |
| CSV | Tool import/analytics |
| .nessus | Raw XML data |
| .db | Full data + KB + audit trail |

## Verify False Positives
| Command | Use |
|---------|-----|
| sslscan <target> | Manual cipher suite check |
