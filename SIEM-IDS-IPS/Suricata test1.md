# Scenario
You’re a security analyst who must monitor traffic on your employer's network. You’ll be required to configure Suricata and use it to trigger alerts.
- First, you'll explore custom rules in Suricata.
- Second, you'll run Suricata with a custom rule in order to trigger it, and examine the output logs in the fast.log file.
- Finally, you’ll examine the additional output that Suricata generates in the standard eve.json log file.
## Definition of files used
- The sample.pcap file is a packet capture file that contains an example of network traffic data, which you’ll use to test the Suricata rules. This will allow you to simulate and repeat the exercise of monitoring network traffic.
- The custom.rules file contains a custom rule when the lab activity starts. You’ll add rules to this file and run them against the network traffic data in the sample.pcap file.
- The fast.log file will contain the alerts that Suricata generates. The fast.log file is empty when the lab starts. Each time you test a rule, or set of rules, against the sample network traffic data, Suricata adds a new alert line to the fast.log file when all the conditions in any of the rules are met. The fast.log file can be located in the /var/log/suricata directory after Suricata runs.The fast.log file is considered to be a depreciated format and is not recommended for incident response or threat hunting tasks but can be used to perform quick checks or tasks related to quality assurance.
- The eve.json file is the main, standard, and default log for events generated by Suricata. It contains detailed information about alerts triggered, as well as other network telemetry events, in JSON format. The eve.json file is generated when Suricate runs, and can also be located in the /var/log/suricata directory.
When you create a new rule, you'll need to test the rule to confirm whether or not it worked as expected. You can use the fast.log file to quickly compare the number of alerts generated each time you run Suricata to test a signature against the sample.pcap file.
## 1. Examine a custom rule in Suricata
![1.1.Suricata_custom_rule](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/1.1.Suricata_folder.PNG)<br><br>

We used the "cat custom.rules" command that returns that output in the shell. We can check each component in detail:
- "alert" is the action taken by this rule. Most common actions are alter, drop, pass and reject.
- "http $HOME_NET any -> $EXTERNAL_NET any" is the header of the rule, which defines the rules about network traffic, in this case any connection from the "HOME_NET" to any external site.
- "(msg:"GET on wire"; flow:established,to_server; content:"GET"; http_method; sid:12345; rev:3;)" is the final part of the signature, and are a bunch of rule options that allows a better customizable signature.

## 2. Trigger a custom rule in Suricata
- 1: List the files in the suricata folder:<br><br>
![2.1.Suricata_folder](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/2.1.Suricata_files_0.PNG)<br><br>
No files where found on the suricata directory prior to execute it.

- Run suricata using the custom.rules and sample.pcap files:<br><br>
![2.2.Suricata_run](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/2.2.Suricata_running_1.PNG)<br><br>

The options used in the command are:
- "-r sample.pcap" specifies an input file to mimic network traffic.
- "-S custom.rules" instructs Suricata to use the rules defined in the custom.rules file.
- "-k none" instructs Suricata to disable all checksum checks. Checksums are a way to detect if a packet has been modified in transit.

Now List the files generated by Suricata:<br><br>
![2.3.Suricata_files_1](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/2.3.Suricata_files_1.PNG)<br><br>

Checking the "fast.log" file we can see some information generated by Suricata when it processes a packet that meets the conditions on an alter generating rule.

Now check the eve.json output:<br><br>
![2.4.Suricata_evefile_raw](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/2.4.Suricata_evefile_raw.PNG)<br><br>

This opens the raw content of the file, using the jq command displays the entries in an improved format:<br><br>
![2.5.Suricata_evefile_jq](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/2.5.Suricata_evefile_jq.PNG)<br><br>

You can even extract specific event data from the "eve.json" file by specifying fields:<br><br>
![2.6.Suricata_evefile_jq_fields](https://github.com/Cr1msonPho3nix/Incident-Response-Projects/blob/main/img/Suricatatest1/2.6.Suricata_evefile_jq_fields.PNG)<br><br>