
# Setup e CVE Lab - Weeks #2 and #3

## Identification 

- CVE-2022-26134 is a critical vulnerability in Atlassian Confluence Server and Data Center, where an Object-Graph Navigation Language (OGNL) injection allows an unauthenticated attacker to execute arbitrary code on a Confluence server or data center instance. 
- This vulnerability impacts all versions of Confluence Server and Data Center before the following fixed versions 7.4.17, 7.13.7, 7.14.3, 7.15.2, 7.16.4, 7.17.4, 7.18.1, and newer.


## Cataloging

- This vulnerability was published in 02/06/2022 and the last modified date for it is 30/06/2022.
- Discovered by Volexity after detecting exploitation in corporate environments.
- Severity level: 9.8 CRITICAL


## Exploit

- The OGNL injection vulnerability allows attackers to inject crafted OGNL expressions, bypassing validation and executing arbitrary commands on Confluence servers.
- Attackers can gain privilege escalation by bypassing authentication and executing commands as the Confluence server, compromising system security.
- This exploit enables remote code execution, allowing attackers to execute shell commands and potentially gain control of the vulnerable server.
- Once compromised, attackers can perform lateral movement within the network, scanning and targeting other internal systems through the Confluence server.


## Attacks

- Hackers used the vulnerability to install webshells, maintain control, and perform long-term exploitation on compromised servers.
- Attackers accessed the Confluence database, dumping user tables containing sensitive information such as usernames and emails.
- Exploited servers were used to install cryptomining malware, hijacking server resources for unauthorized cryptocurrency mining.
- Hackers altered web access logs to remove evidence of their activities, hindering forensic analysis and detection.

(Source:
https://www.volexity.com/blog/2022/06/02/zero-day-exploitation-of-atlassian-confluence/
https://www.trendmicro.com/en_us/research/22/i/atlassian-confluence-vulnerability-cve-2022-26134-abused-for-cryptocurrency-mining-other-malware.html)
