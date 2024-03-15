<h1>Hackathon</h1>

<h2>Description</h2>
Scnning and Addressing the vulnerabilities comprised by the OWASP Top Ten (Top 10 Web Application Security Risks) and provide detailed solutions with complete guidelines on how to 
address each of the vulnerabilities comprised by such checklist. 


The application was created from a fork of the famous OWASP Juice Shop, and it’s currently 
deployed to a cloud platform (Azure) using Virtual Machines (VMs) that are exposed directly on the 
internet with public addresses with no protection mechanisms to support its operation at all.

<br />


<h2>A02:2021-Cryptographic failures:</h2>

- <b>Problem: 

Cryptographic failures pose significant risks to data security and privacy. Various actors, including hackers, malicious insiders, and state-sponsored entities, can exploit vulnerabilities in cryptographic systems. Technical constraints such as weak encryption algorithms, flawed implementations and insufficient key management can also contribute to cryptographic failures. Additionally, technology constraints such as hardware limitations and compatibility issues can impede the effectiveness of cryptographic solutions.

</b> 

<h2> </h2>



<h2></h2>

<p align="center">
Scan with Snyk, Use of Weak HASH Detected: <br/>
<img src="https://i.imgur.com/AT5bdmH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

 Solutions:
Adoption of Strong Cryptographic Algorithms: Ensure that the cryptographic algorithms used in the system are strong and resistant to known attacks as well as regularly update cryptographic protocols and algorithms to stay ahead of emerging threats.<br />
<br />

Scan with Snyk, Use of a Broken or Risky Cryptography Algorighm Detected:  <br/>
<img src="https://i.imgur.com/5wkB4Ov.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

According to snyk overview in the above screenshot:jsonwebtoken is a JSON Web Token implementation (symmetric and asymmetric)
Affected versions of this package are vulnerable to Use of a Broken or Risky Cryptographic Algorithm such that the library can be misconfigured to use legacy, insecure key types for signature verification. For example, DSA keys could be used with the RS256 algorithm.
<br />
<br />

Scan with Snyk: <br/>
<img src="https://i.imgur.com/XQgGOwo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The above screenshot shows another cryptographic failure. According to the scan done with the snyk, it reveals that  when constants are hardcoded into applications, this information could easily be reverse-engineered and become known to attackers. For example, if a breached authentication token is hardcoded in multiple places in the application, it may lead to components of the application remaining vulnerable if not all instances are changed. Another negative effect of hard-coding constants is potential unpredictability in the application's performance if the development team fails to update every single instance of the hardcoded constant throughout the code. For these reasons, hard-coding security-relevant constants is considered bad coding practice and should be remedied if present and avoided in future.

Best practices, Never hard code security-related constants; use symbolic names or configuration lookup files.
As hard coding is often done by coders working alone on a small scale, examine all legacy code components and test carefully when scaling.
Adopt a "future-proof code" mindset: While use of constants may save a little time now and make development simpler in the short term, it could cost time and money adapting to scale or other unforeseen circumstances (such as new hardware) in the future.
<br />
<br />
Scan with Snyk:  <br/>
<img src="https://i.imgur.com/T9dbqTP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Details of the screenshot above:The above scan with snyk explained that developers may use hardcoded credentials for convenience when coding in order to simplify their workflow. While they are responsible for removing these before production, occasionally this task may fall through the cracks. This also becomes a maintenance challenge when credentials are re-used across multiple applications.
Once attackers gain access, they may take advantage of privilege level to remove or alter data, take down a site or app, or hold any of the above for ransom. The risk across multiple similar projects is even greater. If code containing the credentials is reused across multiple projects, they will all be compromised.

Best practices for prevention Plan software architecture such that keys and passwords are always stored outside the code, wherever possible.
Plan encryption into software architecture for all credential information and ensure proper handling of keys, credentials, and passwords.
Prompt for a secure password on first login rather than hard-code a default password.
If a hardcoded password or credential must be used, limit its use, for example, to system console users rather than via the network.
Use strong hashes for inbound password authentication, ideally with randomly assigned salts to increase the difficulty level in case of brute-force attack.
<br />

A10:2021 – Server-Side Request Forgery (SSRF)<br />

Server-Side Request Forgery (SSRF) is a security vulnerability that occurs when an attacker is able to trick a server into making an unintended HTTP request to a resource controlled by the attacker.

Scan with Snyk:  <br/>
<img src="https://i.imgur.com/m3RJFCG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

According to snyk overview in the above screenshot: request is a simplified http request client.
Affected versions of this package are vulnerable to Server-side Request Forgery (SSRF) due to insufficient checks in the lib/redirect.js file by allowing insecure redirects in the default configuration, via an attacker-controller server that does a cross-protocol redirect (HTTP to HTTPS, or HTTPS to HTTP).
<br />
<br />

Scan with Snyk:  <br/>
<img src="https://i.imgur.com/510uPhe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The above screenshot shows another server-side request forgery vulnerability. According to the scan done with the snyk, it reveals that in a server-side request forgery attack, a malicious user supplies a URL (an external URL or a network IP address such as 127.0.0.1) to the application's back end. The server then accesses the URL and shares its results, which may include sensitive information such as AWS metadata, internal configuration information, or database contents with the attacker. Because the request comes from the back end, it bypasses access controls, potentially exposing information the user does not have sufficient privileges to receive. The attacker can then exploit this information to gain access, modify the web application, or demand a ransom payment.

Best practices for prevention Blacklists are problematic and attackers have numerous ways to bypass them; ideally, use a whitelist of all permitted domains and IP addresses.
Use authentication even within your own network to prevent exploitation of server-side requests.
Implement zero trust and sanitise and validate all URL and header data returning to the server from the user. Strip invalid or suspect characters, then inspect to be certain it contains a valid and expected value.
Ideally, avoid sending server requests based on user-provided data altogether.
Ensure that you are not sending raw response bodies from the server directly to the client. Only deliver expected responses.
Disable suspect and exploitable URL schemas. Common culprits include obscure and little-used schemas such as file://, dict://, ftp://, and gopher://.
<br />
<br />
Scan with Snyk:  <br/>
<img src="https://i.imgur.com/Atk1gWp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The above screenshot shows that the inputs are not properly validated or sanitised as the header accepts URLs which allows bypassing subsequent filters.
In any application or code, the user input for making HTTP requests such as fields, parameters, or headers should not accept URLs or hostnames to prevent SSRF vulnerability.
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
