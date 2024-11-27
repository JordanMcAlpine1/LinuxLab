# LinuxLab

## Description  

This project involves performing a series of investigative tasks, including password recovery, user account penetration, log file analysis, file permission auditing, debugging scripts, inspecting custom aliases, exploiting vulnerabilities for root access, and password cracking to gather and decode all flags.  

## Operating System  

- **Linux**  

---

## Finding Flag 1  
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



## Finding Flag 2  
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



## Finding Flag 3  
- Flag 3 Indicator: Find a log file related to the hacker's name and a zip file with additional info.

### Steps/Commands to Locate and Retrieve Flag 3

##### 1. Navigate to the mitnick user's home directory
cd /home/mitnick

##### 2. List all files and directories, including hidden ones
ls -Ra

##### 3. Identify the .secret.zip file in the Documents directory
ls ~/Documents

##### 4. View the log file in /var/log directory
ls /var/log

##### 5. Count the number of unique IP addresses in the mitnick.log file
cat /var/log/mitnick.log | sort | uniq | wc -l

##### 6. Use the count (102) as the password to unzip the secret.zip file
unzip ~/Documents/.secret.zip

##### 7. Inspect the contents of the unzipped file, which is named "babbage"
ls

##### 8. Read the contents of the "babbage" file to find the password for the babbage user
nano babbage


![Screenshot 2024-10-31 at 8 39 27 PM](https://github.com/user-attachments/assets/06cef98f-3301-429b-aaa9-bb08e8a05599)


##### 9. Log in as the babbage user to find flag_3
su babbage
##### Enter the password: freedom

##### 10. Retrieve the flag after successfully logging in as babbage


![Screenshot 2024-10-31 at 8 44 39 PM](https://github.com/user-attachments/assets/53b27e21-bd67-4ebc-a94b-ecbf25006b5e)



## Finding Flag 4  
- Flag 4 Indicator: Find a directory with a list of hackers. Look for a file that has read permissions for the owner, no permissions for groups, and executable only for everyone else.

### Steps/Commands to Locate and Retrieve Flag 4

##### 1. Navigate to the babbage user's home directory
cd /home/babbage/

##### 2. List all files and directories, including hidden ones
ls -Ra

##### 3. Switch to the Documents directory where hacker files are stored
cd Documents

##### 4. List the permissions of all files in the Documents directory
ls -l

##### 5. Filter the files with read permissions for the owner, no permissions for groups, and executable only for everyone else
ls -l | grep "^\-r\-\-\-\-\-\-\-x"

##### 6. Inspect the contents of the "stallman" file (the one with content)
cat stallman

##### 7. Retrieve the password for the stallman user
##### The password is "computer"

##### 8. Log in as the stallman user to find flag_4
su stallman
##### Enter the password: computer

##### 9. Retrieve the flag after successfully logging in as stallman


![Screenshot 2024-10-31 at 8 48 20 PM](https://github.com/user-attachments/assets/87873da2-6bee-4c39-978d-b3fce25127bf)



## Finding Flag 5  
- Flag 5 Indicator: This user is writing a Bash script, except it isn't quite working yet. Find it, debug it, and run it.

### Steps/Commands to Locate and Retrieve Flag 5

##### 1. Navigate to the stallman user's home directory
cd

##### 2. List all files and directories, including hidden ones
ls -Ra

##### 3. Go to the Documents directory where the script is located
cd Documents/

##### 4. Make the script executable
chmod +x flag5.sh

##### 5. Run the script to check for syntax errors
./flag5.sh

##### 6. Inspect the first few lines of the script to find the error
head -6 flag5.sh

##### 7. Edit the script to remove the extra "do" on line 4
##### In the script, remove one of the "do"s, then save and exit

##### 8. Run the script again to check for the next error
./flag5.sh

##### 9. Inspect the error message and notice the missing "then" in the if statement
# Add the missing "then" after "if [ ${#file} -gt $width ]"

##### 10. Run the script again
./flag5.sh

##### 11. The script will now execute correctly and display the flag:


![Screenshot 2024-10-31 at 8 54 49 PM](https://github.com/user-attachments/assets/d8bc1a79-640f-434f-82a8-222e43d24c95)
