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

