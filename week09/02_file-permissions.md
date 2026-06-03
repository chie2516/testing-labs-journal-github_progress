# Understanding File Permissions

## Task 1 --- Create a File

Run:

    touch secret.txt
    ls -l secret.txt

### Screenshot
<img width="2762" height="431" alt="touch" src="https://github.com/user-attachments/assets/30fea7fe-7842-424c-8847-5fd61851b2be" />
### Questions
1.  Who owns the file?
ans: team18 owns the file.
3.  What are the default permissions?
ans: The default permissions of secret.txt are rw-rw-r-- (664), as shown by the ls -l output. The owner and group have read and write permissions, while others have read-only permission.

### Reflection

Why is file ownership important in Linux systems?
File ownership is important in Linux because it controls who can access, modify, and manage files. It helps protect data by ensuring that only authorized users can make changes, preventing unauthorized access and improving system security.
------------------------------------------------------------------------

## Task 2 --- Restrict File Permissions

Run:

    chmod 600 secret.txt
    ls -l secret.txt

### Screenshot
<img width="4109" height="807" alt="jjl" src="https://github.com/user-attachments/assets/492bd74d-1c81-4d67-be1b-80451bd47f36" />

### Questions

1.  Who can read the file now?
ans: Only the file owner (team18) can read the file. Group members and other users do not have permission to read it.

3.  Who cannot access it?
ans: Group members and all other users cannot access the file. Only the owner has permission to access it.


------------------------------------------------------------------------

## Task 3 --- Open Permissions (Security Risk)

Run:

    chmod 777 secret.txt
    ls -l secret.txt

### Screenshot

<img width="1280" height="224" alt="700" src="https://github.com/user-attachments/assets/86cdcda2-5426-4169-9421-a87eb5bc2af4" />

### Questions
1.  Who can access the file now?
ans: Everyone can access the file, including the owner, group members, and all other users. They all have read, write, and execute permissions.

3.  Why might this configuration be dangerous?
ans: This configuration is dangerous because it gives all users permission to read, modify, and execute the file. Unauthorized users could change, delete, or misuse the file, which creates a security risk.

