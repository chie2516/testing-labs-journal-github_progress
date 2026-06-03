# Password Security

## Task 1 --- Test a Weak Password

Run:

    echo "password123" | cracklib-check

### Screenshot

<img width="1280" height="1155" alt="echo" src="https://github.com/user-attachments/assets/5067ba36-8e26-48ab-ab04-df28453e729a" />

### Questions

1.  What does the tool say about the password?
ans: The tool indicates that the password "password123" is based on a dictionary word, which means it is weak and can be guessed or cracked more easily than a strong password.

3.  Why is this password weak?
ans: The password is weak because it uses the common word "password", which appears in many password dictionaries used by attackers. It also follows a predictable pattern by simply adding numbers to the end, making it easier to guess or crack through dictionary and brute-force attacks.

### Reflection

Explain why weak passwords are dangerous.
ans: Weak passwords are dangerous because they can be easily guessed or cracked by attackers. If someone gains access to a password, they may be able to access personal information, files, or accounts without permission. This can lead to data theft, privacy breaches, and unauthorized changes to important systems.

------------------------------------------------------------------------

## Task 2 --- Test a Strong Password

Run:

    echo "Tr4!nBicyclePlanet" | cracklib-check

### Screenshot



### Questions

1.  What result did the tool return?
2.  What characteristics make this password stronger?

### Reflection

Describe at least three characteristics of strong passwords.

------------------------------------------------------------------------

## Task 3 --- Password Analysis

Evaluate the following passwords:

-   123456
-   qwerty
-   P@ssword1
-   correcthorsebatterystaple

### Questions

1.  Which passwords are weak?
2.  Which password is strongest?
3.  Why?

### Reflection

Explain what you learned about password strength.
