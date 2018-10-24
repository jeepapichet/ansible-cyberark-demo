# CyberArk Ansible Demo

Demonstrate how to use CyberArk to secure credentials for Ansible tasks.


## Prerequisites

* Target hosts credential are in the Vault
* To use AIM CP - Ansible controller server must have CyberArk Credential Provider installed and assigned appropriate ownership on target safes
* To use Conjur - Ansible controller server must have conjur identity with appropriate permisisons and Vault Synchronizer service running 
* To use CyberArk PSM SSH Proxy - PSMP server must be avaiable (obviously)  

## Installing

cyberarkpass is already included in Ansible Core

conjur plugin can be installed from Galaxy

```
$ ansible-galaxy install cyberark.conjur
```

## Running the tests

Sample inventory files are availble for different secret retrieval scenarios. The checkdisk.yml playbook just login to target machine and execute `df` and printout the result 

### 1. Using AIM Credential Provider

Ansible use cyberarkpassword lookup to fetch SSH Username/Password from AIM Credential Provider 

```
$ ansible-playbook -i inventory/hosts_aimcp checkdisk.yml
```

### 2. Using Conjur 

Ansible use conjur lookup to fetch SSH Username/Password for target hosts from Conjur REST API

```
$ ansible-playbook -i inventory/hosts_conjur checkdisk.yml
```

### 3. Using PSMP + AIM Credential Provider 

Ansible retrieve Vault username and password from AIM Credential Provider and then use that  Vault credential to connect to target hosts via PSM SSH Proxy

```
$ ansible-playbook -i inventory/hosts_psmp_aimcp checkdisk.yml
```

### 4. Using PSMP + Conjur 

Ansible retrieve Vault username and password from Conjur REST API and then use that Vault credential to connect to target hosts via PSM SSH Proxy

```
$ ansible-playbook -i inventory/hosts_psmp_conjur checkdisk.yml
```
