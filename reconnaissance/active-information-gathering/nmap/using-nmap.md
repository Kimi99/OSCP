---
description: Variety of commands and use cases that I've came across
---

# Using nmap

```
# Stealthy
nmap -sS <TARGET_IP>

# Scan all ports, might take a while
nmap -p- <TARGET_IP>

# Scan for UDP ports
nmap -sU <TARGET_IP>

# Scan for version, uses NSE-scripts to try and identify the OS and service versions
nmap -sC -sV -O <TARGET_IP>

# GO-TO scan
nmap -sC -sV -oA <FILE_PATH> <TARGET_IP>

# Fast scan
nmap -F <TARGET_IP>
nmap -sS -p- -T5 -vvv <TARGET_IP>

# Scan the most common 100 ports
nmap --top-ports 100 <TARGET_IP>

# Scaning for vulnerabilities
nmap --script vuln <TARGET_IP>
```

Find more nmap scripts: [https://nmap.org/nsedoc/scripts](https://nmap.org/nsedoc/scripts/)

```
// To find the scripts on your machine run:
locate *.nse

// Script help
-script-help <SCRIPT_NAME>
```

Some useful nmap tags:

* \-p 22, 80, 443 - Scan only the listed ports, might be useful to start this scan after a fast full port scan
* \-v - Verbosity level, -vvv is the highest one. You can start the all port scan and increase the verbosity to get port information on the go. You can also press the V-key to increase the verbosity while the scan is running
* \-oA - output all formats of the scan result to 3 files with different types (.gnmap, .nmap, .xml)
* \-A - Enable OS detection, version detection, script scanning, and traceroute
* \+ in the --script tag directs nmap to execute the script no matter what

Useful combination: start the all port scan with high level verbosity and wait for a few moments. After you have some findings, start the dedicated port scan (using -p) to further enumerate the existing ports. The all port scan can continue working in the background.

Don't forget the **UDP** ports!

### Scanning an IP range:

You might need a scan for several machines on the same IP range. This will scan all the machines on the given IP range.

```
// -sn flag stops nmap from running port-scans (speeds up the process)
nmap -vvv -sn <TARGET_IP>/24
```
