# Exploring Your System's Security

## Task 1 --- List System Users

Run:

    cat /etc/passwd

### Screenshot

<img width="1280" height="1212" alt="cat" src="https://github.com/user-attachments/assets/b9c67f4b-d793-44f1-ada4-072394a9d6d8" />


### Questions

1.  How many users exist on the system?
   ans: 37 users exist on the system.
3.  Which accounts appear to be system accounts?
ans: daemon, bin, sys, sync, games, man, lp, mail, news, uucp, proxy, www-data, backup, list, irc, _apt, nobody, systemd-network, dhcpcd, systemd-timesync, messagebus, sshd, avahi, polkitd, dnsmasq, _rpc, statd, pulse, lightdm, cups-pk-helper, saned, colord, hplip, vnc and iperf3. That's are 35 system accounts.
5.  Why do operating systems create system accounts?
ans: Operating systems create system accounts to run background services and daemons securely. Rather than running all services as the all-powerful root user, each service is given its own dedicated account with limited permissions. This follows the principle of least privilege, meaning a process only has access to what it needs and nothing more. If a service is compromised, the damage is contained to that account only, protecting the rest of the system
### Reflection
Explain why understanding system users is important for cybersecurity.
ans: Understanding system users is important for cybersecurity because attackers often target service accounts to gain access to a system. If a service is compromised, the attacker operates under that account's permissions. Knowing which accounts exist allows administrators to spot any unauthorised accounts that should not be there. It also helps with monitoring system logs. If an account is accessing resources it normally would not, this could indicate a security breach. Applying the principle of least privilege, where each account only has the access it needs, also reduces the damage caused by any attack. 
In short, knowing your system users helps you understand where your system is most vulnerable.
------------------------------------------------------------------------

## Task 2 --- Inspect Running Processes

Run:

    ps aux

### Screenshot
<img width="1280" height="818" alt="ps" src="https://github.com/user-attachments/assets/deb0ecaa-413a-4435-bd7e-220929f2e10d" /> <img width="1280" height="423" alt="ps aux" src="https://github.com/user-attachments/assets/795f3473-23d7-45b0-bf9c-25a2cf34251a" />

### Questions
1.  Which processes are running as `root`?
ans: The processes running as root are:
PID 1076 — python /usr/sbin/wayvnc-control.py (VNC remote desktop)
PID 1156 — [kworker/u16:2-v3d_render] (GPU kernel worker)
PID 1311 — fusermount3 -o rw,nosuid,nodev,fsname=portal... (filesystem mounting)
PID 1542 — /usr/sbin/cups-browsed (printer service)
PID 1625 — [kworker/u17:3-events_unbound] (kernel worker thread)
3.  Why can processes running as root be dangerous?
ans: Processes running as root are dangerous because root has unrestricted access to the entire system. If an attacker exploits a vulnerability in a root process, they gain full control of the system. This means they could read or delete any file, create new accounts, install malware, or manipulate network settings.
For example, if wayvnc-control.py running as root was exploited, the attacker would have complete control over the Raspberry Pi. This is why processes should only run with the permissions they need, following the principle of least privilege, rather than running as root unnecessarily.
5.  What could happen if a malicious program ran with root privileges?
ans: If a malicious program ran with root privileges, it would have complete control over the system with no restrictions. It could delete or modify any file, install backdoors to maintain access, steal passwords and sensitive data, and cover its tracks by modifying system logs. It could also open network ports to allow remote attackers in or spread to other devices on the network. Essentially the attacker would have full control of the system, making it very difficult to recover without completely reinstalling the operating system.

### Reflection
What did you learn about system processes and security?
ans: From this lab I learned that Linux systems run many processes, most of which belong to system accounts rather than real users. Only a few processes need to run as root, and keeping that number low is important for security.
I also learned that the ps aux command is a useful tool for seeing exactly what is running on a system and who is running it. This is important because if a process is running as root that should not be, it could be a sign of a security issue or misconfiguration.
The ss -tuln command showed me which network ports are open, which is also critical for security. Open ports like SSH (22) and VNC (5900) are potential entry points for attackers if not properly secured.
Overall I learned that monitoring running processes and open ports is a key part of system security, and that the principle of least privilege, giving processes only the access they need, helps reduce the risk of a full system compromise if something goes wrong.
------------------------------------------------------------------------
## Task 3 --- Identify Open Network Ports

Run:

    ss -tuln

### Screenshot
<img width="4160" height="915" alt="ss tuln" src="https://github.com/user-attachments/assets/539c35b6-cd43-4045-8029-58715b7637d2" />
### Questions
1.  Which ports are open?
ans: The ss -tuln command revealed several open ports on the Raspberry Pi. On UDP, ports 111 (RPC portmapper), 5353 (mDNS) and two dynamic ports were open. On TCP, port 22 (SSH), port 631 (CUPS printer service), port 111 (RPC portmapper), port 5201 (iperf3) and port 5900 (VNC remote desktop) were all listening for connections. The most notable open ports from a security perspective are port 22 (SSH) and port 5900 (VNC), as these allow remote access to the system and could be targeted by attackers if not properly secured.
3.  Which services appear to be listening?
ans: Which services appear to be listening?

6:14 PM
From the ss -tuln output, the services listening are:
RPC Portmapper (port 111) — remote procedure call service
mDNS (port 5353) — local network device discovery
SSH (port 22) — remote login access
CUPS (port 631) — printer service
iperf3 (port 5201) — network speed testing
VNC (port 5900) — remote desktop access
5. Why might open ports represent a security risk?
ans: Open ports represent a security risk because each open port is a potential entry point for an attacker. Every service listening on a port could have vulnerabilities that an attacker could exploit to gain access to the system. For example, SSH on port 22 could be targeted with a brute force attack if a weak password is used, and VNC on port 5900 could allow an attacker full remote desktop access if not properly secured.
Ports that are not needed, such as iperf3 on port 5201, should be closed as they increase the attack surface of the system unnecessarily. A good security practice is to only keep ports open that are required and use a firewall to restrict access to the rest.

### Reflection
Explain the relationship between open ports and potential attack
surfaces.
Every open port represents a service that is accessible over the network, and the more open ports a system has, the larger its attack surface. This means there are more opportunities for an attacker to find a vulnerability and gain access to the system.
On this Raspberry Pi, ports such as SSH (22), VNC (5900), iperf3 (5201), CUPS (631) and RPC (111) are all open. Each of these is a possible entry point for an attacker. If any of these services are misconfigured or have a known vulnerability, they could be exploited to gain unauthorised access.
Closing ports that are not needed, such as iperf3 on port 5201, reduces the attack surface and makes the system harder to compromise. A smaller attack surface means fewer opportunities for an attacker, which is why it is good practice to only keep ports open that are absolutely necessary.
