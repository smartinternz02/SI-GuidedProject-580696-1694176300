# Week 2 Assignment

## 🔍 Assignment Overview

In this assignment, we will explore and demonstrate the use of various cybersecurity tools available in Kali Linux. Our goal is to gain practical knowledge and skills in each of the 10 primary categories within Kali Linux, ranging from Information Gathering to Social Engineering Tools. For each category, we will select one tool and delve into its description, use case, and provide step-by-step demonstrations to understand its functionality.

![Kali Photo](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/kali.png)

## 📋 10 Categories Listed in Kali Linux

- Information Gathering
- Vulnerability Analysis
- Web Application Analysis
- Database Assessment
- Password Attacks
- Wireless Attacks
- Reverse Engineering
- Exploitation Tools
- Sniffing Spoofing
- Post Exploitation

## ⚠️ Disclaimer

All the tools demonstrated and explored in this assignment have been used exclusively on websites either owned by me, specifically "owais-shariff.netlify.app," or on domains that have an active bug bounty program and are intended for bug bounty practice. I want to emphasize that I have the rights and permission to conduct Vulnerability Assessment and Penetration Testing (VAPT) tests on these websites.

For anyone seeking to replicate these tests or use similar tools, it is imperative to ensure that they perform such tests only on websites for which they have obtained explicit permission. I want to make it unequivocally clear that I do not authorize ANYONE to conduct VAPT tests on my personal website, "owais-shariff.netlify.app," or any other website under my ownership or management without my prior consent and written authorization. Unauthorized testing on any website is strictly prohibited and may have legal consequences. Please act responsibly and ethically when conducting VAPT tests on any web property.

## 🛠️ Demonstration & Exploration of the tools

### 1. Vulnerability Analysis (**nmap)**

**Description:** 

Nmap (Network Mapper) is a versatile open-source tool used for network discovery and security auditing. It can discover hosts and services on a network and identify potential vulnerabilities.

**Use Case:** 

Nmap is essential for Vulnerability Analysis as it helps in identifying open ports, services running on those ports, and potential weaknesses.

**Demonstration Steps:**

1. **Install Nmap:**
    - Begin by installing Nmap on your computer. You can download it from the official website ([https://nmap.org/download.html](https://nmap.org/download.html)) or use a package manager for your operating system.
2. **Determine the Target:**
    - Identify the target or network that you want to perform vulnerability analysis on. This could be a single host, a range of IP addresses, or an entire network.
3. **Vulnerability Scan:**
    - I Tried the BlueRoom on TryHackMe for depicting how to do a vulnerability scan on an IP.
    
    ```
    sudo nmap -sC --script vuln 10.10.39.151
    ```
        
4. **Output Results:**
    - Save the results of your Nmap scans to a file for further analysis. You can use the `oN` flag to specify the output format and file name.
    
    ```
    nmap -oN scan_results.txt <target>
    ```
    
7. **Analyze Results:**
    - Examine the results of your Nmap scans to identify potential vulnerabilities and security issues. Pay attention to open ports, service versions, and any specific vulnerabilities reported.

    ![Vulnerability Scan](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/nmvuln.webp)

As we can see from the above picture the ports open are 

  ```
    135/tcp
    139/tcp
    445/tcp
  ```
And the vulnerability is 

  ```
    ms17-010
  ```

We will make use of the above found details and use metasploit now.

### 2. Exploitation Tools (**metasploit framework)**

**Description:** 

The Metasploit Framework is a widely-used penetration testing tool that helps identify, exploit, and validate vulnerabilities in target systems.

**Use Case:** 

Metasploit Framework is crucial in Exploitation Tools to simulate real-world attacks and test system defenses.

**Demonstration Steps:**

1. Open the Metasploit console in Kali Linux.
    ![Console](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/msfconsole.jpeg)

2. Select a module for a specific vulnerability.Which in this case is **ms17-010**
    ![Module](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/msfmod.jpeg)

3. Configure Rhost & Lhost
    ![Configure](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/msfconfig.webp)

4. Use 2nd exploit since target machine on windows 7.
    ![Use](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/msfuse.webp)

5. Since we have access to the meterpreter now we do hashdump to get passwords.
    ![HashDump](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/meter.webp)

Use a website like [CrackStation](https://crackstation.net/). To crack the hashes and get the password.

6. Since this was a CTF room we are supposed to find Flags. We can use a simple command to search for them.
    ![Search](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/meterflag.webp)


### 3. Sniffing Spoofing (**Burpsuite)**

**Description:** 

Burp Suite is a popular cybersecurity tool used for web application security testing and analysis. Developed by PortSwigger, it serves as a comprehensive platform for identifying vulnerabilities and assessing the security posture of web applications. Burp Suite is widely employed by security professionals, penetration testers, and ethical hackers to discover and address security flaws in web applications before malicious actors can exploit them.

**Use Case:** 

1. Web Vulnerability Scanning: Burp Suite can automatically scan web applications for common vulnerabilities such as SQL injection, cross-site scripting (XSS), and insecure authentication mechanisms.
2. Proxy Server: It acts as a proxy server, allowing users to intercept and manipulate HTTP requests and responses, which is invaluable for understanding how web applications work and identifying potential vulnerabilities.
3. Spidering and Crawling: The tool can crawl websites to map their structure and identify hidden or forgotten content, helping testers identify potential attack surfaces.
4. Intruder: Burp Suite's Intruder tool enables automated brute-force and fuzzing attacks, making it easier to identify vulnerabilities related to input validation and authentication.
5. Repeater: This feature lets testers manually manipulate and replay individual HTTP requests, making it easy to test specific scenarios and vulnerabilities.
6. Reporting: Burp Suite provides customizable reporting options, allowing users to generate detailed vulnerability reports to share with development teams or stakeholders.
7. Extensions: The tool supports a wide range of extensions and add-ons, making it highly customizable and adaptable to different testing scenarios.

**Demonstration Steps:**

**Step 1: Install and Launch Burp Suite**
- Download and install Burp Suite from the [official website](https://portswigger.net/burp).
- Launch Burp Suite after installation.

**Step 2: Configure Proxy Settings**
- In Burp Suite, go to the "Proxy" tab, located in the left-hand sidebar.
- Under the "Intercept" sub-tab, ensure that the "Intercept is on" option is selected. This enables you to intercept and modify requests.
- Configure your browser or application to use Burp Suite as a proxy server. Typically, set the proxy IP address to "127.0.0.1" and the port to the one specified in Burp Suite (default is 8080). Configuration steps may vary depending on your browser or application.

**Step 3: Intercept Requests**
- With the proxy configured, use your browser or application as usual. All outgoing HTTP requests will be intercepted by Burp Suite.
- As you navigate to websites or use your application, intercepted requests will appear in the "Proxy" > "Intercept" tab of Burp Suite.

**Step 4: Inspect and Modify Requests**
- In the "Intercept" tab, you can see the intercepted requests. Select a request you want to inspect and click on it to view details.
- Modify the request by clicking the "Forward" button, making changes (e.g., modifying parameters or headers), and then clicking "Forward" again to send the modified request to the server.

**Step 5: Inspect and Modify Responses**
- After the server responds to your request, you can also intercept and modify the responses. They will appear in the "Intercept" tab.
- Click on a response to inspect it. Modify the response if needed, and then click "Forward" to send the modified response to your browser or application.

**Step 6: Continue Navigating**
- Continue navigating your web application, intercepting and modifying requests and responses as necessary.
- To stop intercepting requests, click the "Intercept is on" toggle to turn it off.

**Step 7: Review and Analysis**
- In the "Proxy" > "HTTP history" tab, review all intercepted requests and responses for analysis.
- Use this information to identify vulnerabilities, test security features, and gain a better understanding of how the application works.

**Step 8: Save and Export**
- If you want to save your proxy history or generate reports, you can export the data from the "HTTP history" tab or use Burp Suite's reporting features.


**This is from one of the practice challenges of [PicoCtf](https://play.picoctf.org)**

1. Intercept anyone HTTP request and forward the same without any modification.
    ![1](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/1.png)

2. In this http request we didn’t make any changes to the request.
    ![2](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/2.png)

3. Intercept another HTTP request and forward the same after modifying the request.
    ![3](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/3.png)

4. This is the http request with the jwt token set, This jwt token is for users. But we want access as an admin.
    ![4](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/4.png)

5. As you can see we changed the jwt toke (cookie). There are various websites  you can use to do so.
    ![5](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/5.png)

6. After changing the http request we can see this time we have been logged in as admin. And since this was a ctf challenge we got a flag.
    ![6](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/6.png)

### 4. Post Exploitation (**mimikatz)**

**Description:** 

Mimikatz is a powerful post-exploitation tool used to extract and manipulate credentials from compromised Windows systems.

**Use Case:** 

Mimikatz is critical in Post Exploitation scenarios to escalate privileges and gather sensitive information.

**Demonstration Steps:**

1. **Download and Extract Mimikatz:**
    - Download the latest Mimikatz release from the official GitHub repository ([https://github.com/gentilkiwi/mimikatz](https://github.com/gentilkiwi/mimikatz)).
    - Extract the contents to a directory on your Windows system, e.g., "C:\Mimikatz."
2. **Open an Elevated Command Prompt:**
    - On your Windows system, press `Win + X` and choose "Windows Terminal (Admin)" or "Command Prompt (Admin)" to open an elevated command prompt.
3. **Navigate to the Mimikatz Directory:**
    - Use the `cd` command to navigate to the directory where you extracted Mimikatz. For example:
        
        ```
        cd C:\\Mimikatz
        
        ```
        
4. **Load the Mimikatz Module:**
    - To use Mimikatz, you need to load its module. Run the following command:
        
        ```
        mimikatz.exe
        
        ```
        
5. **Dump Credentials from Memory:**
    - Inside the Mimikatz shell, you can use various commands to extract credentials. For example, to extract plaintext passwords from memory, use:
        
        ```
        sekurlsa::logonpasswords
        
        ```
        
6. **View Extracted Credentials:**
    - Mimikatz will display the extracted credentials, including usernames and plaintext passwords, if available.
7. **Additional Commands:**
    - Explore other Mimikatz commands to perform various post-exploitation activities, such as listing loaded DLLs, Kerberos ticket extraction, and more.
    

Note: This requires a vulnerable windows system. Mimikatz was built for Windows 7 and even worked till Windows 10 on some version. However, As of today for my system, Windows 11, This security vulnerability has been patched and is no longer effective. Which is why I will note be demonstrating this myself. 

You can read more about this at: 

[Microsoft's new Windows 11 update 'eradicates' a key hacker tactic](https://www.protocol.com/bulletins/microsoft-windows-11-credential-dumping)

However here’s a screenshot I found online showing what theh end result of the credential dumping looks like:

![Untitled](https://github.com/3xpl0itk1t/IBMQcourse/blob/main/Week%202/Week%202/mimikatz.png)
