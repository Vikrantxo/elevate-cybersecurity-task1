# elevate-cybersecurity-task1
# Task 1: Local Network Port Scan

## Objective
The objective of this task was to learn how to discover open ports on devices in the local network to understand network exposure. This involves using network scanning tools to perform reconnaissance and identify potential security risks.

## Tools Used
* **Nmap:** Used for performing the port scan.

## Process
1.  **Network Identification:** First, I identified my local network range to define the scan target.
2.  **Scan Execution:** I executed a TCP SYN scan (`-sS`) as specified in the task instructions. This scan type required root privileges (`sudo`) because it creates raw network packets to check for open ports without completing a full TCP connection.
3.  **Output Redirection:** The command was run as `sudo nmap -sS 127.0.0.1 > scan_results.txt` to save the output directly to a file for analysis.
4.  **Analysis:** Finally, I analyzed the saved results to identify listening services and evaluate potential security vulnerabilities.

## Scan Results & Analysis
The scan was performed on `localhost` (127.0.0.1) and revealed the following four open TCP ports:

| Port       | State | Service         | Analysis                                                                                           |
| :--------- | :---- | :-------------- | :------------------------------------------------------------------------------------------------- |
| `3306/tcp` | open  | `mysql`         | This port is the default for the MySQL database service, indicating a database server is running. |
| `5000/tcp` | open  | `upnp`          | This port is commonly used for Universal Plug and Play, which allows for automatic device discovery. |
| `7000/tcp` | open  | `afs3-fileserver` | This port is associated with the Andrew File System, suggesting a distributed file service may be active.|
| `8021/tcp` | open  | `ftp-proxy`     | This port is commonly used for an FTP (File Transfer Protocol) proxy service.                 |

*Screenshot of the scan being executed:*
![Nmap Scan](./screenshot.png)

## Identified Security Risks
Based on the open ports found, the following potential security risks were identified:

* **MySQL (Port 3306):** An exposed database server is a high-value target. Risks include brute-force attacks on weak credentials, SQL injection vulnerabilities, and potential data theft if not properly firewalled and secured.
* **UPnP (Port 5000):** UPnP has known historical vulnerabilities that could allow an attacker on the local network to manipulate network configurations or pivot to other devices.
* **AFS File Server (Port 7000):** Any file server, if misconfigured, can lead to unauthorized file access, modification, or data leakage.
* **FTP Proxy (Port 8021):** FTP is an insecure protocol that transmits credentials in plaintext. An FTP proxy could be exploited or abused if not securely configured, posing a risk of credential theft.

## Key Learnings
This task provided practical experience in network reconnaissance. The key takeaway is that open ports are potential entry points for attackers, and it is crucial to understand what services are running on a network and to ensure they are properly secured, for example, by using a firewall to close unnecessary ports.
