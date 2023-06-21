# Ansible

### Intro

It is a operations tool that provides

1. IT automation
2. Configuration management
3. Automatic deployment

***

### Push/Pull Architecture

#### Pull Architecture

* Nodes check with the server periodically and fetch the configurations from it
* Examples are **Chef** & **Puppet**
* Requires clients to be installed on the nodes i.e Master/Slave architecture

#### Push Architecture

* Server pushes configuration via ansible modules (small programs) to the nodes
* **Ansible** uses the push architecture
* It uses agentless approach since it uses SSH to deploy the configuration on the nodes
* We can also use custom authentication protocols like **Kerberos** via plugins

***

### Ansible Architecture

* Have a Local Machine where Ansible is installed
* Nodes are the systems to be configured. They are controlled by the local machine
* Module is collection of configuration files
  * These config files are called [playbooks](1.-playbooks.md)
* [Inventory](3.-inventory.md) is a document that groups the nodes under specific labels

<figure><img src="../../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>
