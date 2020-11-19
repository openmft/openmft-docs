# 3.4 Integrate OpenMFT with IBM SFG \(Sterling File Gateway\)

## 3.4.1 OpenMFT can be natively integrated with IBM SFG.

These are the dependencies for OpenMFT to be installed and integrated with IBM SFG:

* PostgreSQL DB as mentioned in the [pre-requisites section](pre-requisites.md)

```text
USE_SFG=true # This is part of the [SFG] section in openmft.conf and is required to install the necessary components and integrate with sfg
```

OpenMFT integrates with IBM Sterling B2B Integrator / Sterling File Gateway and enables the following functionality without having to write any BPs:

* Easier on-boarding
* Transactional processing
* Persistent and Guaranteed delivery even if the end-points are down temporarily for a few hours or the entire weekend
* Integration with AWS S3, GCP Storage, etc

OpenMFT can be installed in the same server as SFG for development or testing purposes, but can also be configured as a cluster where each component could be split. 

```text
# These are all the options for install, one can pick and choose which 
# components to install, but dbschema & vault are one time tasks for the 
# entire cluster if a multi-node cluster is being provisioned with 
# ui, certs svc & sfg separately.
./om -install [dbschema,vault,certs,svc,ui,sfg]
```

### 3.4.1.1 All in one install \(Single node install mode\)

```text
./om -install dbschema,vault,certs,svc,ui,sfg
```

### 3.4.1.2 OpenMFT UI and SFG \(Optional for 2nd node and higher\)

{% hint style="info" %}
This option is usually used when we are installing UI alongside SFG in the 2nd node onwards in a multi-node cluster.  **DATABASE Schema provisioning and VAULT are one time tasks and must be skipped from 2nd node onwards in a cluster, but the VAULT\_TOKEN should be copied to openmft.conf from the 1st node or the vault node.** 
{% endhint %}

```text
./om -install ui,certs,svc,sfg
```

### 3.4.1.3 OpenMFT UI only \(Optional for 2nd node and higher\)

{% hint style="info" %}
If UI is being installed in its own cluster of servers outside of SFG, then ui option could be used to install.
{% endhint %}

```text
./om -install ui, certs
```

### 3.4.1.4 SFG dependencies only \(Optional for SFG 2nd node and higher\)

```text
./om -install svc,sfg
```

## 3.4.2 Install Demo use cases

Please refer to the [Install Demo documentation](3.3-install-openmft-as-a-standalone-server.md#3-3-2-install-demo-use-cases) to install demo use cases by the industry. 

## 3.4.3 Run Demo use cases

Please refer to the [Run Demo documentation](3.3-install-openmft-as-a-standalone-server.md#3-3-3-run-demos) to run the demo use cases by the industry

