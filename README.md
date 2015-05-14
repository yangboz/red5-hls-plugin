red5-hls-plugin
=======

HLS plugin for Red5

The purpose of this plugin is to provide HLS live streaming using an flash media stream as its source. 

The plugin utilizes Xuggler for transcoding and is provided as-is; any modifications or fixes will be handled as time permits.

Development of this plugin was sponsored by BigMarker (https://www.bigmarker.com/); BTW they're hiring, contact: careers@bigmarker.com

The Red5 users list may be found here: https://groups.google.com/forum/#!forum/red5interest

Eclipse
----------

To create the eclipse project files, execute this within the plugin and / or example directories:
```
mvn eclipse:eclipse
```

Then you will be able to import the projects into Eclipse.

Deployment
------------

1. Build both the hls-plugin and the example application (or use your own app). 
2. Place the war in the red5/webapps directory
3. Place the "hls-plugin-1.1.jar" jar in the red5/plugins directory
4. Put the "xuggle-xuggler-5.x.jar" jar in the red5/plugins directory
5. Start red5
 
<i>Note: make sure you do not have the xuggler util jar in "plugins" or "lib", it has been found to cause failures</i>

Xuggler
-------------
The Xuggler project is no longer actively developed, but remains the best way to manipulate media in Java using FFMpeg. The project page is here: https://github.com/artclarke/xuggle-xuggler
You can download Xuggler 5.4 with native libs included here: http://xuggle.googlecode.com/svn/trunk/repo/share/java/xuggle/xuggle-xuggler/5.4/xuggle-xuggler-5.4.jar

Tiago's Step-by-step Guide
-------------
Steps to install in Ubuntu 12.04

Note: Use red5 user to do the not sudo steps
```
1 - Install required packages
sudo apt-get purge openjdk-6-*
sudo apt-get install openjdk-7-jdk gcc-4.6 g++-4.6 perl yasm ant pkg-config maven2 git make
sudo ln /usr/bin/gcc-4.6 /usr/bin/gcc -s
sudo ln /usr/bin/g++-4.6 /usr/bin/g++ -s

2 - Download red5 (trunk version)
//wget "https://builds.apache.org/job/Red5%20Trunk/lastSuccessfulBuild/artifact/trunk/target/red5-server-1.0.2-RC3-server.tar.gz"

sudo apt-get install red5-server

3 - Build xuggler
git clone git://github.com/xuggle/xuggle-xuggler.git
cd xuggle-xuggler
ant
cp /dist/lib/xuggle-xuggler-noarch.jar /var/lib/red5/plugins/
cp /dist/lib/xuggle-xuggler-arch-x86_64-unknown-linux-gnu.jar /var/lib/red5/plugins/

4 - Build Red5 HLS plugin
git clone https://github.com/mondain/red5-hls-plugin.git
cd red5-hls-plugin/plugin/
mvn -Dmaven.test.skip=true
cd ../..
mkdir red5-hls-plugin/example/lib/
cp red5-hls-plugin/plugin/target/hls-plugin-1.1.jar red5-hls-plugin/example/lib/

cd red5-hls-plugin/example/
mvn eclipse:eclipse
mvn -Dmaven.test.skip=true


5 - Deploy plugin and example application to red5
cp target/hlsapp-1.1.war /var/lib/red5/webapps/
cp target/hls-plugin-1.1.jar  /var/lib/red5/plugins/

6 - Change queueCapacity to 20 in file /home/red5/red5-server-1.0.2-RC3/conf/red5-core.xml

7 - Start red5 server
```
Donations
-------------
Donate to the cause using Bitcoin: https://coinbase.com/checkouts/2c5f023d24b12245d17f8ff8afe794d3
