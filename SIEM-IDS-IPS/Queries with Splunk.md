# Scenario
You are a security analyst working at the e-commerce store Buttercup Games. You've been tasked with identifying whether there are any possible security issues with the mail server. To do so, you must explore any failed SSH logins for the root account.
## 1. Search all the information in index
- Check all the data from "index":<br><br>
![1.1.SPLUNK.alltime.index](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/1.1.SPLUNK.alltime.index.PNG)<br><br>

Entering the query 'index="main"' and selecting 'All Time' from the time range gives us all the events accross all time
## 2. How many networks exists within the information received?
![1.1.SPLUNK.alltime.index](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/2.1.SPLUNK.hosts.PNG)<br><br>

With the information gathered looking for all logs, we can see there are 5 values as hosts:
- 'vendor_sales' seems to be related to the information about the company sales.
- 'mailsv' is related to the company's mail server.
- Hosts 'www1','www2' and 'www3' are related to company's applications each.
## 3. How many failed attempts logs were collected in the mail host due to failed passwords?
![3.1.SPLUNK.failedpassword](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Queries_SPLUNK_1/3.1.SPLUNK.failedpassword.PNG)<br><br>

Has we can see in the image, 8154 events were registered as a "failed password" in the mail host, through the narrowed search 'index=* host="mailsv" failed password'.