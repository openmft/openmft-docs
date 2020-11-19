# 3.2 Download & stage OpenMFT

## 3.2.1 Create a base path

In our example, we created /apps, but you can create any folder under your user account where you have at least 10 GB or more.  Update .bash\_profile with OPENMFT\_BASE variable for basepath and add $OPENMFT\_BASE/openmft/bin to PATH:

```text
export OPENMFT_BASE=/apps
export PATH=$PATH:$OPENMFT_BASE/openmft/bin
```

Activate the bash\_profile:

```text
source ~/.bash_profile
```

## 3.2.2 Getting Super Powers starts with downloading amazing software

Becoming a super hero is a fairly straight forward process.  Start by downloading below files into the base path.  You can either click on these links:

* [https://s3.amazonaws.com/s3.openmft.org/om](https://s3.amazonaws.com/s3.openmft.org/om)
* [https://s3.amazonaws.com/s3.openmft.org/openmft\_schema.sql](https://s3.amazonaws.com/s3.openmft.org/openmft_schema.sql)
* [https://s3.amazonaws.com/s3.openmft.org/openmft\_template.conf](https://s3.amazonaws.com/s3.openmft.org/openmft_template.conf)

If the software is downloaded using the links above to either a Windows or a Mac, the files could be transferred to the target Linux server using SFTP. 

OR directly download them from command line using wget on Linux:

```text
cd /apps/
wget https://s3.amazonaws.com/s3.openmft.org/om
wget https://s3.amazonaws.com/s3.openmft.org/openmft_schema.sql
wget https://s3.amazonaws.com/s3.openmft.org/openmft_template.conf
```



##  3.2.3 Copy openmft\_template.conf to openmft.conf and update it

Copy openmft\_template.conf file or rename it to openmft.conf:

```text
cp openmft_template.conf openmft.conf
```

Below is an example of openmft.conf.  Update the following properties per site settings:

* basepath
* Favicon, Logo and Copyright if you want to customize the branding 
* log file settings if logs need to go a specific folder
* DATABASE section is meant for the OpenMFT Database.  
  * dburl -&gt; User, pwd, host, port \(default=5432\) & database values have to be updated in this format: "postgres://user:pwd@host:port/database?sslmode=disable" 
* SFG section is where SFG\_HOME \(base\) directory and other SFG related details are configured
* VAULT\_HOME will be created when OpenMFT is installed and address in VAULT\_ADDR may need to be changed to  your host name.

 

```
[DEFAULT]
basepath=/apps # Example path, change to your base path

[RESOURCES]
FAVICON=resources/img/favicon.png
LOGO=resources/img/openmft_logo.png
COPYRIGHT="© 2020 https://docs.openmft.org"
OPENMFT_SSL_CERT=certs/server.crt
OPENMFT_SSL_KEY=certs/server.key

[LOG]
log_file=openmft_installation.log
log_file_run=openmft_run.log
log_file_setup=openmft_setup.log
log_level=INFO
backup_count=5

[DATABASE]
schema = "openmft_schema.sql"
DBTYPE = postgres
DBNAME = openmft
HOST = localhost
PORT = 5432
USERNAME = openmftuser
PASSWD = OpenMFT2020
SSLMODE = disable

[SSL_CERTIFICATE]
create_self_signed=yes
hosts=127.0.0.1,dev.openmft.org
cert_file=
key_file=

[SFTPD_SERVICE]
LISTEN_ADDRESS=127.0.0.1:55022

[SFG]
USE_SFG=false # Change to true if you have SFG
SFG_HOME=/ibm/sfg # Example path, change this to your SFG Base path
COMMUNITY_NAME = OPENMFT_COMM 
SFG_API_BASE_URL = http://localhost:40074 # Change the host and port accordingly
SFG_API_USER = api_user # api_user needs to exist in SFG with APIUSER permissions
SFG_API_PASSWD = j6eiUroCMDe7CuqMozef # This is a sample password for the api_user
NETMAP_NAME = OPENMFT_SFG_NETMAP
# Below are SFG objects that will be configured during install if set to yes
INSTALL_SFTP_ADAPTER = no # If it is a brand new SFG and you need SFTP adapter setup, set it to yes
INSTALL_CD_ADAPTER = no # If it is a brand new SFG and you need CDSA adapter setup, set it to yes
INSTALL_BUSINESS_PROCESS = yes
INSTALL_SCHEDULER = yes
INSTALL_AMFSERVICE = yes
#Please change accordingly your environment
SFG_HOST=localhost
SFTP_PORT=40039
USECASE_HTTP_ADAPTER_PORT=40449

[VAULT]
VAULT_HOME=/apps/openmft/vault  # Change apps to your basepath
VAULT_ADDR=http://localhost:8200
```

## 3.2.4 Change permissions to execute for OpenMFT Distro \(om\):

```text
chmod +x om
```







