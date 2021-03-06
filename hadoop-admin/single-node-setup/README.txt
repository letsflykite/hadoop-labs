Hadoop Administration - Single Node install
---

Lab goal : install and configure hadoop on a single node


-- step 1)
Login into the linux node.  Instructor will provide credentials



-- step 3)
verify password-less ssh is working on this node
    $  ssh localhost
say yes to the prompt


-- step 4)
verify the following files are in ~/hi directory
    hadoop install file : ~/hi/software/hadoop/apache
    java installer : ~/hi/software/java


-- step 5) install java
    $  cd ~/hi/software/java
    $  sudo sh ./jdk-6u45-linux-x64-rpm.bin


-- step 6)
verify java is installed
    $ java -version

you should see output similar to the following
    java version "1.6.0_45"
    Java(TM) SE Runtime Environment (build 1.6.0_45-b06)
    Java HotSpot(TM) 64-Bit Server VM (build 20.45-b01, mixed mode)


-- step 7)
we will install hadoop using TAR file format.
verify the hadoop file exists in   ~/hi/software/hadoop/apache/hadoop-1.1.2-bin.tar.gz
(version numbes 1.1.2 might be different on your node)


-- step 8)
untar hadoop file under home directory
    $  cd    #  <-- so you are in home dir
    $  tar xf ~/hi/software/hadoop/apache/hadoop-1.1.2-bin.tar.gz
    $  mv hadoop-1.1.2 hadoop   (adjust if your version is different)
now we have hadoop program files in  ~/hadoop  dir.  We will refer this directory as HADOOP_HOME

verify the following directories exist under HADOOP_HOME
    bin
    conf
    lib
    sbin


-- step 9)
create a data dir for hadoop
    $  mkdir /hadoop/hadoop-data


Next, we will configure Hadoop.  Hadoop configuration file are in  HADOOP_HOME/conf dir.

Minimal configuration files are provided in ~/hi/config/hadoop-single directory.  We will copy these files into HADOOP_HOME/conf dir


-- step 10)
(optional)
Edit file HADOOP_HOME/conf/hadoop-env.sh
and update the JAVA_HOME variable
    export JAVA_HOME=/usr/java/latest

(optional) also edit the following line (around line 37)
    export HADOOP_SSH_OPTS="-o StrictHostKeyChecking=no"


-- step 11)
copy minimal config files provided into HADOOP_HOME/conf dir
    $  cp ~/hi/config/hadoop-single/*   ~/hadoop/conf/

inspect the following files:

    conf/core-site.xml
    conf/mapred-site.xml
    conf/hdfs-site.xml
    conf/masters
    conf/slaves


-- step 12)
format namenode storage
    $   ~/hadoop/bin/hadoop namenode -format


-- step 13)
start hadoop deamons
    $  ~/hadoop/bin/start-all.sh


-- step 14)
verify the deamons are running
    $   jps
(if jps is not in path, try  /usr/java/latest/bin/jps)

output will look similar to this
    9316 SecondaryNameNode
    9203 DataNode
    9521 TaskTracker
    9403 JobTracker
    9089 NameNode

Looks like we have all deamons running!


-- step 15)
Verify UIs by namenode and job tracker
In a browser, go to the following URLs
    namenode UI:   http://machine_host_name:50070
    job tracker UI:   http://machine_host_name:50030

substitute 'machine host name' with public IP of your node
e.g :   http://ec2......com:50070


[BONUS LAB 1]
explore hadoop-data directories
    $ find /hadoop/hadoop-data
how does hadoop organize data?


-- Well done!)
You have installed and configured hadoop on a single node
