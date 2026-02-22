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
