# Cyber Security 101

## Start Your Cyber Security Journey
### Offensive Security Intro
- [[1_Pre_Security]] - for more detailed info
- Offensive Security involves breaking into computer systems, exploiting software bugs, and finding loopholes in applications to gain unauthorized access.
- The goal is to understand hacker tactics and enhance our system defenses. 
- To find hidden URLs, we use a tool called **dirb**. [[Linux_Commands]] This tool uses  a brute-force approach, by taking a list of potential names and testing one by one if they exist in your website.
### Defensive Security Intro
- [[1_Pre_Security]] - for more detailed info

### Search Skills
- Evaluation of Search Results - A few things to consider when evaluating information:
	- Source: Identify the author or organization publishing the informaiton.
	- Evidence and reasoning: Check whether the claims are backed by credible evidence and logical reasoning.
	- Objectivity and bias: Evaluate whether the information is presented impartially and rationally, reflecting multiple perspectives. 
	- Corroboration and consistency: Validate the presented information by corroboration from multiple independent sources.
- Almost every Internet search engine allows you to carry out advanced searches. https://github.com/cipher387/Advanced-search-operators-list
- Shodan (https://www.shodan.io/) - a search engine for devices connected to the Internet. It allows you to search for specific types and versions of servers, networking equipment, industrial systems, and IoT devices. 
- Censys (https://search.censys.io/) appears similar to Shodan. However, Shodan focuses on Internet-connected devices and systems, such as servers, routers, webcams, and IoT devices. Censys, on the other hand, focuses on Internet-connected hosts, websites, certificates, and other Internet assets. Some of its use cases include enumerating domains in use, auditing open ports and services, and discovering rogue assets within a network.
- VirusTotal (https://www.virustotal.com/) is an online website that provides a virus-scanning service for files using multiple antivirus engines. It allows users to upload files or provide URLs to scan them against numerous antivirus engines and website scanners in a single operation. They can even input file hashes to check the results of previously uploaded files. 
- Have I Been Pwned (https://haveibeenpwned.com/) does one thing; it tells you if an email address appeared in a leaked data breach. Finding one's email withing leaked data indicates leaked private information, and more importantly, passwords.
- Common Vulnerabilities and Exposures (CVE) program (https://www.cve.org/)is a directory of vulnerabilities. It provides a standardized identifier for vulnerabilities and security issues in software and hardware products.
	- Each vulnerability is assigned a CVE ID with a standardized format like **CVE-2024-299888**. 
	- The MITRE Corporation maintains the CVE system.
	- There is also the National Vulnerability Database (NVD, https://nvd.nist.gov/), which also provides the CVSS & CWE.
- The Exploit Database (https://www.exploit-db.com/) lists exploit codes from various authors; some of these codes are tested and marked as verified. 
- Linux Manual Pages
	- On Linux and every Unix-like system, each command is expected to have a man page. For example checking the manual page for the command **ip**, would be **man ip**.
- Microsoft Windows
	- Microsoft provides and official Technical Documentation (https://learn.microsoft.com/) page for its products.  


### Linux Fundamentals
- [[1_Pre_Security]] - for more detailed information #linux
## Linux Fundamentals
- [[1_Pre_Security]] - for more detailed information #linux
## Windows and AD Fundamentals
- [[1_Pre_Security]]  - for Windows Fundamentals
### Active Directory Basics
- Microsoft's Active Directory is the backbone of the corporate world. It simplifies the management of devices and users within a corporate environment. 
- A **Windows Domain** is a group of users and computers under the administration of a given business. The main idea behind a domain is to centralize the administration of common components of a Windows computer network in a single repository called **Active Directory (AD)**. The server that runs the Active Directory services is known as a **Domain Controller (DC)**. 
![[Pasted image 20260216080326.png]]
- The main advantages of having a configured Windows domain are:
	- Centralized identity management: All users across the network can be configured from Active Directory with minimum effort. 
	- Managing security policies: You can configure security policies directly from Active Directory and apply them to users and computers across the network as needed. 
- The core of any Windows Domain is the **Active Directory Domain Service (AD DS)**. This service acts as a catalogue that holds the information of all of the "objects" that exist on your network. 
- *Users* are one of the most common object types in Active Directory. Users are on of the objects known as **security principals**, meaning that they can be authenticated by the domain and can be assigned privileges over resources like files or printers. 
	- Users can be used to represent two types of entities:
		1. **People**: users will generally represent persons in your organization that need to access the network, like employees.
		2. **Services:** you can also define users to be used by services like IIS or MSSQL. Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service.
- *Machines* are another type of object within Active Directory; for every computer that joins the Active Directory domain, a machine object will be created. Machines are also considered "security principals" and are assigned an account just as any regular user. The machine accounts themselves are local administrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in.
	- Identifying machine accounts is relatively easy. They follow a specific naming scheme. Teh machine account name is the computer's name followed by a dollar sign. For example, a machine named **DC01** will have a machine account called **DC01$**.
- *Security Groups* are also considered security principals and, therefore, can have privileges over resources on the network. Groups can have both users and machines as members. Several groups are created by default in a domain that can be used to grant specific privileges to users. Below are some of the most important groups in a domain:

| Security Group     | Description                                                                                                                                               |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Domain Admins      | Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs. |
| Server Operators   | Users in this group can administer Domain Controllers. They cannot change any administrative group membershps.                                            |
| Backup Operators   | Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers.                    |
| Account Operators  | Users in this group can create or modify other accounts in the domain.                                                                                    |
| Domain Users       | Includes all existing user accounts in the domain.                                                                                                        |
| Domain Computers   | Incudes all existing computers in the domain.                                                                                                             |
| Domain Controllers | Includes all existing DCs on the domain.                                                                                                                  |
- To configure users, groups, or machines in Active Directory, we need to log in to the Domain Controller and run "Active Directory Users and Computers" from the start menu:
![[Pasted image 20260216082043.png]]
- Security Groups vs Organizational Units (OUs)
	- OUs are handy for applying policies to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise. Remember, a user can only be a member of a single OU at a time, as it wouldn't make sense to try to apply two different sets of policies to a single user. 
	- Security Groups, on the other hand, are used to grant permissions over resources. For example, you will use groups if you want to allow some users to access a shared folder or network printer. A user can be part of many groups, which is needed to grant access to multiple resources. 
- [[AD PowerShell Scripts]]
- Managing Computers in AD
	1. Workstations
		1. Workstations are one of the most common devices within an AD domain. Each user in the domain will likely be logged into a workstation. 
	2. Servers
		1. Servers are the second most common device within an AD domain. Servers are generally used to provide services to users or other servers.
	3. Domain Controllers
		1. Domain Controllers are the third most common device within an Active Directory domain. Domain Controllers allow you to manage the Active Directory Domain.
- Group Policy Objects (GPOs) are simply a collection of setting that can be applied to OUs. GPOs can contain policies aimed at either users or computers, allowing you to set a baseline on specific machines and identities.
- To configure GPOs, you can use the Group Policy Management tool, available from the start menu:
![[Pasted image 20260216083545.png]]
- GPOs are distributed to the network via a network share called **SYSVOL**, which is stored in the DC. All users in a domain should typically have access to this share over the network to sync their GPOs periodically. The SYSVOL share points by default to the **C:\Windows\SYSVOL\sysvol\\** directory on each of the DCs in our network. 
- When using Windows domains, all credentials are stored in the Domain Controllers. Two protocols can be used for network authentication in Windows domains:
	- **Kerberos:** Used by any recent version of Windows. This is the default protocol in any recent domain.
	- **NetNTLM:** Legacy authentication protocol kept for compatibility purposes. 
- When Kerberos is used for authentication, the following process happens:
	- 1. The user sends their username and a timestamp encrypted using a key derived from their password to the **Key Distribution Center (KDC)**, a service usually installed on the Domain Controller in charge of creating Kerberos tickets on the network.
    
    - The KDC will create and send back a **Ticket Granting Ticket (TGT)**, which will allow the user to request additional tickets to access specific services. The need for a ticket to get more tickets may sound a bit weird, but it allows users to request service tickets without passing their credentials every time they want to connect to a service. Along with the TGT, a **Session Key** is given to the user, which they will need to generate the following requests.
    
    - Notice the TGT is encrypted using the **krbtgt** account's password hash, and therefore the user can't access its contents. It is essential to know that the encrypted TGT includes a copy of the Session Key as part of its contents, and the KDC has no need to store the Session Key as it can recover a copy by decrypting the TGT if needed.
	![[Pasted image 20260216084345.png]]
	- When a user wants to connect to a service on the network like a share, website or database, they will use their TGT to ask the KDC for a **Ticket Granting Service (TGS)**. TGS are tickets that allow connection only to the specific service they were created for. To request a TGS, the user will send their username and a timestamp encrypted using the Session Key, along with the TGT and a **Service Principal Name (SPN),** which indicates the service and server name we intend to access.
    
    - As a result, the KDC will send us a TGS along with a **Service Session Key**, which we will need to authenticate to the service we want to access. The TGS is encrypted using a key derived from the **Service Owner Hash**. The Service Owner is the user or machine account that the service runs under. The TGS contains a copy of the Service Session Key on its encrypted contents so that the Service Owner can access it by decrypting the TGS.
![[Pasted image 20260216084549.png]]
    - The TGS can then be sent to the desired service to authenticate and establish a connection. The service will use its configured account's password hash to decrypt the TGS and validate the Service Session Key.
![[Pasted image 20260216084604.png]]
- NetNTLM works using a challenge-response mechanism:
![[Pasted image 20260216084649.png]]
	1. The client sends an authentication request to the server they want to access.
	2. The server generates a random number and sends it as a challenge to the client.
	3. The client combines their NTLM password has with the challenge (and other known data) to generate a response to the challenge and sends it back to the server for verification.
	4. The server forwards the challenge and the response to the Domain Controller for verification.
	5. The Domain Controller uses the challenge to recalculate the response and compares it to the original response sent by the client. If they both match, the client is authenticated; otherwise, access is denied. The authentication result is sent back to the server.
	6. The server forwards the authentication result to the client. 
- AD supports integrating multiple domains so that you can partition your network into units that can be managed independently. If you have two domains that share the same namespace (thm.local in our example), those domains can be joined into a single **Tree**. 
![[Pasted image 20260216085344.png]]
- The union of several trees with different namespace into the same network is known as a **forest**. 
![[Pasted image 20260216085438.png]]
- **Trust relationships** - In simple terms, having a trust relationship between domains allows you to authorize a user from domain **THM UK** to access resources from domain **MHT EU**. 
- The simplest trust relationship that can be established is a **one-way trust relationship**. In a one-way trust, if **Domain AAA** trusts **Domain BBB**, this means that a user on BBB can be authorized to access resources on AAA:
![[Pasted image 20260216085930.png]]
- **Two-way trust relationships** can also be made to allow both domains to mutually authorize users from the other. By default, joining several domains under a tree or a forest will form a two-way trust relationship.

## Command Line
### Windows Command Line
- Everyone prefers a graphical user interface (GUI) until they master a command-line interface (CLI). 
- There are many advantages to using a CLI besides speed and efficiency:
	- **Lower resource usage:** CLIs require fewer system resources than graphics-intensive GUIs. In other words, you can run your CLI system on older hardware or systems with limited memory. 
	- **Automation:** While you can automate GUI tasks, creating a batch file or script with the commands you need to repeat is much easier.
	- **Remote Management:** CLI makes it very convenient to use SSH to manage a remote system such as a server, router, or an IoT device. This approach works well on slow network speeds and systems with limited resources.
- Before issuing commands, we should note that we can only issue the commands within the Windows Path. You can issue the command **set** to check your path from the command line. [[Windows_Commands]].
- **ver** command - shows the operating system (OS) version.
- **systeminfo** command - list various information about the system such as OS information, system details, processor, and memory. 
- You can pipe a command through **more** if the output is too long. Then, you can view it page after page by pressing the space bar button. For example running **driverquery** and compare it to running **driverquery | more**. In the latter, you can display the output page by page and can exit it using CTRL + C.
- **help** - provides help information for a specific command
- **cls** - Clears the Command Prompt screen.
- **ipconfig** - utilized to check your network connection.
- **ipconfig /all** - view more information about your network configuration. 
- Network Troubleshooting:
	- **ping \[insert target_name]** - sends a specific ICMP packet and listens for a response. If a response is received, we know that we can reach the target and that the target can reach us.
	- **tracert** command - The command **tracert \[insert target_name]** traces the network route traversed to reach the target.
- More Networking Commands:
	- **nslookup**  - The nslookup command looks up a host or domain and returns its IP address. The syntax **nslookup \[insert target_name]** will look up the target_name using the default name server.
	- **netstat** - This command displays current network connections and listening ports. A basic **netstat** command with no arguments will show you established connections.
- **cd** - You can use **cd** without parameters to display the current drive and directory. It is the equivalent of asking the system, *where am I?*
- You can view the child directories using **dir**
	- **dir /a** - Displays hidden and system files as well.
	- **dir /s** - Displays files in the current directory and all subdirectories.
- You can type **tree** to visually represent the child directories and subdirectories.
- **cd ..** to go up one level
- **mkdir \[insert directory_name]** - **mkdir** stands for *make directory*.
- **rmdir \[insert directory_name]** - **rmdir** stands for *remove directory*.
- **type** command - to easily view text files
- **more** command - for longer text files, will display enough text file contents to fill your terminal window. Utilize **Spacebar** to move by one page or **Enter** to move by one line.
- **copy** command - allows you to copy files from one location to another. 
- **move** command - allows you to move files.
- **del** or **erase** commands - delete a file
- **tasklist** command - list the running processes. Can check all available filters by displaying the help page using **task /?**.
- With the process ID (PID) known, we can terminate any task using **taskkill /PID \[insert target_pid]**. 
### Windows PowerShell
- *PowerShell is a cross-platform task automation solution made up of a command-line shell, a scripting language, and a configuration management framework.*
- PowerShell is a powerful tool from Microsoft designed for task automation and configuration management. It combines a command-line interface and a scripting language built on the .NET framework. 
- PowerShell was developed to overcome the limitations of existing command-line tools and scripting environments in Windows.
- To fully grasp the power of PowerShell, we first need understand what an **object** is in this context.
- In programming, an **object** represents an item with **properties** (characteristics) and **methods** (actions). 
- An object in PowerShell can contain file names, usernames or sizes as data (**properties**), and carry functions (**methods**) such as copying a file or stopping a process.
- PowerShell can be launched from a Command Prompt (cmd.exe) by typing **powershell**, and pressing **Enter**. 
- PowerShell commands are known as **cmdlets**. They are much more powerful than the traditional Windows commands and allow for more advanced data manipulation. [[PowerShell cmdlets]]
- Cmdlets follow a consistent **Verb-Noun** naming convention. This structure makes it easy to understand what each cmdlet does. The **Verb** describes the action, and the **Noun** specifies the object on which action is performed. 
- **Get-Command** - lists all available cmdlets, functions, aliases, and scripts that can be executed in the current PowerShell session.
- If we want to display only the available commands of type "function", we can use **-CommandType "Function"**. 
- Another essential cmdlet to keep in our tool belt is **Get-Help**: it provides detailed information about cmdlets, including usage, parameters, and examples. 
![[Pasted image 20260216110142.png]]
- **Get-Alias** lists all aliases available.
![[Pasted image 20260216110219.png]]
- To search for modules (collections of cmdlets) in online repositories like the PowerShell Gallery, we can use **Find-Module**. 
- Once identified, the modules can be downloaded and installed from the repository with **Install-Module**, making new cmdlets contained in the module available for use. 
- Similar to **dir** command in Command Prompt, **Get-ChildItem** lists the files and directories in a location specified with the **-Path** parameter. If no **Path** is specified, the cmdlet will display the content of the current working directory.
- To navigate to a different directory, we can use the **Set-Location** cmdlet. It changes the current directory, bringing up to the specified path, akin to the **cd** command in Command Prompt.
![[Pasted image 20260216111050.png]]
- To create an item in PowerShell, we can use **New-Item**. We will need to specify the path of the item and its type (whether it is a file or a directory). 
![[Pasted image 20260216111217.png]]
- Similarly, the **Remove-Item** cmdlet removes both directories and files. Can also copy or move files using **Copy-Item** and **Move-Item**. 
- To read and display the contents of a file, we can use the **Get-Content** cmdlet, which works similarly to the **type** command in Command Prompt (or **cat** in Unix-like systems). 
- Piping is a technique used in command-line environments that allows the output of one command to be used as the input or another. This creates a sequence of operations where the data flows from one command to the next. Represented by the **|** symbol, piping is widely used in the Windows CLI. 
![[Pasted image 20260216111717.png]]
- **Get-ComputerInfo** cmdlet retrieves comprehensive system information, including operating system information, hardware specifications, BIOS details, and more. 
- **Get-LocalUser** lists all the local user accounts on the system. 
- **Get-NetIPConfiguration** provides detailed information about the network interfaces on the system, including IP addresses, DNS servers, and gateway configuration.
- **Get-Process** provides a detailed view of all currently running processes, including CPU and memory usage, making it a powerful tool for monitoring and troubleshooting.
- **Get-Service** allows the retrieval of information about the status of services on the machine, such as which services are running, stopped, or paused. 
- **Get-NetTCPConnection** displays current TCP connections, giving insights into both local and remote endpoints. 
- **Get-FileHash** is a useful cmdlet for generating file hashes. 
- **Invoke-Command** is essential for executing commands on remote systems, making it fundamental for system administrators, security engineers, and penetration testers. 
### Linux Shells
- When interacting with a shell, you must be in the directory where you want to perform operations. By default when you open a shell in most of the Linux distributions, you will be in your home directory. To see your current working directory, you can execute **pwd**, which stand for Print Working Directory.
- The **grep** command is a very popular command among Linux users. This powerful command can search for any word or pattern inside a file. Suppose you want to search for a specific entries in a huge file. You can use the grep command along with the pattern of those entries, which will extract them for you. 
![[Pasted image 20260216113155.png]]
- Multiple shells are installed in different Linux distributions. To see which shell you are using, type the following command: **echo $SHELL**
- You can also list down the available shells in your Linus OS. The file **/etc/shells/** contains all the installed shells on a Linux system.
- If you want to permanently change your default shell, you can use the command: **chsh -s /usr/bin/zsh**
- Bourne Again Shell (Bash) is the default shell for most Linux distributions. When you open the terminal, bash is present for you to enter commands. 
- Some of the key features provided by bash are listed below:
	- Bash is a widely used shell with scripting capabilities.
	- It offers a tab completion feature, which means if you are in the middle of completing a command, you can press the tab key on your keyboard. It will automatically complete the command based on a possible match or give you multiple suggestions for completing it.
	- Bash keeps a history file and logs all of your commands. You can use the up and down arrow keys to use the previous commands without tying them again. You can also type **history** to display all your previous commands. 
- Friendly Interactive Shell (Fish) is not default in most Linux distributions. As its name suggests, it focuses more on user-friendliness than other shells. Some of the key features provided by fish are listed below:
	- It offers a very simple syntax, which is feasible for beginner users.
	- Unlike bash, it has auto spell correction for the commands you write.
	- You can customize the command prompt with some cool themes using fish.
	- The syntax highlighting feature of fish colors different part of a command based on their roles, which can improve the readability of commands. It also helps us to spot errors with their unique colors.
	- Fish also provides scripting, tab completion, and command history functionality like the shells mentioned int his task.
- Z Shell (Zsh) is not installed by default in most Linux distributions. It is considered a modern shell that combines the functionalities of some previous shells. Some of the key features provided by zsh are listed below:
	- Zsh provides advanced tab completion and is also capable of writing scripts.
	- Just like fish, it also provides auto spell correction for the commands.
	- It offers extensive customization that may make it slower than other shells.
	- It also provides tab completion, command history functionality, and several other features.
- A shell script is nothing but a set of commands. Suppose a repetitive task requires you to enter multiple commands using a shell. Instead of entering them one after one on every repetition of that task, which may take more of your time, you can combine them into a script. 
- The file must be named with an extension **.sh**, the default extension for bash scripts. 
- Every script should start from shebang. Shebang is a combination of some characters that are added at the beginning of a script, starting with **#!** followed by the name of the interpreter to use while executing the script. 
![[Pasted image 20260216114847.png]]
- Loop, as the name suggests, is something that is repeating. For example, you have a list of many friends, and you want to send them the same message. Instead of sending them individually, you can make a loop in your script , give your fiend list to the loop and the message, and it will send that message to all of your friends. 
![[Pasted image 20260216115110.png]]
- Conditional statements are an essential part of scripting. They help you execute a specific code only when a condition is satisfied; otherwise, you can execute another code. 
![[Pasted image 20260216115207.png]]
- **Comments** - Sometimes the code can be very lengthy. In this scenario, the code might confuse you when you look at it after some time or share it with somebody. An easy way to resolve this problem is to use comments in different parts of the code. A comment is a sentence that we write in our code just for the sake of understanding. It is written with a **#** sign followed by a space and the sentence you need to write. 
![[Pasted image 20260216115417.png]]
## Networking
### Networking Core Protocols
- Domain Name System (DNS), is responsible for properly mapping a domain name to an IP address. DNS operates at the Application Layer (Layer 7 of the ISO OSI model). 
- DNS traffic uses UDP port 53 by default and TCP port 53 as a default fall back. [[Ports]]
- **A record:** The A (Address) record maps a hostname to one or more IPv4 addresses. For example, you can set *example.com* to resolve to *172.17.2.172*. 
- **AAAA Record:** The AAAA record is similar to the A Record, but it is for IPv6. Remember that it is AAAA (quad-A), as AA and AAA would refer to a battery size; furthermore, AAA refers to *Authenitcation, Authorization, and Accounting;* neither falls under DNS.
- **CNAME Record:** The CNAME (Canonical Name) record maps a domain name to another domain name. For example, *www.example.org* can be mapped to *example.com* or even to *example.org*. 
- **MX Record:** The MX (Mail Exchange) record specified the mail server responsible for handling emails for a domain. 
- If you want to look up the IP address of a domain from the command line, you can use a tool such as **nslookup**. 
![[Pasted image 20260216142231.png]]
- You can look up the WHOIS records of any registered domain name using one of the online services or via the command-line tool **whois**, available on Linux systems, among others. As expected a WHOIS record provides information about the entity that registered a domain name, including name, phone number, email, and address. 
- Some of the commands or methods that your web browser commonly issues to the web server are:
	- **GET** retrieves data from a server, such as an HTML file or an image.
	- **POST** allows us to submit new data to the server, such as submitting a form or uploading a file.
	- **PUT** is used to create a new resource on the server and to update and overwrite existing information.
	- **Delete**, as the name suggests, is used to delete a specified file or resource on the server. 
- Unlike HTTP, which is designed to retrieve web pages, File Transfer Protocol (FTP) is designed to transfer files.
- Example commands defined by the FTP protocol are:
	- **User** is used to input the username.
	- **PASS** is used to enter the password.
	- **RETR** (retrieve) is used to download a file from the FTP server to the client.
	- **STOR** (store) is used to upload a file from the client to the FTP server.
- FTP server listens on TCP port 21 by default; data transfer is conducted via another connection from the client to the server.
- Simple Mail Transfer Protocol (SMTP) defines how mail client talks with a mail server and how a mail server talks with another.
- Some of the commands used by your mail client when it transfers an email to an SMTP server:
	- **HELO** or **EHLO** initiates an SMTP session
	- **MAIL FROM** specifies the sender's email address
	- **RCPT TO** specifies the recipient's email address
	- **DATA** indicates that the client will begin sending the content of the email message
	- **.** is sent on a line by itself to indicate the end of the email message
- The Post Office Protocol version 3 (POP3) is designed to allow the client to communicate with a mail server and retrieve email messages. Without going into in-depth technical details, an email client sends its messages by relying on SMTP and retrieves them using POP3.
- Some common POP3 commands are:
	- **USER \<username>** identifies the user
	- **PASS \<password>** provides the user's password
	- **STAT** requests the number of messages and total size
	- **LIST** lists all messages and their sizes
	- **RETR \<message_number>** retrieves the specified message
	- **DELE \<message_number>** marks a message for deletion
	- **QUIT** ends the POP3 session applying changes, such as deletions
- One solution to maintaining a synchronized mailbox across multiple devices is Internet Message Access Protocol (IMAP).
- IMAP allows synchronizing read, moved, and deleted messages.
- The IMAP protocols re more complicated than the POP3 protocol commands. A few examples are:
	- **LOGIN \<username> \<password>** authenticates the user
	- **SELECT \<mailbox>** selects the mailbox folder to work with
	- **FETCH \<mail_number> \<data_item_name>** Example **fetch 3 body\[]**  to fetch message number 3, header and body
	- **MOVE \<sequence_set> \<mailbox>** moves the specified messages to another mailbox
	- **COPY \<sequence_set> \<data_item_name>** copies the specified messages to another mailbox
	- **LOGOUT** logs out
### Networking Secure Protocols
- Transport Layer Security (TLS) is added to existing protocols to protect communication confidentiality, integrity, and authenticity. Consequently HTTP, POP3, SMTP, and IMAP become HTTPS, POP3S, SMTPS, and IMAPS, where the appended "S" stands for Secure. 
- TLS ensures that no one can read or modify the exchanged data.
- The first step for every server (or client) that needs to identify itself is to get a signed TLS certificate.
- HTTP relies on TCP and uses port 80 by default and all traffic is sent in cleartext. 
- HTTPS stands for Hypertext Transfer Protocol Secure. It is basically HTTP over TLS. Exchanged traffic is encrypted and there is no way to know the contents without acquiring the encryption key.
- telnet sends traffic in clear text. This problem necessitated a solution.
- Nowadays, when you use an SSH client, it is most likely based on OpenSSH libraries and source code. Some benefits are:
	- Secure authentication
	- Confidentiality
	- Integrity
	- Tunneling
	- X11 Forwarding
- Virtual Private Network (VPN) - the VPN client will encrypt the traffic and pass it to the main branch via the established tunnel (shown in blue). The VPN traffic is limited to the blue lines; the green lines would carry the decrypted VPN traffic.
![[Pasted image 20260217142831.png]]

### Wireshark: The Basics
- Wireshark is an open-source, cross-platform network packet analyzer tool capable of sniffing and investigating live traffic and inspecting packet captures (PCAP). 
- Wireshark is one of the most potent traffic analyzer tools available in the wild. 
![[Pasted image 20260217143038.png]]

- Wireshark has two type of packet coloring methods: temporary rules that are only available during a program session and permanent rules that are saved under the preference file (profile) and available for the next program session. 
- Default permanent coloring is shown below.
![[Pasted image 20260217143218.png]]
- You can use the blue "shark button" to start network sniffing (capturing traffic), the red button will stop the sniffing, and the green button will restart the sniffing process.
- Wireshark can combine two pcap files into one single file. YOu can use the "File --> Merge" menu path to merge a pcap with the processed one. 
- Packets consist of 5 to 7 layers based on the OSI model.
![[Pasted image 20260217143444.png]]
	- The Frame (Layer 1)
	- Source \[MAC] (Layer 2)
	- Source \[IP] (Layer 3)
	- Protocol (Layer 4)
	- Protocol Errors (continuation of Layer 4)
	- Application Protocol (Layer 5)
	- Application Data (extension of Layer 5)
- The most basic way of filtering is to use the "right-click meu" or "Analyze --> Apply as Filter" menu to filter the specific value.
### TCPdump: The Basics
- The TCPdump tool and its libpcap is the foundation for various other networking tools today. Moreover, it was ported to MS Windows as wincap.
- Specify the Network Interface: First thing to decide is which network interface to listen to using **-i INTERFACE**. You can choose to listen on all available interfaces using **-i any**; alternatively you can specify an interface you want to listen on, such as **-i eth0**. 
- **-w FILE** to save file.
- **-r FILE** to read a file.
- **-c COUNT** to specify the number of packets to capture.
- **man tcpdump** for the manual page.
- Filtering by Host
![[Pasted image 20260218103018.png]]
- Filtering expressions:

| Command                                  | Explanation                                                     |
| ---------------------------------------- | --------------------------------------------------------------- |
| tcpdump host IP or tcpdump host HOSTNAME | Filters packets by IP address or hostname                       |
| tcpdump src host IP                      | Filters packets by a specific source host                       |
| tcpdump dst host IP                      | Filters packets by a specific destination host                  |
| tcpdump port PORT_NUMBER                 | Filters packets by port number                                  |
| tcpdump src port PORT_NUMBER             | Filters packets by the specified source port number             |
| tcpdump PROTOCOL                         | Filters packets by protocol; examples include ip, ip6, and icmp |
- Displaying packets:

| Command     | Explanation                                        |
| ----------- | -------------------------------------------------- |
| tcpdump -q  | Quick and quite: brief packet information          |
| tcpdump -e  | Include MAC addresses                              |
| tcpdump -A  | Print packets as ASCII encoding                    |
| tcpdump -xx | Display packets in hexadecimal format              |
| tcpdump -x  | Show packets in both hexadecimal and ASCII formats |
### Nmap: The Basics
- Nmap (Network Mapper) is an open-source tool used for network discovery and security auditing. It also assists in the exploration of network hosts and services, providing information about open ports, operating systems, and other details.
- Nmap uses multiple ways to specify its targets:
	- IP range using **-**: if you want to scan all the IP addresses from 192.168.0.1 to 192.168.0.10, you can write 192.168.0.1-10
	- IP subnet using **/**: if you want to scan a subnet, you can express it as 192.168.0.1/24, and this would be equivalent to 192.168.0.0-255
	- Hostname: You can also specify your target by hostname, for example, **example.thm**.
- Scanning a "Local" Network
	- Nmap offers the **-sn** option, i.e., ping scan. However, don't expect this to be limited like **ping**.
	- Because we are scanning the local network, where we are connected via Ethernet or Wifi, we can look up the MAC address of the devices. Consequently, we can figure out the network card vendors, which is beneficial information as it can help us guess the type of target device(s). 
![[Pasted image 20260218105008.png]]
 - Scanning a "Remote" Network
	- In this context, "remote" means that at least one route separates our system from this network.
	- Our system has the IP address **192.168.66.89** and belongs to the **192.168.66.0/24** network. In the terminal below we scan the target network **192.168.11.0/24** were there are two or more routers (hops) separate our local system from the targets.
![[Pasted image 20260218105301.png]]
- Nmap offers a list scan with the option **-sL**.. This scan only lists the targets to scan without actually scanning them. For example, **nmap -sL 192.168.0.1/24** will list the 256 targets that will be scanned. This option helps confirm the targets before running the actual scan.
- The **-sn** flag aims to discover live hosts without attempting to discover the services running on them. This might be helpful if you want to discover the devices on a network without causing much noise. 
- By design, TCP has 65,535 ports, and the same applies to UDP.
- The easiest and most basic way to know whether a TCP port is open would be to attempt to **telnet** to the port. 
- **Connect Scan** - The connect scan can be triggered using **-sT**. This tries to complete the TCP three-way handshake with every target TCP port.
- **SYN Scan (Stealth)** - Unlike the connect scan, which tries to connect to the target TCP port, i.e., complete a three-way handshake, the SYN scan only executes the first step: it sends a TCP SYN packet. You can select the SYN scan using the **-sS** flag.
- **Scanning UDP Ports** - Nmap offers the option **-sU** to scan for UDP services. 
- Nmap scans the most common 1,000 ports by default. 

| Option     | Explanation                                                    |
| ---------- | -------------------------------------------------------------- |
| -sT        | TCP connect scan - complete three-way handshake                |
| -sS        | TCP SYN - only first step of the three-way handshake           |
| -sU        | UDP scan                                                       |
| -F         | Fast mode- scans the 100 most common ports                     |
| -p\[range] | Specifies a rang of port number - **-p-** scans all the ports. |
- Nmap Version Detection: Extract More Information

| Option | Explanation                                          |
| ------ | ---------------------------------------------------- |
| -O     | OS detection                                         |
| -sV    | Service and version detection                        |
| -A     | OS detection, version detection, and other additions |
| -Pn    | Scan hosts that appear to be down                    |
- Nmap provides various options to control the scan speed and timing

| Option                                                            | Explanation                                                                                        |
| ----------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| -T\<0-5>                                                          | Timing template - paranoid (0), sneaky (1), polite (2), normal (3), aggressive (4), and insane (5) |
| --min-parallelism \<numprobes> and --max-parallelism \<numprobes> | Minimum and maximum rate (packets/second)                                                          |
| --host-timeout                                                    | Maximum amount of time to wait for a target host                                                   |
- Verbosity and Debugging - The best way to get more updates about what's happening is to enable verbose output by adding **-v**. 
- You can increase the verbosity level by adding another "v" such as **-vv** or even **-vvv**. 
- If all this verbosity does not satisfy your needs, you must consider the **-d** for debugging-level output. 
- Saving Scan Report
	- **-oN \<filename>** - Normal Output
	- **-oX \<filename>** - XML output
	- **-oG \<filename>** - grep-able output (useful for grep and awk)
	- **-oA \<basename>** - Output in all major formats.

## Cryptography
### Cryptography Basics
- Cryptography's ultimate purpose is to ensure *secure communication in the presence of adversaries.*
- Cryptography is used to protect confidentiality, integrity, and authenticity. 
![[Pasted image 20260219100816.png]]

![[Pasted image 20260219100831.png]]
- **Symmetric encryption**, also known as **symmetric cryptography**, uses the same key to encrypt and decrypt the data. Keeping the kay secret is a must; it is also called **private key cryptography**. 
![[Pasted image 20260219101010.png]]
- **Asymmetric Encryption** uses a pair of keys, one to encrypt and the other to decrypt. This is also called, **public key cryptography**. 
![[Pasted image 20260219101108.png]]
- XOR, short of "exclusive OR", is a logical operation in binary arithmetic that plays a crucial role in various computing and cryptographic applications. In binary, XOR compares two bits and returns 1 if the bits are different and 0 if they are the same.

| A   | B   | A ⊕ B |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 1   | 0   | 1     |
| 1   | 1   | 1     |
- **Modulo Operation**, commonly written as **%** or as **mod**. The modulo operator, X%Y, is the remainder when X is divided by Y. 
- 25%5 = 0 because 25 divided by 5 is 5, with a remainder of 0, i.e., 25 = 5 X 5 + 0
### Public Key Cryptography Basics
- **Authentication:** You want to be sure you communicate with the right person, not someone else pretending.
- **Authenticity:** You can verify that the information comes from the claimed source.
- **Integrity:** You must ensure that no one changes the data you exchange.
- **Confidentiality:** You want to prevent an unauthorized party from eavesdropping on your conversations.
- **RSA** is a public-key encryption algorithm that enables secure data transmission over insecure channels. RSA is based on the mathematically difficult problem of factoring a large number. 
- **Diffie-Hellman Key Exchange:** Key exchange aims to establish a shared secret between two parties. It is a method that allows two parties to establish a shared secret over an insecure channel without requiring a pre-existing shared secret and without an observer being able to get this key. Diffie-Hellman Key Exchange is often used alongside RSA public key cryptography.
- **SSH** - you should treat your private SSH keys like passwords. Using tools like John the Ripper, you can attack an encrypted SSH key to attempt to find the passphrase, highlighting the importance of using a complex passphrase.
- Leaving an SSH key in the **authorized_keys** file on a machine can be a useful backdoor, and you don't need to deal with any of the issues of un-stabilized reverse shells like Control-C or lack of tab completion.
- **Digital Signature** - Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Using symmetric cryptography, you produce a signature with your private key, which can be verified using your public key. 
- Some articles use terms such as electronic signature and digital signature interchangeably. In this task, the term *digital signature* refers to signing a document using a private key or certificate.
- **Certificates**: Certificates are an essential application of public key cryptography, and they are also linked to digital signature. A common place where they are used is for HTTPS. 
- The certificates have a chain of trust, starting with a root CA (Certificate Authority). 
- **PGP** stands for Pretty Good Privacy. It's software that implements encryption for encrypting files, performing digital signing, and more.
- **GPG** is commonly used in email to protect the confidentiality of email messages. Furthermore, it can be used to sign an email message and confirm its integrity. 
- **Cryptography**: is the science of securing communication and data using codes and ciphers.
- **Cryptanalysis**: is the study of methods to break or bypass cryptographic security systems without knowing the key.
- **Brute-Force Attack**: is an attack method that involves trying every possible key or password to decrypt a message.
- **Dictionary Attack**: is an attack method where the attacker tries dictionary words or combinations of them.
### Hashing Basics
- A **hash value** is a fixed-size string or characters that is computed by a hash function. A **hash function** takes an input of an arbitrary size and returns an output of fixed length, i.e., hash value. 
- Hash functions are different from encryption. There is no key, and it's meant to be impossible (or computationally impractical) to go from output back to the input. 
- Hashing helps protect data's integrity and ensure password confidentiality.
- A hash collision is when two different inputs give the same output. 
- The **pigeonhole effect** states that the number of items (pigeons) is more than the number of containers (pigeonholes); some containers must hold more than one item.
- **Three insecure practices** when it comes to passwords:
	- Storing passwords in plaintext.
	- Storing passwords using a deprecated encryption.
	- Storing passwords using an insecure hashing algorithm.
- **Password salting** refers to adding a **salt**, i.e., a random value, to the password before it is hashed.
- A **Rainbow Table** is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash. 
- Websites like https://crackstation.net/ and https://hashes.com/en/decrypt/hash internally use massive rainbow tables to provide fast password cracking for **hashes without salts**. 
- On Linux, password hashes are stored in **/etc/shadow**, which is normally only readable by root. They used to be store in **/etc/passwd**, which was readable by everyone. 
- The **shadow** file contains the password information. Each line contains nine fields, separated by colons (:). The first two fields are the login name and the encrypted password. More information about the other fields can be found by executing **man 5 shadow** on a Linux system. 
- **MS Windows Passwords** are hashed using NTLM, a variant of MD4. They're visually identical to MD4 and MD5 hashes, so it's very important to use context to determine the hash type. 
- On MS Windows, password hashes are stored in the SAM (Security Accounts Manager). MS Windows tries to prevent normal users from dumping them, but tools like mimikatz exist to circumvent MS Windows security. 
- You can't "decrypt" password hashes. They're not encrypted. You have to crack the hashes by hashing many different inputs, potentially adding the salt if there is one and comparing it to the target hash. Once it matches, you know what the password was. Tools like https://hashcat.net/hashcat/ and https://www.openwall.com/john/ are commonly used for these purposes. 
- Hashing can be used to check that files haven't been changed. 
- **HMAC (Keyed-Hash Message Authentication Code)** is a type of message authentication code (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data. 
### John the Ripper: The Basics
- John the Ripper is a well-known, well-loved, and versatile hash-cracking tool. It combines a fast cracking speed with an extraordinary range of compatible hash types. 
- A hash is a way of taking a piece of data of any length and representing it in another fixed-length form. Many popular hashing algorithms exist, such as MD4, MD5, SHA1, and NTLM. 
- Hashing functions are designed as one-way functions. In other words, it is easy to calculate the hash value of a given input; however, it is a hard problem to find the original input given the hash value. In simple terms, a hard problem quickly becomes computationally infeasible in computer science.
- This computational problem has its roots in mathematics as P vs NP.
	- P (Polynomial Time): Class P covers the problems whose solution can be found in polynomial time.
	- NO (Non-deterministic Polynomial Time): Problems in the class NP are those for which a given solution can be checked quickly, even though finding the solution itself might be hard.
	- John the Ripper, or John as it's commonly shortened, is a tool for conducting fast brute force attacks on various hash types (dictionary attack). 
- "Jumbo John" version of John the Ripper is the most popular extended version of John the Ripper.
- To check if John the Ripper has been installed you can type **john** into the terminal. 
-  https://github.com/openwall/john/blob/bleeding-jumbo/doc/INSTALL
## Exploitation Basics
### Moniker Link (CVE-2024-21413)
- On 2/13/2024, Microsoft announced RCE & credential link vulnerability with the assigned CVE of CVE-2024-21413.
### Metasploit: Introduction
- Metasploit is the most widely used exploitation framework. Metasploit is a powerful tool that can support all phases of a penetration testing engagement, from information gathering to post-exploitation.
- **msfconsole:** The main command-line interface.
- **Modules:** Suppporting modules such as exploits, scanners, payloads, etc.
- **Tools:** Stand-alone tools that will help vulnerability research, vulnerability assessment, or penetration testing. Some of these tools are msfvenom, pattern_create, and pattern_offset. 
- **Exploit:** A piece of code that uses a vulnerability present on the target system.
- **Vulnerability:** A design, coding, or logic flaw affecting the target system. The exploitation of a vulnerability can result in disclosing confidential information or allowing the attacker to execute code on the target system.
- **Payload:** An exploit will take advantage of a vulnerability. However, if we want the exploit to have the result we want, we need to use a payload. Payloads are the code that will run on the target system.
- **Auxiliary** - Any supporting module, such as scanners, crawlers, and fuzzers, can be found here:
![[Pasted image 20260221070802.png]]
- **Encoders** - Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them. Signature-based antivirus and security solutions have a database of known threats.
![[Pasted image 20260221070927.png]]
- **Evasion** - While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, "evasion" modules will try that, with more or less success.
![[Pasted image 20260221071232.png]]
- **Exploit** - Exploit, neatly organized by target system.
![[Pasted image 20260221071346.png]]
- **NOPs** - NOPs (No OPeration) do nothing, literally. They are represented in the Intel x86 CPU family with 0x90, following which the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes. 
![[Pasted image 20260221071601.png]]
- **Payloads** - Payloads are codes that will run on the target system. Exploits will leverage a vulnerability on the target system, but to achieve the desired result, we will need a payload. Examples could be; getting a shell, loading a malware or backdoor to the target system, running a command, or launching calc.exe as a proof of concept to add to the penetration test report.
![[Pasted image 20260221071941.png]]
- You will see four different directories under payloads:  adapters, singles, stagers, and stages.
	- **Adapters:** An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a PowerShell adapter, which will make a single PowerShell command that will execute the payload.
	- **Singles:** Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.
	- **Stagers:** Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. "Staged payloads" will first upload a stager on the target system then download the rest of payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
	- **Stages:** Downloaded by the stager. This will allow you to use larger sized payloads.
	- Metasploit has a subtle way to help you identify single (also called "inline") payloads and stages payloads.
		- generic/shell_reverse_tcp
		- windows/x64/shell/reverse_tcp
		- Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the "_" between "shell" and "reverse." While the latter is a staged payload, as indicated by the "/" between "shell" and "reverse".
- **Post** - Post modules will be useful on the final stage of the penetration testing process listed above, post-exploitation. 
![[Pasted image 20260221073246.png]]
- The Metasploit Framework can be launched using **msfconsole**command on any system the Metasploit Framework is installed on.
- The **msfconsole** can be used just like a regular command-line shell. 
![[Pasted image 20260221074437.png]]
- It will support most Linux commands, including **clear** (to clear the terminal screen), but will not allow you to use some features of a regular command line.
- The help command can be used on its own or for a specific command. Below is the help menu for the set command.
![[Pasted image 20260221074700.png]]
- You can use the history command to see commands you have typed earlier. 
- An important feature of msfconsole is the support of tab completion. 
- The module to be used can also be selected with the **use** command followed by the number at the beginning of the search line.
![[Pasted image 20260221074939.png]]
- While the prompt has changed, you will notice we can still run the commands previously mentioned. This means we did not "enter" a folder as you would typically expect in an operating system command line.
![[Pasted image 20260221075114.png]]
- The prompt tells us we now have a context set in which we will work. You can see this by typing the show options command.
![[Pasted image 20260221075226.png]]
- In this example, we will set the RHOSTS parameter to the IP address of our target system using the **set** command.
- Once you have set a parameter, you can use the **show options** command to check the value that was set correctly.
![[Pasted image 20260222084009.png]]
- **RHOSTS:** "Remote host", the IP address of the target system. A single IP address or a network range can be set. This will support the CIDR (Classless Inter-Domain Routing) notion (/24, /16, etc.) or a network range (10.10.10.x - 10.10.10.y). You can also use a file where the targets are listed, one target per file line using file:/path/of/the/target_file.txt.
- **RPORT:** "Remote port", the port on the target system the vulnerable application is running on.
- **PAYLOAD:** The payload you will use with the exploit.
- **LHOST:** "Localhost", the attacking machine IP address.
- **LPORT:** "Local port", the port you will use for the reverse shell to connect back to. This is a port on your attacking machine, and you can set it to any port not used by any other application.
- **Session:** Each connection established to the target system using Metasploit will have a session ID. You will use this with post-exploitation modules that will connect to the target system using an existing conneciton.
- You can override any set parameter using the set command again with a different value. You can also clear any parameter value using the **unset** command or clear all set parameters with the **unset all** command.
- You can use the **setg** command to set values that will be used for all modules. The **setg** command is used like the set command. You can clear any value set with **setg** using **unsetg**. 
- **Using modules** - Once all module parameters are set, you can launch the module using the **exploit** command. Metasploit also supports the **run** command, which is an alias created for the **exploit** command as the word exploit did not make sense when using modules that were not exploits (port scanners, vulnerability scanners, etc.). 
- The exploit command can be used without any parameters or using the "**-z**" parameter.
- The **exploit -z** command will run the exploit and background the session as soon as it opens.
- Some modules support the **check** option. This will check if the target system is vulnerable without exploiting it. 
- **Sessions** - You can use the **background** command to background the session prompt and go back to the msfconsole prompt. 
- Alternatively, **CTRL+Z** can be used to background sessions. 
- The **sessions** command can be used from the msfconsole prompt or any context to see the existing sessions.
- To interact with any session, you can use the **sessions -i** command followed by the desired session number.
### Metasploit: Exploitation
- You can list potential port scanning modules available using the **search portscan** command.
- **CONCURRENCY:** Number of targets to be scanned simultaneously.
- **PORTS:** Port range to be scanned. Metasploit will scan port numbers from 1 to 10000.
- **RHOSTS:** Target or target network to be scanned.
- **THREADS:** Number of threads that will be used simultaneously. More threads will result in faster scans. 
- You can use the **info** command for any module to have a better understanding of its use and purpose.
- Most of the exploits will have a preset default payload. However, you can always use the **show payloads** command to list other commands you can use with that specific exploit.
- Once you have decided on the payload, you can use the **set payload** command to make your choice.
### Metasploit: Meterpreter
- Meterpreter is a Metasploit payload that supports the penetration testing process with many valuable components. 
- Meterpreter runs on the target system but is not installed on it. It runs in memory and does not write itself to the disk on the target. This feature aims to avoid being detected during antivirus scans.
- We have used the **msfvenom --list payloads** command and grepped "meterpreter" payloads (adding **| grep meterpreter** to the command line), so the output only shows these. 
![[Pasted image 20260222091912.png]]
## Web Hacking
### Web Application Basics
- The **Front End** are the parts that you can see and interact with.
	- **HTML** (Hypertext Markup Language) is a foundational aspect of web applications. It is a set of instructions or code that instructs a web browser on what to display and how to display it. 
	- **CSS** (Cascading Style Sheets) in web applications describes a standard appearance, such as certain colors, types of text, and layouts.
	- **JS** (JavaScript) is part of a web application front end that enables more complex activity in the web browser. Whereas HTML can be considered a simple set of instructions on what to display, JavaScript is a more advanced set of instructions that allow choices and decisions to be made on what to display.
- The **Back End** of a web application is things you don't see within a web browser but are important for the web application to work. 
	- This involves things such as the **Database**, other **Infrastructure** components, and **WAF** (Web Application Firewall).
- Uniform Resource Locater (URL) is a web address that lets you access all kinds of online content.
![[Pasted image 20260223144635.png]]
- **Scheme** - The **scheme** is the protocol used to access the website.
- **User** - Some URLs can include a user's login details (usually a username) for sites that require authentication.
- **Host/Domain** - The **host** or **domain** is the most important part of the URL because it tells you which website you're accessing. 
- **Port** - The **port number** helps direct your browser to the right service on the web server.
- **Path** - The **path** points to the specific file or page on the server that you're trying to access.
- **Query String** - The **query string** is the part of the URL that starts with a question mark (?). It's often used for things like search terms or form inputs.
- **Fragment** - The **fragment** starts with a hash symbol (#) and helps point to a specific section of a webpage - like jumping directly to a particular heading or table.
- There are two types of HTTP messages:
	- **HTTP Requests**: Sent by the user to trigger actions on the web application.
	- **HTTP Responses:** Sent by the server in response to the user's request. 
- **Start Line** - The start line is like the introduction of the message. It tells you what kind of message is being sent - whether it's a request from the user or a response from the server. 
- **Headers** - Headers are made up of key-value pairs that provide extra information about the HTTP message.
- **Empty Line** - The empty line is a little divider that separates the header from the body. 
- **Body** - The body is where the actual data is stored.
- An **HTTP request** is what a user sends to a web server to interact with a web application and make something happen.
- The **request line** (or start line) is the first part of an HTTP request and tells the server what kind of request it's dealing with. It has three main parts: the **HTTP method**, the **URL path**, and the **HTTP version**. 
- The first line in every HTTP response is called the **Status Line**. It give you three key pieces of info:
	- **HTTP Version, Status Code,** and **Reason Phrase**
- **Information Responses (100 - 199)**
- **Successful Responses (200 - 299)**
- **Redirection Messages (300 - 399)**
- **Client Error Responses (400 - 499)**
- **Server Error Responses (500 - 599)**
	- Common status codes: **100 (Continue), 200 (OK), 301 (Moved Permanently), 404 (Not Found), and 500 (Internal Server Error)
### JavaScript Essentials
- JavaScript (JS) is a popular scripting language that allows web developers to add interactive features to websites containing HTML and CSS (styling). 
- Variables are containers that allow you to store data values in them. There are three ways to declare variables in JS: **var**, **let**, and **const**. 
- **Data Types** - In JS, data types define the type of value a variable can hold. Examples include **string** (text), **number**, **boolean** (true/false), null, undefined, and object (for more complex data like arrays or objects).
- **Functions** - A function represents a block of code designed to perform a specific task.
- **Loops** - Loops allow you to run a code block multiple times as long as a condition is **true**. 
- JS is an **interpreted** language, meaning the code is executed directly in the browser without prior compilation. 
- Internal JS refers to embedding the JS code directly within an HTML document. 
- External JS involves creating and storing JS code in separate file ending with a **.js** file extension. 
- When pen-testing a web application, it is important to check whether the website uses internal or external JS. This can be easily verified by viewing the page's source code.
- Best practices - Avoid relying on Client-Side Validation Only, Refrain from Adding Untrusted Libraries, Avoid Hardcoded Secrets, Minify and Obfuscate You JavaScript Code.
### SQL Fundamentals
- There are quite a few different types of databases that can be bult, but to primary types are: **relational databases** (aka SQL) & **non-relational databases** (aka NoSQL)
- ![[Pasted image 20260223153822.png]]
- **Relational databases:** Store structured data, meaning the data inserted into this database follows a structure.
- **Non-relational databases:** Instead of storing data the above way, store data in a non-tabular format. 
![[Pasted image 20260223153936.png]]
- **Primary and Foreign Keys** - There are to types of **keys:** 
	- **Primary Keys** - A primary key is used to ensure that the data collected in a certain column is unique.
	- **Foreign Keys** - A foreign key is a column (or columns) in a table that also exists in another table within a database, and therefore provides a link between the two tables. 
- The benefits of SQL and relational databases
	- It's fast, easy to learn, reliable, and flexible. 
- **CRUD** operations results are fundamental for data operations and when interacting with databases.
	- **Create (INSERT statement)** - Adds a new record to the table.
	- **Read (SELECT statement)** - Retrieves record from the table.
	- **Update (UPDATE statement)** - Modifies existing data in the table.
	- **Delete (DELETE statement)** - Removes record from the table.
### Burp Suite: The Basics
- In essence, Burp Suite is a Java-based framework designed to serve as a comprehensive solution for conducting web application penetration testing. It has become the industry standard tool for hands-on security assessments of web and mobile applications, including those that rely on application programming interfaces (APIs). 
- Burp Suite Community offers **Proxy, Repeater, Intruder, Decoder, Comparer, and Sequencer**. 
- **Intercepting Requests:** When requests are made through the Burp Proxy, they are intercepted and held back from reaching the target server. 
- **FoxyProxy** allows you to connect to the Burp Suite Proxy. 
## Offensive Security Tooling
### Hydra
- Hydra is a brute force online password cracking program, a quick system login password "hacking" tool. Hyrda can run through a list and "brute force" some authentication services. 
- The options we pass into Hydra depend on which service (protocol) we're attacking. For example, if we wanted to brute force FTP with the username being **user** and a password list being **passlist.txt**, we'd use the following command: hydra -l user -P passlist.txt ftp://MACHINE_IP
### Gobuster
- Gobuster is an open-source offensive tool written in Golang. It enumerates web directories, DNS subdomains, vhosts, Amazon S3 buckets, and Google Cloud Storage by brute force, using specific wordlists and handling the incoming responses.
- Looking at the phases of ethical hacking, Gobuster could be placed between the reconnaissance and scanning phases.
- Gobuster is included by default in distributions like Kali Linux. 
- **gobuster --help** - This help page gives us a good overview of its functionalities and options.
![[Pasted image 20260224095956.png]]
### Shells Overview
- Shells in cyber security are widely used by attackers to remotely control systems, making them an important part of the attack chain.
- A shell is software that allows a user to interact with an OS. It can be a graphical interface, but it is usually a command-line interface, and this will depend on the operating system running on the target system.
- Shells allow attackers to execute several activities:
	- **Remote System Control**
	- **Privilege Escalation**
	- **Data Exfiltration**
	- **Persistence and Maintenance Access**
	- **Post-Exploitation Activities**
	- **Access Other Systems on the Network**
- **Reverse Shell** - A reverse shell, sometimes referred to as a "connect back shell," is one of the most popular techniques for gaining access to a system in cyberattacks. The connections initiate form the target system to the attacker's machine, which can help avoid detection from network firewalls and other security appliances.
- **How Reverse Shells Work**
	- **Set up a Netcat (nc) Listener** - A reverse shell will connect back to the attacker's machine. This machine will be waiting for a connection, so Netcat can be used ot listen to a connection using the following command **nc -lvnp 443**. 
	- The **-l** option indicates to Netcat to listen or wait for a conneciton.
	- **-v** option enables verbose mode. 
	- **-n** option prevents the connections from using DNS for lookup.
	- **-p** flag indicates the port that will be used to wait for the connection.
	- Any port can be used to wait for a connection, but attackers and pentesters tend to use known ports by other applications like 53, 80, 8080, 443, 139, or 445. This is to blend the reverse shell with legitimate traffic and avoid detection by security appliances. 
- **Gaining Reverse Shell Access** - Once we have our listener set, the attacker should execute what is known as a reverse shell payload. This payload usually abuses the vulnerability or unauthorized access granted by the attacker and executes a command that will expose the shell through the network. There's a variety of payloads that will depend on the tools and OS of the compromised system. We can explore some of them here - [Reverse Shell Cheat Sheet | pentestmonkey](https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet).
- **Attacker Receives the Shell** - Once the payload is executed, the attacker will receive a **reverse shell**, as shown below, allowing them to execute commands as if they were logging into a regular terminal in the OS.
![[Pasted image 20260224101658.png]]
- **Bind Shell** - A bind shell will bind a port on the compromised system and listen for a connection; when this connection occurs, it exposes the shell session so the attacker can execute command remotely.
- This method can be used when the compromised target does not allow outgoing connections, but it tends to be less popular since it needs to remain active and listen for connections, which can lead to detection.
- Once the Bind Shell setup is executed, it will wait for an incoming connection.
- Now that the target machine is waiting for incoming connections, we can use Netcat to connect.
- **Shell Listeners**
	- **Rlwrap** - It is a small utility that used the GNU readline library to provide editing keyboard and history.
	- **Ncat** - Ncat is an improved version of Netcat distributed by the NMAP project. It provides extra features, like encryption (SSL). 
![[Pasted image 20260224103948.png]]
	- **Socat** - It is a utility that allows you to create a socket connection between two data sources.
- **Shell Payloads** - A Shell Payload can be a command or script that exposes the shell to an incoming connection in the case of a bind shell or send connection in the case of a reverse shell. 
- Payloads that can be used in the Linux OS to expose the shell through the most popular **reverse shell** are:
	- **Bash**
	- **PHP**
	- **Python**
	- **Telnet**
	- **AWK**
	- **BusyBox**
- **Web Shell** - A web shell is a script written in a language supported by a compromised web server that executes command through the web server itself. A web shell is usually a file containing the code that executes commands and handles files. It can be hidden within a compromised web application or service, making it difficult to detect and very popular among attackers. 
	- **Example PHP Web Shell**
![[Pasted image 20260224104740.png]]
- Some of the most popular web shells that can be found online are:
	- [flozz/p0wny-shell: Single-file PHP shell](https://github.com/flozz/p0wny-shell) - A minimalistic single-file PHP web shell that allows remote command execution.
	- [b374k/b374k: PHP Webshell with handy features](https://github.com/b374k/b374k) - A more feature-rich PHP web shell with file management and command execution, among other functionalities.
	- [c99 Shell Download](https://www.r57shell.net/single.php?id=13) - A well-known and robust PHP web shell with extensive functionality.
### SQLMap: The Basics
 - SQL injection is a prevalent vulnerability and has long been a hot topic in cyber security. 
 - A database is a collection of data that can be stored, modified, and retired. 
 - Carrying out an SQL injection attack involves discovering the SQL injection vulnerability inside the application and manipulating the database. 
 - **SQLMap** is an automated tool for detecting and exploiting SQL injection vulnerabilities in web applications. The **--help** command with SQLMap will list all available flags you can use.
 - If you don't want to manually add the flags to each command, use the **--wizard** flag with SQLMap. When you use this flag, the tool will guide you through each step and ask questions to complete the scan, making it perfect for beginners.
## Defensive Security
### Defensive Security Intro
- Refer to [[1_Pre_Security]]
### SOC Fundamentals
- A **SOC** (Security Operations Center) is a dedicated facility operated by a specialized security team.
- **Detection**
	- Detect vulnerabilities, detect unauthorized activity, detect policy violations, detect intrustions.
- **Response** 
	- Support with the incident response.
- There are three pillars of a SOC.
	- People, Process, and Technology
- The **People** are known as the SOC team. 
![[Pasted image 20260224111139.png]]
- **Process** - Each role has its own processes. The alert triage is the basis of the SOC team. The first response to any alert is to perform the triage. 
![[Pasted image 20260224111235.png]]
- **Technology** - refers to the security solutions. The security solutions efficiently minimize the SOC team's manual effort to detect and respond to threats.
	- **SIEM**: Security Information and Event Management 
	- **EDR**: Endpoint Detection and Response
	- **Firewall**
### Digital Forensics Fundamentals
- Forensics is the application of methods and procedures to investigate and solve crimes. The branch of forensics that investigates cyber crimes is known as **digital forensics**. 
- **Digital Forensics Methodology**: 
	- **Collection** - the first phase of digital forensics is data collection.
	- **Examination** - The collected data may overwhelm due to its size.
	- **Analysis** - The investigators now have to analyze the data by correlating it with multiple pieces of evidence to draw conclusions.
	- **Reporting** - In the last phase of digital forensics, a detailed report is prepared. 
![[Pasted image 20260224111659.png]]
- There are different types of digital forensics, all with their own collection and analysis methodologies:
![[Pasted image 20260224111735.png]]
- **Evidence Acquisition**
	- **Proper Authorization** - The forensics team should obtain authorization from the relevant authorities before collecting any data.
	- **Chain of Custody** - A chain of custody is a formal document containing all the details of the evidence.
	- **Write Blockers** - Write blockers are an essential part of the digital forensics team's toolbox. Write blockers can block any evidence alteration actions. 
	- **Windows Forensics** 
		- Two different categories of forensic images are taken from a Windows operating system.
			- **Disk Image** - contains all the data present on the storage device on the system (HDD, SSD, etc.). 
			- **Memory Image** - The memory image contains the data inside the operating system's RAM. This memory is volatile, meaning the data will get lost after the system is powered off or restarted. 
		- **FTK Imager** - FTK Imager is a widely used tool for taking disk images of Windows operating systems. 
		- **Autopsy** - Autopsy is a popular open-source digital forensics platform.
		- **DumpIt** - DumptIt offers the utility of taking a memory image from a Windows operating system.
		- **Volatility** - Volatility is a powerful open-source tool for analyzing memory images.
### Incident Response Fundamentals
- Refer to [[1_Pre_Security]]
### Logs Fundamentals
|Log Type|Usage|Example|
|---|---|---|
|System Logs|The system logs can be helpful in troubleshooting running issues in the OS. These logs provide information on various operating system activities.|- System Startup and shutdown events  <br>- Driver Loading events  <br>- System Error events  <br>- Hardware events|
|Security Logs|The security logs help detect and investigate incidents. These logs provide information on the security-related activities in the system.|-Authentication events  <br>- Authorization events  <br>- Security Policy changes events  <br>- User Account changes events - Abnormal Activity events|
|Application Logs|The application logs contain specific events related to the application. Any interactive or non-interactive activity happening inside the application will be logged here.|- User Interaction events  <br>- Application Changes events  <br>- Application Update events  <br>- Application Error events|
|Audit Logs|The Audit logs provide detailed information on the system changes and user events. These logs are helpful for compliance requirements and can play a vital role in security monitoring as well.|- Data Access events  <br>- System Change events  <br>- User Activity events  <br>- Policy Enforcement events|
|Network Logs|Network logs provide information on the network’s outgoing and incoming traffic. They play crucial roles in troubleshooting network issues and can also be handy during incident investigations.|- Incoming Network Traffic events  <br>- Outgoing Network Traffic events  <br>- Network Connection Logs - Network Firewall Logs|
|Access Logs|The Access logs provide detailed information about the access to different resources. These resources can be of different types, providing us with information on their access.|- Webserver Access Logs  <br>- Database Access Logs - Application Access Logs  <br>- API Access Logs|
- **Windows Event Logs Analysis** - Windows OS has a utility known as Event Viewer, which gives a nice graphical user interface to view and search for anything in these logs. 
- Here is a table of some important Event IDs in Windows OS:

| Event ID | Description                                        |
| -------- | -------------------------------------------------- |
| 4624     | A user account successfully logged in              |
| 4625     | A user account failed to login                     |
| 4634     | A user account successfully logged off             |
| 4720     | A user account was created                         |
| 4724     | An attempt was made to reset an account's password |
| 4722     | A user account was enabled                         |
| 4725     | A user account was disabled                        |
| 4726     | A user account was deleted                         |
## Security Solutions
### Introduction to SIEM
- Security Information and Event Management system (SIEM) is the core security solution that a SOC analyst uses in the security operations center.
![[Pasted image 20260224113541.png]]
- Features of SIEM: Centralized Log Collection, Normalization of Logs, Correlation of Logs, Real-time Alerting, Dashboards and Reporting
### Firewall Fundamentals
- A firewall is designed to inspect a network's or digital device's incoming and outgoing traffic. The firewall will allow or deny traffic based on its maintained rules.
- **Types of Firewalls**
	- **Stateless Firewall** - This type of firewall operates on layer 3 and layer 4 of the OSI model and works solely by filtering the data based on predetermined rules without taking note of the previous connections.
	- **Stateful Firewall** - Unlike stateless firewalls, this type of firewall goes beyond filtering packets by predetermined rules. It also keeps track of pervious connections and stores them in a stable table.
	- **Proxy Firewall** - The problem with previous firewalls was their inability to inspect the contents of a packet. Proxy firewalls, or application-level gateways, act as intermediaries between the private network and the Internet and operate on the OSI model's layer 7.
	- **Next-Generation Firewall (NGFW)** - This is the most advance typed of firewall that operates from layer 3 to layer 7 of the OSI model, offering deep packet inspection and other functionalities that enhance the security of incoming and outgoing network traffic. It has an intrusion prevention system that blocks malicious activities in real time. 
- **Windows Defender Firewall** - This firewall contains all the basic functionality for creating, allowing, or denying specific programs or creating customized rules. 
- **Linux iptables Firewall**
	- **Netfilter** - Netfilter is the framework inside the Linux OS with core firewall functionalities, including packet filtering, NAT, and connection tracking.
	- ufw (Uncomplicated Firewall), as the name says, eliminates the complications of making rules in a complex syntax in "iptables", by giving you an easier interface.
### IDS Fundamentals
- **Intrusion Detection System (IDS)** - detects malicious activities in a timely manner. 
- **Host Intrusion Detection System (HIDS):** Host-based IDS solutions are installed individually on the hosts and are responsible for only detecting potential security threats associated with that particular hose. 
- **Network Intrusion Detection System (NIDS):** Network-based IDS solutions are crucial in detecting potentially malicious activities within the whole network, regardless of any specific hosts. 
![[Pasted image 20260224115131.png]]
- **Detection Modes**
	- **Signature-Based IDS:** Many attacks occur every day. Each attack has its unique pattern, which is known as a signature. 
	- **Anomaly-Based IDS:** This type of IDS first learns the normal behavior (baseline) of the network or system and performs detections if there is any deviation from the normal behavior. Anomaly-based IDS can also detect zero-day attacks because they don't rely on available signatures for detection.
	- **Hybrid IDS:** A hybrid IDS combines the detection methods of signature-based IDS and anomaly-based IDS to leverage the strengths of each approach.
- **IDS Example: Snort**
	- Snort is one of the most widely used open-source IDS solutions developed in 1998. It uses signature-based and anomaly-based detections to identify known threats.
![[Pasted image 20260224115626.png]]
### Vulnerability Scanner Overview
- Vulnerabilities are weaknesses inside of the software or hardware. The process of fixing the vulnerabilities is known as patching.
- **Authenticated Scans** - credentials of the subject host must be provided to the vulnerability scanner. Identifies the vulnerabilities that can be exploited by the attackers having access to the host.
- **Unauthenticated Scans** - The vulnerability scanner does not require the host's credentials; it only needs the IP address. Identifies the vulnerabilities that can be exploited by an external attacker having no access to the subject host. 
- **External & Internal Scans**
- **Tools for Vulnerability Scanning**
	- **Nessus**
	- **Qualys**
	- **Nexpose**
	- **OpenVAS (Open Vulnerability Assessment System)**
- **CVE** - CVE stands for Common Vulnerabilities and Exposures. Consider CVE a unique number for each of your inquiries and complaints. 
	- **CVE prefix:** Every CVE number has the prefix "CVE" in the beginnning.
	- **Year**: The second part of every CVE number contains the year it was discovered.
	- **Arbitrary Digits:** The last part of the CVE numbers contains four or more arbitrary digits. 
- **CVSS** - CVSS stands for Common Vulnerability Scoring System. The CVSS score is calculated by considering multiple factors, including its impact, ease of exploitability, etc. 

| CVSS Score Range | Severity Levels |
| ---------------- | --------------- |
| 0.0 - 3.9        | Low             |
| 4.0 - 6.9        | Medium          |
| 7.0 - 8.9        | High            |
| 9.0 - 10         | Critical        |
## Defensive Security Tooling
### CyberChef: The Basics
- CyberChef is a simple, intuitive web-based application designed to help with various "cyber" operation tasks within your browser. Think of it as a Swiss Army knife for data - like having a toolbox of different tools designed to do a specific task. 
- There are different ways to access and run CyberChef.
	- **Online Access** - All you need is a web browser and an internet connection. Then, you can can click this link  (https://gchq.github.io/CyberChef) to open CyberChef directly within your web browser.
	- **Offline or Local Copy** - You can run this offline or locally on your machine by downloading the latest release file from this link (https://github.com/gchq/CyberChef/releases). 
- CyberChef consists of four areas. These are:
	- 1 - Operations
	- 2 - Recipe
	- 3 - Input
	- 4 - Output
![[Pasted image 20260224121117.png]]
### CAPA: The Basics
- CAPA (Common Analysis Platform for Artifacts) is a tool developed by the FireEye Mandiant team. It is designed to identify the capabilities present in executable files like Portable Executables (PE), ELF binaries, .NET modules, shellcode, and even sandbox reports. 
- The beauty of CAPA is that it encapsulates years of reverse engineering knowledge into an automated tool. 
- To run the tool, open PowerShell, navigate to the correct directory where CAPA is installed, then run **capa** or **capa.exe**, then point to the binary. 
### REMnux: Getting Started
- The REMnux VM is a specialized Linux distro. It already includes tools like Volatility, YARA, Wireshare, oledump, and INetSim. It also provides a sandbox-like environment for dissecting potentially malicious software without risking your primary system. 
### FlareVM: Arsenal of Tools
- FlareVM, or "Forensics, Logic Analysis, and Reverse Engineering," stands out as a comprehensive and carefully curated collection of specialized tools uniquely designed to meet the needs of reverse engineers, malware analysts, incident responders, forensic investigators, and penetration testers. 
- **Arsenal of Tools** for Reverse Engineering & Debugging, Disassemblers & Decompilers, Static & Dynamic Analysis, Forensics & Incident Response, Network Analysis, File Analysis, Scripting & Authomation, and Sysinternals Suite.
## Build Your Cyber Security Career
- Refer to [[1_Pre_Security]]
## OWASP Top 10 (2025)
### OWASP Top 10 2025: IAA Failures
- IAAA (Identity, Authentication, Authorization, and Accountability)
- **Identity** - the unique account (e.g., User ID/email) that represents a person or service.
- **Authentication** - providing the identity (passwords, OTP, passkeys)
- **Authorization** - what identity is allowed to do.
- **Accountability** - recording and alerting on who did what, when, and from where.
- **A01: Broken Access Control** - Broken Access Control happens when the server doesn't properly enforce who can access what on every request. 
	- Enforce server-side checks on **every** request.
- **A07: Authentication Failures** - Authentication Failures happen when an application can't reliably verify or bind a user's identify.
	- Enforce unique indexes on the canonical form, rate-limit/lock out brute force, and rotate sessions on password/privilege changes.
- **A09: Logging & Alerting Failures** - When applications don't record or alert on security-relevant events, defenders can't detect or investigate attacks. 
	- Log the full auth lifecycle (fail/success, password/2FA/role changes, admin actions), centralize logs off-host with retention, and alert on anomalies (e.g., brute-force bursts, privilege elevation). 
### OWASP Top 10 2025: Application Design Flaws
- **AS02: Security Misconfigurations** - Security misconfigurations happen when systems, servers, or applications are deployed with unsafe defaults, incomplete settings, or exposed services. These are not code bugs but mistakes in how the environment, software, or network is set up. 
- **AS03: Software Supply Chain Failures** - Software supply chain failures happen when applications rely on components, libraries, services, or models that are compromised, outdated, or improperly verified.
- **AS04: Cryptographic Failures** - Cryptographic failures happen when encryption is used incorrectly or not at all. 
- **AS06: Insecure Design** - Insecure design happens when flawed logic or architecture is built into a system from the start. These flaws stem from skipped threat modelling, no design requirements or reviews, or accidental errors. 
### OWASP Top 10 2025: Insecure Data Handling
- **A04: Cryptographic Failures** - Cryptographic failures happen when sensitive data isn't adequately protected due to lack of encryption, faulty implementation, or insufficient security measures. 
- **A05: Injection** - Injection has been a long-standing feature on the OWASP Top 10 list. Injection remains a classic example of web exploitation. Injection occurs when an application takes user input and mishandles it.
- **A08: Software or Data Integrity Failures** - Software or Data Integrity Failures occur when an application relies on code, updates, or data it assumes are safe, without verifying their authenticity, integrity, or origin.