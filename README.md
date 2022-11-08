# Archiving-and-Logging-Data
Expanded a Log Management System  
You will play the role of a security analyst at Credico Inc., a financial institution that offers checking, savings, and investment banking services.  
In an effort to mitigate network attacks and meet federal compliance, Credico Inc. developed an efficient log management program that performs:  
* Log size management using logrotate.  
* Log auditing with auditd to track events, record the events, detect abuse or unauthorized activity, and create custom reports. 

You will expand and enhance this log management system by learning new tools, adding advanced features, and researching additional concepts.  

**Step 1: Create, Extract, Compress, and Manage tar Backup Archives**  
Creating tar archives is something you must do every day in your role at Credico Inc. In this section, you will extract and exclude specific files and directories to help speed up your workflow.  

1. Command to extract the TarDocs.tar archive to the current directory:  
Answer:  
sudo tar xvvf Tardocs.tar  

<img width="337" alt="11-a" src="https://user-images.githubusercontent.com/106919343/200645519-97efd256-5f0e-4396-ad2e-57f3bb644fe3.png">  

<img width="416" alt="12-b" src="https://user-images.githubusercontent.com/106919343/200645536-46348124-0531-4f1a-8294-02c95dac1977.png">

2. Command to create the Javaless_Doc.tar archive from the TarDocs/ directory, while excluding the TarDocs/Documents/Java directory:  

Answer:  
tar cvvf Javaless_Docs.tar -–exclude=“TarDocs/Documents/Java” TarDocs/Documents/  
<img width="599" alt="12experiment" src="https://user-images.githubusercontent.com/106919343/200645898-9e96f65e-0770-498f-b22f-dcf96869b32b.png">  

3. Command to ensure Java/ is not in the new Javaless_Docs.tar archive:  

Answer:
tar tvvf Javaless_Docs.tar | grep Java  
<img width="415" alt="13experiment" src="https://user-images.githubusercontent.com/106919343/200646102-a848566c-a651-4dad-9824-a1377990fb9d.png">  

**Step 2: Create, Manage, and Automate Cron Jobs**  
In response to a ransomware attack, you have been tasked with creating an archiving and backup scheme to mitigate against CryptoLocker malware. This attack would encrypt the entire server’s hard disk and can only be unlocked using a 256-bit digital key after a Bitcoin payment is delivered.  

1. Cron job for backing up the /var/log/auth.log file:  

Answer:  
Creating the cron job  
Crontab -e

Cron job:
0 6 * * 3 tar czvf /auth_backup.tgz /var/log/auth.log  
<img width="629" alt="21" src="https://user-images.githubusercontent.com/106919343/200646628-b45fb665-4a28-4a12-823f-5535f2ccef45.png">  

<img width="709" alt="21-a" src="https://user-images.githubusercontent.com/106919343/200646677-bd9c1f6c-1a09-4dcc-a141-96394a30758d.png">  

**Step 3: Write Basic Bash Scripts**  
Portions of the Gramm-Leach-Bliley Act require organizations to maintain a regular backup regimen for the safe and secure storage of financial data.  

You'll first need to set up multiple backup directories. Each directory will be dedicated to housing text files that you will create with different kinds of system information.  

1. Using brace expansion, create the following four directories:  

~/backups/freemem  
~/backups/diskuse  
~/backups/openlist  
~/backups/freedisk  

Answer:  
mkdir -p ~/backups/{freemem,diskuse,openlist,freedisk}  
<img width="736" alt="31" src="https://user-images.githubusercontent.com/106919343/200647181-957dc5bd-ac7c-458a-95c0-64f65705eaee.png">  

Now, you will create a script that will execute various Linux tools to parse information about the system. Each of these tools should output results to a text file inside its respective system information directory.  

2. Edit the system.sh script file so that it that does the following:  

* Prints the amount of free memory on the system and saves it to ~/backups/freemem/free_mem.txt.  
* Prints disk usage and saves it to ~/backups/diskuse/disk_usage.txt.  
* Lists all open files and saves it to ~/backups/openlist/open_list.txt.  
* Prints file system disk space statistics and saves it to ~/backups/freedisk/free_disk.txt.

Answer:  
#!/bin/bash  
free -h > ~/backups/freemem/free_mem.txt  
du -hs ~ > ~/backups/diskuse/disk_use.txt  
lsof > ~/backups/openlist/open_list.txt  
df -h > ~/backups/freedisk/free_disk.txt  
<img width="659" alt="32" src="https://user-images.githubusercontent.com/106919343/200647811-572bc0a9-ac0d-481d-ba03-f0f7d3be46b4.png">  

3. Command to make the system.sh script executable:  
Answer:  

chmod +x system.sh  

<img width="360" alt="33" src="https://user-images.githubusercontent.com/106919343/200647950-452745be-0bd4-4c8c-976c-4e9c71bbf048.png">  

<img width="332" alt="33a" src="https://user-images.githubusercontent.com/106919343/200647988-a08cc748-d0a1-42cc-a3b5-9c08a7f042bd.png">  

Commands to test the script and confirm its execution:  

Answer:  
./system.sh  
<img width="476" alt="34a" src="https://user-images.githubusercontent.com/106919343/200648133-95844243-0232-478d-9d60-25befe4e830e.png">  
<img width="471" alt="4b" src="https://user-images.githubusercontent.com/106919343/200648399-974b87ca-b33c-45dd-b31f-053cfad61c6b.png">  

**Step 4. Manage Log File Sizes**  

You realize that the spam messages are making the size of the log files unmanageable.  

You’ve decided to implement log rotation in order to preserve log entries and keep log file sizes more manageable. You’ve also chosen to compress logs during rotation to preserve disk space and lower costs.  

1. Run sudo nano /etc/logrotate.conf to edit the logrotate configuration file.  

Configure a log rotation scheme that backs up authentication messages to the /var/log/auth.log. 

  a. Add your config file edits:  
  
  Answer:  
  /var/log/auth.log {  
      Weekly  
      Rotate 7  
      Not if empty  
      Compress  
      Delaycompress  
      Missingok  
      Endscript  
   }  
   <img width="732" alt="41" src="https://user-images.githubusercontent.com/106919343/200648957-16e61189-8025-4e33-a421-ad66ebd46ed1.png">  
   
**Bonus: Check for Policy and File Violations**  
In an effort to help mitigate against future attacks, you have decided to create an event monitoring system that specifically generates reports whenever new accounts are created or modified, and when any modifications are made to authorization logs.  

1. Command to verify `auditd` is active:  
Answer:  
sudo systemctl status auditd  
<img width="450" alt="bonus1" src="https://user-images.githubusercontent.com/106919343/200649538-f900c28a-f0ae-43bf-b392-c6066c3e29ab.png">  

2. Command to set number of retained logs and maximum log file size:  
Answer:  
sudo nano /etc/audit/auditd.conf  
<img width="473" alt="bonus2" src="https://user-images.githubusercontent.com/106919343/200649646-4ec0597f-8c0f-4bf7-9b49-b8f6c1926f59.png">  

  a. Add the edits made to the configuration file:  
  Answer:  
    sudo systemctl restart auditd  
    <img width="340" alt="bonus21" src="https://user-images.githubusercontent.com/106919343/200649839-36c5062a-3f62-4684-a748-d5fa26af5025.png">  

3. Command using auditd to set rules for /etc/shadow, /etc/passwd, and /var/log/auth.log:  
Answer:  
sudo nano /etc/audit/rules.d/audit.rules  

  a. Add the edits made to the rules file below:  
    <img width="619" alt="bonus3" src="https://user-images.githubusercontent.com/106919343/200650027-b4e6e950-1cc3-4dac-bbc6-4b7e7d2afc0f.png">  
    
4. Command to restart auditd:  
Answer:  
sudo systemctl restart auditd  

5. Command to list all auditd rules:  
Answer:  
sudo auditctl -l  
<img width="629" alt="bonus5" src="https://user-images.githubusercontent.com/106919343/200650231-366e00e7-0327-4533-b3b8-c8f9052d75a7.png">  

6. Command to produce an audit report:  
Answer:  
sudo aureport 
<img width="590" alt="bonus6" src="https://user-images.githubusercontent.com/106919343/200650363-be67edc6-7a9b-4cc8-af3f-f6084a902ef7.png">  

7. Create a user with sudo useradd attacker and produce an audit report that lists account modifications:  
Answer:  
sudo aureport -m  
<img width="776" alt="bonus7" src="https://user-images.githubusercontent.com/106919343/200650503-b5935608-c7e1-44da-8814-326aad60569a.png">  
<img width="792" alt="bonus7a" src="https://user-images.githubusercontent.com/106919343/200650532-14717640-89da-4e8f-b4a7-ddc978c81a61.png">  

8. Command to use auditd to watch /var/log/cron:  
Answer:  
sudo auditctl -w /var/log/cron  
<img width="379" alt="bonus8" src="https://user-images.githubusercontent.com/106919343/200650572-e9049d7f-38af-4a8b-8787-7fc77835aa3b.png">  

9. Command to verify auditd rules:  
Answer:  
sudo auditctl -l  
<img width="408" alt="bonus9" src="https://user-images.githubusercontent.com/106919343/200650699-9efa4c8a-ebbe-491d-94f3-4b261f3c5715.png">




