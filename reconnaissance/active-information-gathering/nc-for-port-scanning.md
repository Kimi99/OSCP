---
description: You can use netcat to scan ports with -z flag.
---

# nc (for port scanning)

Bash script to scan port range (remove proxychains if not needed):

```bash
for port in {4800..4900}; do proxychains nc -zv -w1 IP $port 2>&1 | grep OK; done

# nc.traditional port scanning
proxychains -q /usr/bin/nc.traditional -zv IP 9000-9100 -w 1 # (Scan port range 9000-9001)
```
