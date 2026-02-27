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
