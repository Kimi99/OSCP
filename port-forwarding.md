---
description: Basic info and how to do it
---

# Port forwarding

Port forwarding is useful when there are some services running on the machine internally and are not accessible from the outside. They listen on some internal ports that are closed for the outside world.

For example machine **Poison** from HTB had a [tightVNC ](https://en.wikipedia.org/wiki/TightVNC)service listening internally on ports 5801 and 5901.&#x20;

In order to access this service, you need to forward those ports through some connection that you have access to, in this example there is an SSH connection available.

From Wikipedia:

[_Connections from an SSH client are forwarded, via an SSH server, to the intended destination server. The SSH server is configured to redirect data from a specified port (which is local to the host that runs the SSH client) through a secure tunnel to some specified destination host and port. The local port is on the same computer as the SSH client, and this port is the "forwarded port". On the same computer, any client that wants to connect to the same destination host and port can be configured to connect to the forwarded port (rather than directly to the destination host and port). After this connection is established, the SSH client listens on the forwarded port and directs all data sent by applications to that port, through a secure tunnel to the SSH server. The server decrypts the data, and then redirects it to the destination host and port._](https://en.wikipedia.org/wiki/Port\_forwarding)



To create an SSH tunnel and forward the port, you can use this command:

```bash
// SSH tunnel
┌──(kali㉿kali)-[~/Desktop/HTB/Poison]
└─$ ssh -L 9001:127.0.0.1:5901 charix@10.10.10.84
```

This will create a socket and bind it to port 9001 on local machine. Any traffic inbound for this port will be forwarded through the SSH connection (tunnel) to the localhost:5901 on target machine. To check if the tunnel is set up correctly use the **netstat** (or **ss**) command and grep for listening:

```bash
┌──(kali㉿kali)-[~/Desktop/HTB/Poison]
└─$ netstat -an |grep LIST
tcp        0      0 127.0.0.1:9001          0.0.0.0:*               LISTEN     
tcp6       0      0 ::1:9001                :::*                    LISTEN
```

Effectively this will allow us to target the VNC service from the attacker machine like this:

```bash
// Using SSH tunnel
┌──(kali㉿kali)-[~/Desktop/HTB/Poison]
└─$ vncviewer -passwd secret localhost:9001
```

Note that we use localhost:9001 since our machine is set up to listen on that port.
