# Infrastructure as a Code (IaC)

### Categories

1. Ad hoc scripts
   * Shell script that makes calls to like AWS to provison 5 EC2 machines
2. Configuration management tools
   * Used on premis to manage config of servers
   * Ansible, puppet and chef are examples
3. Server Templating tools
   * Used for building out a template will be provisioned on a server
   * Examples are Amazon AMI
4. Orchestration tools
   * Kubernetes is an example
5. Provisioning tools
   * Used to provision cloud resources



### Declarative vs Imperative

#### Declarative

* We define end state of what we want
* Tool manages what API calls need to be made and it makes that happen

#### Imperative

* We tell system what we want to happen and the **sequence** in which we want to happen



### Cloud Specific vs Cloud Agnostic

#### Cloud Specific

* Examples are AWS Cloud Formation, Azure Resource Manager, Coogle Cloud Deployment Manager which focuses on particular cloud

#### Cloud Agnotic

* It does not focus on a simple platform. It is generic in nature
* Examples are Terraform and Pulumi



### Common Patterns

#### Provisioning + Config Management

We can use terraform with ansible, chef or puppet that will allow us to for instance setup a particular service once EC2 machine is deployed

#### Provisioning + Server Templating

Terraform can also be used with hashicorp packer which package the image and can be used later as an AMI

#### Provisioning + Orchestration

Terraform can be used with kubernetes cluster. Terraform is used to deploy cloud resources and k8 will be used to deploy the applications managed onto that cloud resource

