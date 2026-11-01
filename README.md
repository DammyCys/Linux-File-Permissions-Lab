# Linux File Permissions & Group Management Lab

## Project Overview
While working through the Google IT Support Professional Certificate labs, I built a hands-on project to practice secure account management and directory restrictions on a Linux system (Ubuntu via WSL). 

The goal was to create a corporate directory (`/opt/tech_file`) assigned to a group called `tech_team`, allowing team members to work together while using the **Sticky Bit** safety lock to prevent users from accidentally deleting each other's files.

## Steps and Terminal Commands Executed

### 1. Creating the Secure Group and Folder Structure
I created the team group and allocated a neutral folder outside the home directory using root-level privileges:
```bash
sudo addgroup tech_team
sudo mkdir /opt/tech_file
```

### 2. Group Ownership Alignment
I updated the group ownership of the folder to ensure members of our team could access it:
```bash
sudo chown :tech_team /opt/tech_file
```

### 3. Hardening the Directory (Applying the Sticky Bit)
To enforce the restriction preventing cross-user file deletions, I applied permissions using `chmod 1770`:
```bash
sudo chmod 1770 /opt/tech_file
```
Running `ls -ld /opt/tech_file` confirmed the permissions state as `drwxrwx--t`. The `t` at the end verifies that the Sticky Bit is active.

![Terminal showing Sticky Bit Verification](https://github.com/DammyCys/Linux-File-Permissions-Lab/blob/main/Screenshot%20(6)_065426.png)


### 4. Multi-User Verification & Testing
I tested the configuration by logging in as the standard user `dammycys`, navigating to the path, and successfully creating a log file:
```bash
cd /opt/tech_file
touch file_logs.txt
ls -l
```
* **Output:** `-rw-r--r-- 1 dammycys dammycys 0 Nov 1 09:52 file_logs.txt`

![Terminal showing Multi-User File Creation Test](https://github.com/DammyCys/Linux-File-Permissions-Lab/blob/main/Screenshot%20(7)_065432.png)


## Practical Troubleshooting Lessons Learned
- **The `sudo cd` Rule:** Learned that you cannot run `sudo cd` because `cd` is a shell built-in command, not an external application.
- **WSL User Switching:** Practiced managing local credentials and troubleshooting profile authentications using `su - Dammy-Test` and `sudo passwd`.
