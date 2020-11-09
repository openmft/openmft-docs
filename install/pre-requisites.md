---
description: These are the dependencies for OpenMFT to be installed.
---

# 3.1 Pre-requisites

## 3.1.1 OS -&gt; Linux  \(Prefer Redhat or CentOS 7.x\)

OpenMFT has been tested on Redhat and CentOS, but it should work in any Linux operating system.

If anybody is interested to have OpenMFT in Windows, we can build a windows version.  Please do reach out to us at support@openmft.org.



## 3.1.2 Python 3.x \(Prefer Anaconda Python\)



> You can download and install anaconda either from the link below or by copying and pasting the wget command in your Linux environment: [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual)

{% hint style="info" %}
Use regular service account to install Anaconda Python.  Don't use root.  
{% endhint %}



```
wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
```

Add python to PATH in ~/.bash\_profile as shown below and activate the updated profile:

```text
export PATH=/apps/anaconda3/bin:$PATH
```

```text
source ~/.bash_profile
```

Once Python is installed, type the below command line to install PostgreSQL related libraries

```text
pip install psycopg2-binary
```

## 3.1.3 PostgreSQL

This URL should help you to get PostgreSQL server installed on Redhat:  [https://www.postgresql.org/download/linux/redhat/](https://www.postgresql.org/download/linux/redhat/).

For your convenience, the commands to install PostgreSQL are pasted below and should help one to install PostgreSQL and start it up.  One needs to be logged in as root to install PostgreSQL. 

{% hint style="info" %}
PostgreSQL is the only dependency that requires root access to setup OpenMFT.
{% endhint %}

```text
sudo su -
yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
yum install -y postgresql12-server
/usr/pgsql-12/bin/postgresql-12-setup initdb
systemctl enable postgresql-12
systemctl start postgresql-12
```

The below commands should help you to create a database, user, grant database access to the user.  The below commands are just examples, you can name your database anything you like and give any password you prefer \(Only copy commands after the $ and \# symbols, prefixes shown below are part of CLI\):

```text
sudo su - postgres

psql
create user openmftuser password 'OpenMFT2020';
create database openmft;
grant all on database openmft to openmftuser;
\q
```

Give permissions for the user to the public schema created inside the database:

```text
psql openmft
grant all privileges on all tables in schema public to openmftuser;
\q
```



Update postgres settings to trust 127.0.0.1 and your listen address if accessing remotely, by editing pg\_hba.conf file:

```text
cd /var/lib/pgsql/12/data
```

Update pg\_hba.conf in the "local all all peer" section with the below lines.\(Change the value from ident to trust\)

```text
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
host    all             all             localhost               trust
```

Update postgresql.conf with listen\_addresses = "\*" if postgres needs to be accessed remotely:

```text
listen_addresses = '*'
```

Exit from postgres account with "exit" or Ctrl+d:

```text
exit
```

Restart PostgreSQL:

```text
sudo su -
systemctl restart postgresql-12
```

Exit from root account with "exit" or Ctrl+d:

```text
exit
```







