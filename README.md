Couchbase on HP Cloud Services
==============================

This page covers the instructions of installing a single node
Couchbase Server on the HP Cloud Services (HPCS) compute
infrastructure.

The steps...

Add a Security Group
--------------------

Create a new Security Group for demo purposes...

* Example Name: "couchbase demo".
* Example Description: "ports opened for remote couchbase access for demos; not for production usage".

Add Rules...

    IP Protocol / From Port / To Port / Type / CDIR IPS  / Group / Comments
    tcp         / 22        / 22      / IPs  / 0.0.0.0/0 /       / for ssh
    tcp         / 8091      / 8091    / IPs  / 0.0.0.0/0 /       / for HTTP/REST access
    tcp         / 11211     / 11211   / IPs  / 0.0.0.0/0 /       / for memcached ascii protocol access

Don't forget to 'Save Changes'.

Create a Server
---------------

For example...

* Flavor: "standard.large - 4 cCPU / 8GB RAM / 240 GB HD"
* Security Group: "couchbase demo" (the Security Group you previously created
* Install Image: "Linux" / "CentOS 5.8 Server 64-bit ..."

Be patient as the Server launch might take a few minutes.

SSH into the Server
-------------------

For example, if the Server launched with a public address of 15.185.113.205, then...

    $ ssh -i $YOUR_SSH_KEY root@15.185.13.205

Install Couchbase Server
------------------------

You can get the latest Couchbase Server software packages from...

    http://www.couchbase.com/download

For example, we'll use...

    http://packages.couchbase.com/releases/2.2.0/couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm

In your SSH session, use...

    $ wget http://packages.couchbase.com/releases/2.2.0/couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm
    $ rpm -i couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm

Here's an example...

    [root@test0 tmp]# wget http://packages.couchbase.com/releases/2.2.0/couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm
    --2013-10-19 01:38:06--  http://packages.couchbase.com/releases/2.2.0/couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm
    Resolving packages.couchbase.com... 176.32.100.65
    Connecting to packages.couchbase.com|176.32.100.65|:80... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 130662856 (125M) [application/x-redhat-package-manager]
    Saving to: `couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm'
    
    100%[============================================================================================================================>] 130,662,856 3.32M/s   in 38s
    
    2013-10-19 01:38:44 (3.32 MB/s) - `couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm' saved [130662856/130662856]
    
    [root@test0 tmp]# rpm -i couchbase-server-enterprise_2.2.0_x86_64_openssl098.rpm
    Minimum RAM required  : 4 GB
    System RAM configured : 8181668 kB
    
    Minimum number of processors required : 4 cores
    Number of processors on the system    : 4 cores
    
    Starting couchbase-server[  OK  ]
    
    You have successfully installed Couchbase Server.
    Please browse to http://test0:8091/ to configure your server.
    Please refer to http://couchbase.com for additional resources.
    
    Please note that you have to update your firewall configuration to
    allow connections to the following ports: 11211, 11210, 11209, 4369,
    8091, 8092 and from 21100 to 21299.
    
    By using this software you agree to the End User License Agreement.
    See /opt/couchbase/LICENSE.txt.

Configure Your Couchbase Server
-------------------------------

Point your web browser at...

    http://PUBLIC_IP:8091

For example...

    http://15.185.113.205:8091

And follow the steps in the web-based setup screens to complete your
Couchbase Server configuration.

If you configured a "default" bucket (recommended, especially for
demos), you can use memcachetest to put a test workload on your
Couchbase Server, using...

    $ /opt/couchbase/bin/memcachetest -l

There are lots of useful monitoring graphs in the Couchbase Server web
U/I.  Be sure to check them out.
