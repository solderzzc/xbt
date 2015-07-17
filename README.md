# xbt
Automatically exported from code.google.com/p/xbt


XBT TRACKER INSTALLATION(http://www.visigod.com/xbt-tracker/installation)
The XBT Tracker can run on Unix/Linux or Windows. Please check the tutorial that fits you best.
 
 Using Unix/Linux
The XBT Tracker must be compiled from source on Unix/Linux. You need shell and root access to compile and run XBT Tracker. You also need the following packages:
boost-devel
mysql-devel
gcc-c++
subversion
 
To install this required packages you can run the following commands in your server:
Installing the required packages on Debian
1
2
3
apt-get install cmake g++ libboost-date-time-dev libboost-dev \
libboost-filesystem-dev libboost-program-options-dev libboost-regex-dev \
libboost-serialization-dev libmysqlclient15-dev make subversion zlib1g-dev
 
Installing the required packages on CentOS, Fedora or Red Hat
1
yum install boost-devel gcc-c++ mysql-devel subversion
 
If for some reason the boost libraries are still on the old version, you can do the following:
Install Boost manually
1
2
3
4
5
6
cd /usr/local/src/
wget http://sourceforge.net/projects/boost/files/boost/1.53.0/boost_1_53_0.tar.gz/download
tar xvzf boost_1_53_0.tar.gz
cd boost_1_53_0
./bootstrap.sh
./bjam install
 
Then create a folder in your server and type the following:
1
2
3
4
svn co http://xbt.googlecode.com/svn/trunk/xbt/misc xbt/misc
svn co http://xbt.googlecode.com/svn/trunk/xbt/Tracker xbt/Tracker
cd xbt/Tracker
./make.sh
 
After the server is compiled you will have a xbt_tracker binary under xbt/Tracker. Copy this binary into the directory where you will run XBTT along with the xbt_tracker.conf.default that is on the same folder. You will end up with two files in your xbt directory: the xbt_tracker and the xbt_tracker.conf.default. Rename the xbt_tracker.conf.default to xbt_tracker.conf.
we are using /home/xbt_tracker as an example
1
2
3
4
5
cp xbt_tracker /home/xbt_tracker/
cp xbt_tracker.conf.default /home/xbt_tracker/
cp xbt_tracker.sql /home/xbt_tracker/
cd /home/xbt_tracker/
mv xbt_tracker.conf.default xbt_tracker.conf
 
We now need to create a database to be used with XBTT. You can use phpMyAdmin of the mysql command to create it. See the example below using the mysql client:
1
2
3
4
CREATE USER 'xbt_tracker'@'localhost' IDENTIFIED BY 'my_tracker_password';
GRANT USAGE ON * . * TO 'xbt_tracker'@'localhost' IDENTIFIED BY 'my_tracker_password';
CREATE DATABASE IF NOT EXISTS `xbt_tracker` ;
GRANT ALL PRIVILEGES ON `xbt_tracker` . * TO 'xbt_tracker'@'localhost';
 
After the database is created we need to import the default sql that we previously copied into our xbt_tracker home directory. Just type the following command in the shell of your server:
1
mysql -uxbt_tracker -pmy_tracker_password xbt_tracker < xbt_tracker.sql
 
Ok, the default database schema (xbt_tracker.sql) is imported into the database we have created. All that is left is to configure XBTT to use it. To do so, edit the xbt_tracker.conf in the xbt_tracker home directory and use the following (change the values to fit you need. We are going to use the ones from the previous commands):
1
2
3
4
mysql_host = localhost
mysql_user = xbt_tracker
mysql_password = my_tracker_password
mysql_database = xbt_tracker
 
We have now concluded the installation of XBTT on our server. So let's start it. To do it just type:
1
./xbt_tracker
 
You now have XBT Tracker running on the default port 2710. To customize it please read the Configuration page. To see how you can always start XBT Tracker when your server starts please check the General Tips page.
 
 Using Windows
To use the tracker on Windows you can download the installation file from the XBT project page. After downloading the exe file you must run it to install it on your computer. The windows version is installed by default as a service.
Personal note: Although XBT Tracker runs on Windows I recommend you to run it on a linux server.
