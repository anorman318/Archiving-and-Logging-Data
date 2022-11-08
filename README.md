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




