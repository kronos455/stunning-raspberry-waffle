# Build a Raspberry Pi Cluster with Apache Hadoop

## Preface
This page explains how I put together the Raspberry Pi 3 Bramble. Because I didn't know any Linux command line when I first started, this 
recipe may sound condescendingly basic for anyone with basic Linux skills. However, I really want to keep the recipe as simple as possible to allow the most number of interested people to be able to replicate what I've done. 

I will assume that the reader can operate a computer or can ask a friend for help.

Let me know of any typos or anything else you feel this recipe is missing. This document might be a work-in-progress for a little while. I'm open to constructive criticism. I'll put some pics in as well at a later date. I realize that this page, as is, is as bland as toast.

## Components

- Raspberry PI 3 B's: I used 4. I've seen clusters built with as few as 2. The sky's the limit if you want to do more. I also refer to these as 'RP3B' because typing more than I have to seem inefficient. Sources: [Microcenter](http://www.microcenter.com/product/460968/Raspberry_Pi_3_Model_B), [Amazon](http://amzn.to/2oFOKu4)

- USB Power Source: I used a 5-port power source. Just make sure your power source is a minimum of 2.5 amps per port (the power source sold seperately for the RP3B is 5 amp). More on this later.  Sources: [Amazon](http://amzn.to/2ozrd1h)

- A router: I used a basic, 5-port router to start. It was cheap. Then I was invited present the cluster to some folks at the university I attend for my Master's and I needed a wireless to make the cluster remotely. It's up to you.  Sources: (wired) [Amazon](http://amzn.to/2oGa02T), (wireless) [Amazon](http://amzn.to/2oFQ5kF)

- 32 GB Micro SD cards: I had 4 Raspberry PI's so I bought 4 Micro SD Cards. You can go small or big on the disk volume, depending on your intended use, however, I would HIGHLY recommend Class 10 or above if possible. The higher the class, the faster the read & write speeds. I noticed that the Class 10's were significantly faster than the Class 4's I started out with. Sources: [Amazon](http://amzn.to/2oA7LBh)

- Micro USB cables: You'll need 4. I liked the flat ones. Makes it easy to aesthetically manage the cables.  Sources: [Amazon](http://amzn.to/2oznxwD)

- Ethernet Patch Cables: You'll need 4. These are flat, too.  Sources: [Amazon](http://amzn.to/2oFYCnW)

- Electrical Strip: Need one to plug in your power source and router. Out of caution, I bought one that had some surge protection and an accompanying guarantee. They are a little more expensive but they make you feel like you're protecting your newly acquired toy during a thunder-storm.  Sources: [Amazon](http://amzn.to/2ozuI7J)

- USB Fan: Just for fun.  Sources: [Amazon](http://amzn.to/2oFYHb2)

- Acrylic, Stacked Case: Gives a nice presentation of the cluster. Sources: [Amazon](http://amzn.to/2ozuIEN)

This is how I assembled the cluster. Feel free to get artistic. Just keep in mind that there are certain thing that you can't change - each RP3B absolutely needs 2.5 amps or more power, etc. And this isn't an endorsement of Amazon but they do make things easier.

## Citing Sources

I did not make this cluster in a vacuum. I don't have the technical background necessary to "wing it". However, with the right instruction just about anyone can get started and learn. I had no background in Linux so it took me about a month to get the cluster working the first time.

[Beginner Linux code](http://www.makeuseof.com/tag/15-useful-commands-every-raspberry-pi-user-should-know/)

Begin here for Hadoop: 

http://www.widriksson.com/raspberry-pi-hadoop-cluster/#The_setup

http://www.widriksson.com/raspberry-pi-2-hadoop-2-cluster/#Clear_HDFS_filesystem

http://arturmkrtchyan.com/how-to-setup-multi-node-hadoop-2-yarn-cluster

https://developer.ibm.com/recipes/tutorials/building-a-hadoop-cluster-with-raspberry-pi/

https://robcnamahoe.wordpress.com/2016/12/06/setting-up-hadoop-on-a-raspberry-pi-cluster/

All of these pages were useful in that they helped me put the pieces together to install Apache Hadoop 2.7.2. Maybe it was my inexperience at the time, but it felt as I wouldn't have been able to complete the project with only one of those pages alone. I had to piecemeal them together to get the recipe below.

I spent the most time with the page at http://www.widriksson.com/raspberry-pi-hadoop-cluster/#The_setup.

I have cut & paste snippets from these websites into this recipe to make it easier to write. Hopefully, the writers of those blogs don't mind me standing on the shoulders of giants.

# The Setup 

Download Raspbian [Jessie Lite](https://github.com/caiomsouza/raspberrypi/releases) (RP3B recommended OS) from Github user caiomsouza. This is an older release of Jessie but it worked well with this project. I would recommend enabling SSH & password protect your RP3B immediately as soon as you power those puppies up and plug them into your network. Seems like nefarious characters hijack IOT devices for their nefarious purposes.

## A Single Node

We're going to start this project with a single node. My advisors at school always encourage me to get my ideas working first then scale later.

So that's what we're going to do.

Here's a [tutorial](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) of how to get the OS onto the MicroSD card.

If you're lucky enough to own a Mac, as I am, you can use [ApplePi Baker](https://www.tweaking4all.com/news/applepi-baker-v1-9-1-update/), which is an easy and nifty program to put the OS image onto the MicroSD card.

Once you have prepped the MicroSD card with the OS, with the power off, you'll insert it into the RP3B motherboard. That slot is on the front (as opposed to the back where the USB & ethernet ports are).

Power on the RP3B. 

Once that's powered on, you'll need to find the IP address of the RP3B. You can do that by logging onto your router and looking for the new device. The router's IP address is usually something like 192.168.x.x. Unless you've changed it or this is printed on the bottom or side of the router, the username is usually admin and password is usually password.

One more note: Let's say you have a cable modem/router. Then you probably took the router that you plugged the RP3B into and plugged that into the cable modem/router. That's not a problem but you'll just need to remember (write it down) the IP address of both.

Then, if you have Windows you'll use Putty (https://www.bitvise.com/ssh-client-download), you'll open up the terminal and SSH into the RP3B device.

This is going to look something like this:

```markdown
kronos455s-computer:~ kronos455$ ssh pi@192.168.x.x ##This is your command line. 'pi' is the user name. 
                                                    ##You'll be asked the password next. It was 'raspberry' 
                                                    ##for me.
```
For the novice, you'll only use the `ssh pi@192.168.x.x` after the dollar sign. It could be a hash sign as well. Putty is a bit different in that you'll open Putty, select SSH, enter the username `pi`, enter the address `192.168.x.x`, and enter the password `raspberry`.

Once you login and enter the password successfully, you'll be asked to accept a certificate as an added security precaution. Accept it. This will keep keep someone else from being able to use that card in another device. This will be an issue later on in the recipe when you replicate the single-node image in order to set up the cluster. But this is fine. There is a work around. 

Now that you've successfully logged in, you'll configure the RP3B.

That's done by using the following command:

` sudo raspi-config `

Go through the setup and ensure the following configuration or adjust it to your choice:

- Expand SD card
- Set password
- Choose console login
- Chose keyboard layout and locales
- Overclocking, High, 900MHz CPU, 250MHz Core, 450MHz SDRAM (If you do any voltmodding ensure you have a good power supply for the PI)
- Under advanced options:
- --> Hostname: master //I called mine master.
- --> Memory split: 16mb
- --> Enable SSH Server
- --> Restart the PI.

Install a text editor of your choice. I like Nano for the beginner. If you have Raspbian Jessie Lite installed you can do that with this little bit of code:

` sudo apt-get install nano `

Edit as root or with sudo:
/etc/network/interfaces

` sudo nano /etc/dhcpcd.conf`

At the bottom of the file add:

```markdown
iface eth0 inet static
address 192.168.x.x ## IP address of your RP3B
netmask 255.255.255.0 ## This is usually the same on most routers. Check yours to make sure.
gateway: 192.168.0.1 ## This is the address of the router that you plug the RP3B directly into. 
static domain_name_servers=123.123.123.123 123.123.123.123 ##change this to whatever is showing
                                                           ##as the DNS on your router. 
```

### Update system and install Oracle Java

`sudo apt-get update; sudo apt-get install oracle-java8-jdk`

Run _*update-alternatives*_, ensure *_jdk-8-oracle-xxx_* is selected:

`sudo update-alternatives --config java`

### Hadoop Documentation

Be sure to take a look at the documentation to know what libraries must be installed to run Hadoop natively on the RP3B, as we intend to do.

https://hadoop.apache.org/docs/r2.7.2/hadoop-project-dist/hadoop-common/NativeLibraries.html

Run these installs:

```
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install zlib1g-dev gzip bzip2 liblz4-tool
sudo apt-get install python-tk python-setuptools ipython
sudo python -m easy_install -U snappy
```

### Configure Hadoop user

Create a new user for use with Hadoop:
```
sudo addgroup hadoop
sudo adduser --ingroup hadoop hduser
sudo adduser hduser sudo
```
Create SSH paris keys with blank password. This will enable nodes to communicate with each other in the cluster.

```
su hduser
mkdir ~/.ssh
ssh-keygen -t rsa -P ""
cat ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys
```
Login into `localhost` as hduser (answer yes when prompted to trust certificate key – otherwise Hadoop will fail to login later)

```
su hduser
ssh localhost
exit
```
Or, if you kind of know what you're doing in Linux, just do all of this from the user root. I found it easier (it's not more secure, though).

### Compile Native Hadoop 2.7.2 for Raspberry PI (ARM)

We compile Hadoop 2.7.2 for the Raspberry PI in order to, or so I've read but can't cite, avoid error messages that Hadoop will throw if we just download and install a pre-compiled version.

Ensure you have logged out as hduser and logged in as pi user. (for sudo command below to work properly)

Install protobuf 2.5.0

This is required to build Hadoop.
```
sudo wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
sudo tar xzvf protobuf-2.5.0.tar.gz
cd protobuf-2.5.0
./configure --prefix=/usr
make; make check; sudo make install ### Pro-tip: You can copy line by line into the command line
                                    ### or use the semi-colon to chain the commands. 
```

### Install Hadoop 2.7.2

#### Download and build
```
sudo wget http://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-2.7.2/hadoop-2.7.2-src.tar.gz
tar xzvf hadoop-2.7.2-src.tar.gz
```
Java 8 uses a more strict syntax than previous version. We need to be less strict to be able to compile Hadoop 2.7.2. To fix this edit:

`hadoop-2.7.2-src/pom.xml`

```
sudo nano hadoop-2.7.2-src/pom.xml
```

Between `<properties></properties>` tags insert the following:
```
<additionalparam>-Xdoclint:none</additionalparam>
```
For Hadoop 2.7.2 to build properly we also need to apply a patch.
```
cd hadoop-2.7.2-src/hadoop-common-project/hadoop-common/src
sudo wget https://issues.apache.org/jira/secure/attachment/12570212/HADOOP-9320.patch
patch < HADOOP-9320.patch
cd ~/hadoop-2.7.2-src/
```
To start build Hadoop run the following: (Note this may take ~1,5 hours)
```
sudo mvn package -clean -Pdist,native -DskipTests -Dtar
```

### Install

Copy compiled binaries to /opt
```
cd hadoop-dist/target/
sudo cp -R hadoop-2.7.2 /opt/hadoop
```
Give access to hduser
```
sudo chown -R hduser:hadoop /opt/hadoop/
```
Verify installation and native libraries
```
su hduser
cd /opt/hadoop/bin
hadoop checknative -a
```
The output should look like:

```
16/03/24 20:20:03 INFO bzip2.Bzip2Factory: Successfully loaded & initialized native-bzip2 library system-native
16/03/24 20:20:03 INFO zlib.ZlibFactory: Successfully loaded & initialized native-zlib library
Native library checking:
hadoop: true /opt/hadoop/lib/native/libhadoop.so.1.0.0
zlib: true /lib/arm-linux-gnueabihf/libz.so.1
snappy: true /usr/lib/libsnappy.so.1
lz4: true revision:99
bzip2: true /lib/arm-linux-gnueabihf/libbz2.so.1
openssl: true /usr/lib/arm-linux-gnueabihf/libcrypto.so
```

#### Check version

`hadoop version`
```
Hadoop 2.7.2
Subversion Unknown -r Unknown
Compiled by root on 2016-02-21T19:05Z
Compiled with protoc 2.5.0
From source with checksum d0fda26633fa762bff87ec759ebe689c
This command was run using /opt/hadoop/share/hadoop/common/hadoop-common-2.7.2.jar
```

#### Configure environment variables

In /etc/bash.bashrc, add to bottom of file:
```
export JAVA_HOME=$(readlink -f /usr/bin/javac | sed "s:/bin/javac::")
export HADOOP_INSTALL=/opt/hadoop
export PATH=$PATH:$HADOOP_INSTALL/bin
export PATH=$PATH:$HADOOP_INSTALL/sbin
export HADOOP_MAPRED_HOME=$HADOOP_INSTALL
export HADOOP_COMMON_HOME=$HADOOP_INSTALL
export HADOOP_HDFS_HOME=$HADOOP_INSTALL
export YARN_HOME=$HADOOP_INSTALL
export HADOOP_HOME=$HADOOP_INSTALL
```
### Edit and change variables in Hadoop environment.sh (/opt/hadoop/etc/hadoop/)

```
sudo nano /opt/hadoop/etc/hadoop/Hadoop_environment.sh
```
```
export JAVA_HOME=$(readlink -f /usr/bin/javac | sed "s:/bin/javac::")
```
Enable the use of native hadoop library and IPv4 stack:
```
export HADOOP_OPTS="$HADOOP_OPTS -Djava.library.path=$HADOOP_INSTALL/lib/native -Djava.net.preferIPv4Stack=true"
```
### Hadoop 2.7.x YARN and MapReduce memory and resources configuration

Some of the challanges of running Hadoop on the Raspberry is the limited resources. In order for it to run properly, we will need to adjust memory configuration of YARN and Mapreduce framework.

### YARN Configuration (yarn-site.xml)

For more details see: https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-common/yarn-default.xml

yarn-site.xml
```
<configuration>
    <property>
        <name>yarn.resourcemanager.resource-tracker.address</name>
        <value>master:8025</value>
    </property>
    <property>
        <name>yarn.resourcemanager.scheduler.address</name>
        <value>master:8035</value>
    </property>
    <property>
        <name>yarn.resourcemanager.address</name>
        <value>master:8050</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.resource.cpu-vcores</name>
        <value>4</value>
    </property>
    <property>
        <name>yarn.nodemanager.resource.memory-mb</name>
        <value>768</value>
    </property>
    <property>
        <name>yarn.scheduler.minimum-allocation-mb</name>
        <value>64</value>
    </property>
    <property>
        <name>yarn.scheduler.maximum-allocation-mb</name>
        <value>256</value>
    </property>
    <property>
        <name>yarn.scheduler.minimum-allocation-vcores</name>
        <value>1</value>
    </property>
    <property>
        <name>yarn.scheduler.maximum-allocation-vcores</name>
        <value>4</value>
    </property>
    <property>
        <name>yarn.nodemanager.vmem-check-enabled</name>
        <value>true</value>
    </property>
    <property>
        <name>yarn.nodemanager.pmem-check-enabled</name>
        <value>true</value>
    </property>
    <property>
        <name>yarn.nodemanager.vmem-pmem-ratio</name>
        <value>2.1</value>
    </property>
</configuration>
```
### MapReduce 2 configuration properties (mapred-site.xml)

For more details see:
https://hadoop.apache.org/docs/r2.7.2/hadoop-mapreduce-client/hadoop-mapreduce-client-core/mapred-default.xml

mapred-site.xml
```
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.map.memory.mb</name>
        <value>256</value>
    </property>
    <property>
        <name>mapreduce.map.java.opts</name>
        <value>-Xmx204m</value>
    </property>
    <property>
        <name>mapreduce.map.cpu.vcores</name>
        <value>2</value>
    </property>
    <property>
        <name>mapreduce.reduce.memory.mb</name>
        <value>128</value>
    </property>
    <property>
        <name>mapreduce.reduce.java.opts</name>
        <value>-Xmx102m</value>
    </property>
    <property>
        <name>mapreduce.reduce.cpu.vcores</name>
        <value>2</value>
    </property>
    <property>
        <name>yarn.app.mapreduce.am.resource.mb</name>
        <value>128</value>
    </property>
    <property>
        <name>yarn.app.mapreduce.am.command-opts</name>
        <value>-Xmx102m</value>
    </property>
    <property>
        <name>yarn.app.mapreduce.am.resource.cpu-vcores</name>
        <value>1</value>
    </property>
    <property>
        <name>mapreduce.job.maps</name>
        <value>4</value>
    </property>
    <property>
        <name>mapreduce.job.reduces</name>
        <value>4</value>
    </property>
</configuration>
```
### Configure Single Node

### Edit configuration files in /opt/hadoop/etc/hadoop

core-site.xml
```
<configuration>
  <property>
    <name>hadoop.tmp.dir</name>
    <value>/hdfs/tmp</value>
  </property>
  <property>
    <name>fs.defaultFS</name>
    <value>hdfs://localhost:54310</value>
  </property>
</configuration>
```
hdfs-site.xml
```
<configuration>
  <property>
    <name>dfs.replication</name>
    <value>3</value>
  </property>
  <property>
    <name>dfs.blocksize</name>
    <value>5242880</value>
  </property>
</configuration>
```
### Slaves

Currently we only have one node. Keep default value of localhost. We will later add all our nodes here for a multi-node setup.
```
localhost
```
### Format HDFS filesystem
```
sudo mkdir -p /hdfs/tmp ## This actually saves to a folder that is '/'. The '/opt' folder is there, too.
sudo chown hduser:hadoop /hdfs/tmp
sudo chmod 750 /hdfs/tmp
cd /hdfs/tmp
hadoop namenode -format
```
### Start Hadoop

Run the following commands as hduser:
```
bash start-dfs-sh ### Bash assuming you're running Jessie Lite.
bash start-yarn.sh
```
Or you could do what I did and run `bash start-all.sh`.

Verify that all services started correctly:
```
jps
```
Result should show the following active processes:
```
1413 NodeManager
838 NameNode
1451 Jps
1085 SecondaryNameNode
942 DataNode
1311 ResourceManager
```
If all processes not are visible review log files in /opt/hadoop/logs

### Run hadoop hello world – wordcount

Download sample files http://www.widriksson.com/wp-content/uploads/2014/10/hadoop_sample_txtfiles.tar.gz

Run all commands as hduser. Extract the files to home directory of hduser.
```
tar -xvzf hadoop_sample_txtfiles.tar.gz ~/
```
Upload files to HDFS:
```
hadoop fs -put smallfile.txt /smallfile.txt
hadoop fs -put mediumfile.txt /mediumfile.txt
```
Execute wordcount example from source code folder (~/hadoop-2.7.2-src/hadoop-mapreduce-project/hadoop-mapreduce-examples/target/):
```
time hadoop jar hadoop-mapreduce-examples-2.7.2.jar wordcount /smallfile.txt /smallfile-out
time hadoop jar hadoop-mapreduce-examples-2.7.2.jar wordcount /mediumfile.txt /mediumfile-out
```
## Configure Multiple Nodes

**_COMING SOON_**

## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/kronos455/stunning-raspberry-waffle/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/kronos455/stunning-raspberry-waffle/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
