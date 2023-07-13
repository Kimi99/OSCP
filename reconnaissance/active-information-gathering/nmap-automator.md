---
description: Utilizing nmap, but completely automated shell script to save you some time
---

# Nmap automator

Github repo of the tool: [https://github.com/21y4d/nmapAutomator](https://github.com/21y4d/nmapAutomator)

### Example usage:

```
// This will run all the scans consecutively
./nmapAutomator.sh 10.10.10.63 All
```

```
Scan Types:
	Network : Shows all live hosts in the host's network (~15 seconds)
	Port    : Shows all open ports (~15 seconds)
	Script  : Runs a script scan on found ports (~5 minutes)
	Full    : Runs a full range port scan, then runs a thorough scan on new ports (~5-10 minutes)
	UDP     : Runs a UDP scan "requires sudo" (~5 minutes)
	Vulns   : Runs CVE scan and nmap Vulns scan on all found ports (~5-15 minutes)
	Recon   : Suggests recon commands, then prompts to automatically run them
	All     : Runs all the scans (~20-30 minutes)
```
