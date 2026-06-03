# Exploring Your System's Security

## Task 1 --- List System Users

Run:

    cat /etc/passwd

### Screenshot

<img width="1280" height="1212" alt="cat" src="https://github.com/user-attachments/assets/a3f83b34-0c1d-4da1-a2c4-376cc01c7823" />


### Questions

1.  How many users exist on the system?
ans: 
3.  Which accounts appear to be system accounts?
4.  Why do operating systems create system accounts?

### Reflection

Explain why understanding system users is important for cybersecurity.

------------------------------------------------------------------------

## Task 2 --- Inspect Running Processes

Run:

    ps aux

### Screenshot



### Questions

1.  Which processes are running as `root`?
2.  Why can processes running as root be dangerous?
3.  What could happen if a malicious program ran with root privileges?

### Reflection

What did you learn about system processes and security?

------------------------------------------------------------------------

## Task 3 --- Identify Open Network Ports

Run:

    ss -tuln

### Screenshot

<img width="4160" height="915" alt="ss tuln" src="https://github.com/user-attachments/assets/f7e311b3-292a-4f15-a1fa-c95e091b9cc8" />

### Questions

1.  Which ports are open?
2.  Which services appear to be listening?
3.  Why might open ports represent a security risk?

### Reflection

Explain the relationship between open ports and potential attack
surfaces.
