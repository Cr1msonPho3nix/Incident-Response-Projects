# Scenario
You are a security analyst at a financial services company. You receive an alert that an employee received a phishing email in their inbox. You review the alert and identify a suspicious domain name contained in the email's body:
- signin.office365x24.com
You need to determine whether any other employees have received phishing emails containing this domain and whether they have visited the domain. You will use Chronicle to investigate this domain by using Chronicle.
## 1. Perform a search of the suspicious domain
![1.1.Chronicle.domain.search](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
The following information can be seen after performing the domain search:
- VT CONTEXT: This provides information available for the domain from the web "VirusTotal", consisting in the tabs "Detection", "IoCs (Indicators of comprimise)", "Graph" and "Atribution".<br><br>
![1.2.Chronicle.domain.search.VT](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
- WHOIS: This is a section providing information about the domain using a publicly available directory called "WHOIS".<br><br>
![1.3.Chronicle.domain.search.WHOIS](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
- Prevalence: This provides a graph that gives historical information about the domain. Can be helpful to determine whether the domain has been accessed previously.<br><br>
![1.4.Chronicle.domain.search.Prevalence](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
- RESOLVED IPS: This card provides information about the IP from the domain, which is "40.100.174.34". Clicking the IP will search that IP address.<br><br>
![1.5.Chronicle.domain.search.Resolved_IPS](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
- TIMELINE: This tab gives us information about interactions with the domain we searched. Any event will be found here, like "GET" and "POST" requests.<br><br>
![1.6.Chronicle.domain.search.TIMELINE](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
- ASSETS: This tab gives us information about Assets, like physical pcs or hosts, that have accessed the domain.<br><br>
![1.7.Chronicle.domain.search.ASSETS](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
## 2. Is the domain secure with the information given by VT CONTEXT?
We can assume that, with a 12/94 score in VT and a lot of security vendors flagging the domain as malicious, that this domain may NOT be secure at all.

## 3. Which IP is related to this domain? And what information can we get from it?
- In the card "RESOLVED IPS" we can see, as presented before, that the ip "40.100.174.34" is related to this domain. Upon clicking on it we can see that this IP is related to 2 domains:
  - "signin.office365x24.com": The domain we initially found.
  - "signin.accounts-gooqle.com": Another domain we just discovered, possibly fraudulent due to the misspelling on "gooqle", with a Q insted of a G.<br><br>
![3.1.Chronicle.domain.IP_Domains](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>
- We can also see that more Assets got connected, possibly, through the second domain "signin.accounts-gooqle.com".<br><br>
![3.2.Chronicle.domain.IP_Assets](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>