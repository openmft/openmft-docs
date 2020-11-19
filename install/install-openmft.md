# 3.4 Integrate OpenMFT with IBM SFG \(Sterling File Gateway\)

## 3.4.1 OpenMFT can be natively integrated with IBM SFG.

These are the dependencies for OpenMFT to be installed and integrated with IBM SFG:

* PostgreSQL DB as mentioned in the [pre-requisites section](pre-requisites.md)
* 
OpenMFT integrates with IBM Sterling B2B Integrator / Sterling File Gateway and relies on the following components to work:

* OpenMFT Services
* SFG

OpenMFT can be installed in the same server as SFG for development or testing purposes, but can also be configured as a cluster where each component could be split. 

```text
# These are all the options for install, one can pick and choose which 
# components to install, but dbschema & vault are one time tasks for the 
# entire cluster if a multi-node cluster is being provisioned with 
# ui, svc & sfg separately.
./om -install [dbschema,vault,certs,svc,ui,sfg]
```

### 3.3.1.1 All in one install \(Single node install mode\)

{% hint style="info" %}
The below command is run with an "all" flag if one wants to run OpenMFT and all its dependencies in the same server as SFG.
{% endhint %}

```text
./om -install all
```

```text
# Optionally, one could also install in verbose mode
./om -install all -verbose
```

The **following tasks are done automatically** when "all" is used with -install:

* stage openmft folder
* move "om" binary to openmft/bin/om
* Create a symbolic link "openmft" to "openmft/bin/om"
* import the DB schema from openmft\_schema.sql into PostgreSQL database that was created in the "Pre-requisites" section
* install, init, start, unseal, & configure Vault
* create **default administrator** Admin User/password of **admin/password**
* start UI
* start registration, workflow and communication services
* import default workflows that are needed to onboard Sterling File Gateway Traditional Mailboxes and communication profiles like SFTP & Connect:Direct.

### 3.3.1.2 OpenMFT UI and SFG \(Optional for 2nd node and higher\)

{% hint style="info" %}
This option is usually used when we are installing UI alongside SFG in the 2nd node onwards in a multi-node cluster.  **DATABASE Schema provisioning and VAULT are one time tasks and must be skipped from 2nd node onwards in a cluster, but the VAULT\_TOKEN should be copied to openmft.conf from the 1st node or the vault node.** 
{% endhint %}

```text
./om -install ui,svc,sfg
```

### 3.3.1.3 OpenMFT UI only \(Optional for 2nd node and higher\)

{% hint style="info" %}
If UI is being installed in its own cluster of servers outside of SFG, then ui option could be used to install.
{% endhint %}

```text
./om -install ui
```

### 3.3.1.4 SFG dependencies only \(Optional for SFG 2nd node and higher\)

```text
./om -install svc,sfg
```

