# Threat Monitoring with Security Information & Event Management (SIEM)

### Wazuh

* Free and Opensource platform used for threat detection, prevention and response.
* Typically used to protect networks, virualized environments, containers and cloud environments
* It is a SIEM used to
  * Collect, analyze, aggregate, index and analyze security related data
  * Allowing you to detect intrusions, attacks, vulnerabilities and malicious activity



### Wazuh Features

* Security Analysis
* Intrusion Detection
* Log Data Analysis
* File Integrity Monitoring
* Vulnerability Detection
* Incidence Response
* Cloud Security
* Container Security
* Regulatory Compliance



### Wazuh Components

#### 1. Wazuh Agent

Cross platform endpoint security agent installed on system/host you would like to monitor NOTE: Wazuh can also work on network devices where agent can't be installed. This works by getting these devices to send their logs.

#### 2. Wazuh Server

Analyzes and processes the data and matches against rule sets to identify indicators of compromise (IOC)

#### 3. Elastic Stack

Display and indexes the alerts generated by wazuh server and provides user with robust data visualization and analytics functionality

**ELK Stack**

It is combination of 3 open source projects

1. Elastic Search : search and analytics engine
2. Log Stash : server side data processing pipeline
3. Kibana : Lets user visualize data with charts and graphs



### Wazuh Working

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
