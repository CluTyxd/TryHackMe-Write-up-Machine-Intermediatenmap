# Intermediate Nmap - TryHackMe Write-up

## Enumeration

The initial enumeration was performed using Nmap to identify open ports and potential attack vectors.

```bash
nmap <IP> -sS -sC -sV
```

While performing the scan, we discovered several high-numbered ports open on the target machine.

The `-sC` parameter executes the default NSE (Nmap Scripting Engine) scripts, allowing us to gather additional information about the discovered services, such as web page titles, SMB shares, SSL certificates, and other useful details.

The `-sV` parameter performs service version detection, identifying the exact software running on each open port.

During the initial enumeration, we were able to identify a note containing potential credentials: <br><br> <img width="924" height="566" alt="image" src="https://github.com/user-attachments/assets/d3ca1430-bf05-4c62-a4b7-649235fa46fc" /> <br><br>

## Web Enumeration

When accessing the web application running on port `31337`, we found the same credentials exposed on the page: <br><br> <img width="1002" height="291" alt="image" src="https://github.com/user-attachments/assets/f819c7ff-fd19-4a89-af11-67e030d65a11" /> <br><br>

## Initial Access

Using the credentials obtained during enumeration, we attempted SSH authentication and successfully gained access to the machine: <br><br> <img width="759" height="454" alt="image" src="https://github.com/user-attachments/assets/b15fa2ba-d3a9-48e5-9dbe-d43b80365bb3" /> <br><br>

## User Flag

After obtaining initial access, we returned to the `/home` directory to continue enumerating the system.

During the analysis, we identified the user `user`. Upon accessing the user's directory, we found the user flag: <br><br> <img width="511" height="192" alt="image" src="https://github.com/user-attachments/assets/8a783a15-f3ff-42b6-9c0d-6c1eb396c1b3" /> <br><br>

```text
flag{25f1309497a18888dde5222761ea88e4}
```

## Conclusion

This machine demonstrated the importance of thorough enumeration. Through a simple service scan and the analysis of a web application exposed on a non-standard port, it was possible to obtain valid credentials, gain SSH access, and capture the user flag.

## Remediation

To prevent this type of compromise in real-world environments, several security measures should be implemented:

* **Do not store credentials in publicly accessible files**, web pages, or directories without proper protection.
* **Restrict access to services exposed on non-standard ports**, ensuring that only authorized users can access them.
* **Apply the principle of least privilege**, limiting user access to only the resources necessary for their roles.
* **Use strong and unique passwords**, avoiding credential reuse across different services.
* **Implement Multi-Factor Authentication (MFA)** whenever possible, especially for remote access services such as SSH.
* **Perform regular security audits** to identify sensitive information exposed in web applications and systems.
* **Monitor access attempts and suspicious activity**, enabling early detection of potential compromises.
* **Keep systems and services up to date**, reducing the attack surface and mitigating known vulnerabilities.

The exposure of credentials was the primary attack vector in this machine. Adopting these security practices would significantly reduce the risk of unauthorized access to the environment.
