# LinuxLab

## Description  

This project involves performing a series of investigative tasks, including password recovery, user account penetration, log file analysis, file permission auditing, debugging scripts, inspecting custom aliases, exploiting vulnerabilities for root access, and password cracking to gather and decode all flags.  

## Operating System  

- **Linux**  

---

## Objective 1: Find Flag 1  
- Flag 1 Indicator: Finding this flag is imperative to moving on quickly, as it contains the passwords from users before they are hacked. Luckily, it doesn't have a great hiding spot.

### Steps/Commands to Locate and Retrieve Flag 1  

##### 1. List all files and directories, including hidden ones
ls -Ra

##### 2. Navigate to the desktop directory
cd ~/Desktop/

##### 3. View all files (including hidden files)
ls -a

##### 4. Access the flag (read the contents of .flag_1)
nano .flag_1

  
![Screenshot 2024-10-31 at 8 16 27 PM](https://github.com/user-attachments/assets/3a31164e-32c3-46c6-b9a5-4db7aa7559f9)



## Objective 2: Find Flag 2  
- Flag 2 Indicator: A famous hacker had created a user on the system a year ago. Find this user, crack his password, and login to his account.

### Steps/Commands to Locate and Retrieve Flag 2  

##### 1. Navigate to the desktop directory
cd ~/Desktop/

##### 2. Crack the password hashes with John the Ripper
john --wordlist=.pass_list.txt ../Documents/my-files/shadow

##### 3. Show the cracked passwords
john --show ../Documents/my-files/shadow

##### 4. Switch to the user account 'mitnick'
su mitnick

##### 5. Retrieve the flag after logging in
##### (The flag will be displayed once logged in as 'mitnick')


![Screenshot 2024-10-31 at 8 20 08 PM](https://github.com/user-attachments/assets/6cf41d10-4099-424e-a73d-c93ebd449cc8)

