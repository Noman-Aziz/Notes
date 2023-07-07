# Intrusion Detection Systems (IDS)

### Snort

It is a free and open source IDS/IPS used to perform network traffic analysis, content matching to detect and prevent various attacks based on **predefined rules**.



#### Operational Modes

Snort has 3 main operational modes

**1. Packet Sniffing**

Collects and displays network traffic like wireshark does

**2. Packet Logging**

Collects and Logs network traffic in a file

**3. Network Intrusion Detection**

Analyze packets and matches traffic **against signatures**



#### Snort Rules

They are similar to typical firewall rules, they are used to detect network traffic against specific patterns or signatures and consequently make a decision whether to send an alert or drop the traffic (in IPS case). There are 3 types of snort rules

**1. Community Rules**

Free rules created by snort community

**2. Registered Rules**

Free rules created by Talos. Registered account is required to use them.

**3. Subscription Only Rules**

They require an active paid subscription in order to be accessed and used



#### Snort Rule Syntax

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

#### Automated Rule Generator (Snorpy)

Snorpy (http://www.cyb3rs3c.net/) can be used to generate rules easily for snorp



#### Snort IDS Network Placement

<figure><img src="../../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Snort Versions

**1. Snort 2.X**

De facto version of snort which means that is typically deployed and most widely implemented and has the most rules

**2. Snort 3.0**

Latest version that has improved efficiency, performance, scalability and usability over Snort 2.X



### Suricata

It is also free and open source threat detection engine. It combines IDS, IPS and network security monitoring

#### Operational Modes

1. Active (IPS)
2. Passive (IDS)

#### Working

Exactly similar to how snort works

#### Integrating Wazuh with Suricata for Log Processing

Install Wazuh Agent on Suricata Server and edit the configuration file on both agent machine and wazuh dashboard to include `/var/log/suricata/eve.json` file [Reference](https://www.youtube.com/watch?v=NB\_u9m-MMcY\&list=PLBf0hzazHTGNcIS\_dHjM2NgNUFMW1EZFx\&index=16)

