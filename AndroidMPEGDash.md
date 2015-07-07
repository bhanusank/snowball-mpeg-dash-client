
```
```

# System Introduction #

Multimedia is one of the most important component in the mobile devices. The main goal of this project is to add the new "streaming standard" into Android multimedia framework allowing adaptation using also **full-HD** sequences.

Natively Android framework is already able to support video streaming using Apple **HLS** standard. The idea is to extend the handler adding all the logic to manage playlists not only in **m3u8** format but also as **MPD** file (Media Presentation Description).

Also the work enrich the multimedia framework of a new component to add a basic set of adaptation heuristics used to adapt dynamically the streaming bit-rate in use accordingly to some basic platform information like screen resolution and average system throughput.


If you are interested to reproduce the demo without going throw the implementation details you can jump at the [AndroidMPEGDash#Full\_Demo\_Setup](AndroidMPEGDash#Full_Demo_Setup.md) section directly. Otherwise you can read more detailed information in the following subsections.

# Android User Space #

As reference target for the Android integration is used the _**Snowball SoC**_. All the device details are available here:

http://www.igloocommunity.org/


The latest patches are based on **Ice** **Cream** **Sandwich** code release **2012.04**.

## System Build And Setup ##

All the instruction to rebuild the full file-system are available at the following link:

http://releases.linaro.org/12.04/android/leb-snowball/

A very useful starting point to work on snowball is the following web page:

http://www.igloocommunity.org/support/Android_Getting_started

## MPEG-Dash Patches ##

To add the support for **MPEG-Dash** livestreaming to the Android multimedia framework you have to apply the following patches:

  1. A
  1. B
  1. C
  1. D

They will fix some issue in **nuplayer** component to support custom STE output video format and add all the components required to manage Dash Media Presentation Document (**MPD**).

You can download the full set of patches from the following link:

[addlink.com]

### Apply Patches ###

To apply the patches you can do as follow:

```
add here the instructions!!

```


# Pre-Built System Image #

For a quick test of the work done you can use a pre-built image containing the libraries for _Dash_. Following the instructions to download the file and flush it:

```
wget XXXXXXXXXXXXXXXXXXX
sudo riff -f XXXXXXXXXXXXXXXX
```

NOTE: All the information concerning the _riff_ tool and how to use it are available at the following link:

http://www.igloocommunity.org/support/BSP_Quick_Start


# Android Dash Client Applications #

## Android Native Application ##
A small application to be used as front end to test and integrate DASH support can be downloaded at the following links :(  http://dl.dropbox.com/u/61926816/Dash/gitDASHAgrate.apk ). The purpose of this application is to have a reference application where integrate in a simply and homogeneous way all functionalities required to exploit the _MPEG-DASH_ functionalities on Android like:
  * Representation selection;
  * Enable and disable runtime the adaptation engine;
  * Test html5 video integration;
  * Enhance the android multimedia framework providing additional hooks for user interaction;

### Source Code & Application Building System ###

The full application source code is available at the following link:


---

git clone https://<user id>@code.google.com/p/snowball-mpeg-dash-client/


**TAG:** _client-v1.0_

---


To build the full application code including the _JNI_ libraries you need to setup the _Eclipse_ **IDE** adding the Android-sdk plugin and setup also a _Builder_ for the _NDK_. Following you can find some useful reference to setup properly your working environment.

  * **ADT Plugin for Eclipse** (http://developer.android.com/sdk/eclipse-adt.html) **:** Eclipse IDE configuration to support Android SDK

  * **NDK Builder in Eclipse** (http://mobilepearls.com/labs/ndk-builder-in-eclipse/) **:** add builder in Android to compile JNI libs using the _ndk-builder_.

Once the system has been properly configured you can import directly the source code in Eclipse as Android project and build the application _apk_.

### Native Client Overview ###

![http://test-code-hosting-manuele.googlecode.com/files/androidApp-small.jpg](http://test-code-hosting-manuele.googlecode.com/files/androidApp-small.jpg)

### Client Installation&Usage ###

Once the application has been compiled. You can install and run it using ''adb'' debugger command:


---

```
    adb install -r gitDASH.apk
```

---


For more info on adb usage on snowball refer you to the following link:

http://igloocommunity.org/support/Android_Application_development

To play a video, once the list of server is there you have to do a **LONG CLICK** on the item and a sub-menu will appear with three options:

  1. **PLAY:** it will play the video;
  1. **DELETE:** delete the file from item list; (not yet supportd)
  1. **VIEW INFO:** display file info like: file size, format, in case of _mpd_ link it can display also number of description, file format support, chunks duration e.g..


Also, you can add your own links into the application database using the options menu.

## HTML5/JS Web Client ##

An extension of our client allow also the user to have its own player directly embedded in HTML5 web page and to export to the user also some kind of tricky functionalities as described below.


---

Picture to be added

---


Here the dash source is handled natively using HTML5 video tag. Instead, some extra javascript has been developed to:

  * make a pre processing if the **MPD** file.
  * set dynamically some adaptation flags like: enable/disable adaptation; fix representation to be used..e.g..
  * display run time system statistics.

# Known Limitations & Issues #

Some known limitations are:

```
a. missing support for ISO based profile for fragmented MP4;
b. dash live profile validation / service provider interoperability on going.    
```

# Full Demo Setup #

In the following section you can find all the information to reproduce step by step the full Dash client demonstrator on Snowball device.

The demo scenario is reported in the following picture.

[Picture!!](Add.md)

Here you can see that mainly we are using:

  * Snowball **SKY-S9500-ULP-C02** device;
  * Linux PC;
  * Monitor to be connected to the device throw HDMI;
  * Mouse USB.

## Target Configuration ##

From target point of view you need  to :
  1. Flush The System Image
  1. Configure Local Network

### Flush The System Image ###

Here you can find a ready to be used binary image. To dounload and flush it do as follow:

```
wget XXXX.img.gz
gunzip XXX.img.gz
sudo riff -f XXXX.img. 
```


For more information concerning **riff** utility and flushing procedure please refer you to the [AndroidMPEGDash#Pre-Built\_System\_Image](AndroidMPEGDash#Pre-Built_System_Image.md) subsection.

### Configure Local Network ###

To simplify as much as possible the demo setup the target has been connected to the server throw a point to point wired connection. The address IP assigned to the device **MUST** **BE** **192.168.42.1**. Otherwise you should reconfigure also all the other scripts used to simplify the demo setup and execution.  You can configure it throw the _Settings_ _Application_.

```
Settings->Ethernet configuration->Ethernet configuration
```

Check **Static** **IP** in the radio button menu and assign:

  1. **IP** **address** **:** 192.168.42.1
  1. **Netmask** **:** 255.255.255.0



## Local Server Configuration ##

From host point of view you need to:
  1. Install And Configure Apache Server;
  1. Configure Local Network;
  1. Clone Multimedia Resources;

### Install And Configure Apache Server ###

To install the apache server refer you to the [AndroidMPEGDash#Setup\_a\_Local\_Web\_Server](AndroidMPEGDash#Setup_a_Local_Web_Server.md) subsection.

Once it is working properly you can proceed with the configuration of apache to handle automatically mpd resources. To understand why it is temporally required and
to proceed with the configuration. please, refer you to the dedicated [AndroidMPEGDash#Setup\_a\_Local\_Web\_Server](AndroidMPEGDash#Setup_a_Local_Web_Server.md) subsection.

### Configure Local Network ###

The network setup with we re using is quite simple. In fact we have assigned to it a static IP address. Also it works as proxy for the target which allows it to go also on public web network.

So, to configure it you have to :

  * Set the IP address on the local network interface **192.168.42.2**. [example using ifconfig linux shell command line](for.md);
  * Enable IP forward. To do this you can refer to the subsection PIPPO.


If everything has been configured properly you should be able to ping the target taping to following command in a Linux shell:

```
ping 192.168.42.1
```


### Clone Multimedia Resources ###

The demo allow to test OnDemand and Live Dash profile both. For the on demand profile you can put some resources locally on the server. To do this see [AndroidMPEGDash#Media\_Resources](AndroidMPEGDash#Media_Resources.md)

INstead for the live demo you need to configure **CGI** script alias to point to the right CGI script directory. To do this see instruction reported in the [AndroidMPEGDash#Enable\_CGI](AndroidMPEGDash#Enable_CGI.md) section.

At this point you can proceed making the untar of this file under _/var/www/cgi-bin_  directory as follow:

```
tar -xvzf <file>.gz 
```

## Run The Demo ##

If the setup has been done successfully you should need just to switch on the target and wait the main Ice Cream Sandwich home screen. Once it is there, under the Applications menu you will find two different apps already installed:

  * Native Client Application : is a java application as described in the [AndroidMPEGDash#Native\_Client\_Overview](AndroidMPEGDash#Native_Client_Overview.md) section.
  * Web Client Launcher : it is a simply launcher which do all the required settings on the target and launch automatically the web page described in the [AndroidMPEGDash#HTML5/JS\_Web\_Client](AndroidMPEGDash#HTML5/JS_Web_Client.md) subsection.


## Demo Limitations ##

TBD

# Extra Settings #

## Network Traffic Shaper ##

To test the system adaptation engine we have used a small script called **WanderSahper**. More details are available at this link http://www.ubuntu-unleashed.com/2008/05/howto-limit-uploaddownload-speeds-and.html.

On _Ubuntu_ you can install it using _apt-install_ utility.


---

```
  apt-get install wondershaper
```

---


You can setup it in just few steps:


# Now once you have the download/upload amounts in kilobits lets shape our traffic:
```
  sudo wondershaper ''ifacename'' 1536 128
--
 *NOTE :* The size is in ''Kbps''
```

# Check the status of wondershaper:
```
  sudo wondershaper ''ifacename''
```

# Howto disable shaping on specified interface:
```
  sudo wondershaper clear ifacename
```

## Setup a Local Web Server ##

If you are using an Ubuntu Linux machine you can install a web server Apache as follow:


---

```
  sudo apt-get install apache2
```

---


At this point you have to set properly the ownership of the web server root directory:


---

```
  chmod -R 777 /var/www
```

---


At this point to test if the link is working insert in your web-browser the following link:

http://localhost/index.html

At this point your web server is upper running and you can put there all the media sources you want to setup a local environment with multimedia contents.

## Enable CGI ##

To enable **cgi** support on apache you need to edit default setting file under :

```
./sites/available/default
```

And edit the ScriptAlias section as follow:

```
	ScriptAlias /cgi-bin/ /var/www/cgi-bin/
	<Directory "/var/www/cgi-bin/">
		AllowOverride None
		Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
		Order allow,deny
		Allow from all
	</Directory>
```

At this point restart the **apache2** server taping:

```
sudo service apache2 restart
```


## Media Resources ##

At the following link you can find media sequences to test locally the player:

```
   wget http://dl.dropbox.com/u/61926816/Sequences/ED.tgz
```

Untar it under :

```
 /var/www/
```

Using the following command:

```
 cd /var/www
 tar -xvzf /<archive_path>/ED.tgz
```

At this point the web server have the resources to be shared!!

## Remote Git Repository Import ##

```
git clone https://manuelelupo%40yahoo.it@code.google.com/p/snowball-mpeg-dash-client/
cd snowball-mpeg-dash-client
git config http.postBuffer 524288000
git remote add googlecode https://manuelelupo%40yahoo.it@code.google.com/p/snowball-mpeg-dash-client.test/
git push --all googlecode
git push --tags googlecode
```

The last operation can require few minutes depending the repository size your are pushing!!

## Linux network Speedometer ##

To monitor the network performances on the server, should be useful the following application:


---

```
  sudo apt-get install speedometer
```

---


In particular, in oour case we use it to display graphically the network interface performances during the streaming session.


---

```
  speedometer -tx ethX
```

---


## Dump DASH Statistics ##

To dump some DASH information and log them on a local file on your PC you can use **adbstat** utility.

Each time the client send a debug message throw ADB log messages using a specific TAG ID it will save the message and add to it a local timestamp and the bandwith value in use at that time i upload.

```
      ./adbstats <TAG_NAME> <network if>
-----------------------------------------------
      _Example: ./adbstats STATISTICS eth0_
```

It i useful to dump statistics information and post-process them.


### Compilation Instruction ###

> Download the file http://test-code-hosting-manuele.googlecode.com/files/main_server.cpp and compile it as follow:

```
  g++ -o adbstats main_server.cpp -lpthread
```


### Usage Instruction ###

```
- Export *adb* in shell standard path "*PATH* environment";

- adb connect <device IP>:<port>

- ./adbstats <TAG_NAME> <network if>
```

The server will run and create a local file "dump.txt".
At this point the server will filter all the messages on logcat interface. Every time it receive a message with 

<TAG\_NAME>

 it will dump the result into the output local file removing the application tags and holding the pure message!!

So..to interact with it you have to send from your native code or directly from java code a log message with a TAG which you choose to identify the debugging sequence. In this way you can wave multiple instances at same time of the server associated to different **TAGS**.

To end the execution type a button on the keyboard.

### Usage Sample ###

For example in this case we want send throw adb two values to be stored into the dump file for statistic info plotting. To do this we use a DUMP macro like this:

```
#define DUMPSTAT(TAG, format, args...) do { \
	char msg[2048]; \
	sprintf(msg, "%s (%d) :  ", __FUNCTION__, __LINE__); \
	sprintf( msg + strlen(msg), format, args); \
	__android_log_write(ANDROID_LOG_INFO, TAG, msg); \
	}while(0);
```

So, you can insert this line in the point where you want to save the values:

```
DUMPSTAT("DUMPSTAT", " %lld %lld", throughput_mLastDeltaTimeUs, lastBitrateEstimated );
```

The server application will create a log file formatted as follow:

```
6817.53 26976838   0 8730672 
5237.8 26645532   0 4740811
3925.18 27317888   0 3317462 
2809.29 33268488   0 2480539 
2195.8 17655344   0 2100024 
1821.25 17892521   0 1908376 
1687.28 16329079   0 3070895 
2478.92 20352050   0 2453703
1046.61 26490681   0 4220886
555.635 32039832   0 3554809 
1621.77 24909846   0 1546021 
1707.75 15101195   0 1799676 
3004.07 22361394   0 6903872 
1788.05 57118483   0 2299411 
1945.44 21648490   0 1802240 
2076.44 15651620   0 2326104 
2272.42 17289114   0 2727622 
3043.4 16805300   0 3544145
1375.79 43427766   0 7369628 
3789.36 18997370   0 5952432 
5496.63 33808600   0 8791680 
5431.18 20847929   0 7784188 
392.604 41383571   0 4586607 
```

To plot this you can use a very simple script for **gnuplot**. Following a simple example used to display the data formatted as described before.

```
set border linewidth 2
set ylabel "bandwith [kbit/s]"
set xlabel "time (s)"
set grid
set autoscale  x

plot "dump.txt" using ($2)/1000:1 title "Upload Server Throughput" , "dump.txt"  using ($2)/1000:($4)/1024 title "Download Client Throughput"  


set terminal jpeg
set output 'plot.jpeg'
replot

pause -1 "Hit any key to continue"
```


If you run the command

```
gnuplot <scriptname>
```


# Additional Projects #

## HLS Segmenter ##

To create HLS sequences and `m3u8` playlist you can follow the instruction form this page:


http://www.ioncannon.net/programming/452/iphone-http-streaming-with-ffmpeg-and-an-open-source-segmenter/comment-page-1/

The source code for the streamer application is available here http://svn.assembla.com/svn/legend/segmenter/.

Nevertheless, to have the full trans-coding chain working you must recompile _ffmpeg_ enabling the ''x264'' support. Here you can find all the info on how to recompile ffmpeg enabling x264 support and how to transcode your own sequences wrapping them in mpeg2ts.

http://code.google.com/p/test-code-hosting-manuele/wiki/ffmpegTranscodingTutorial


Once you have recompiled ffmpeg you are ready to create your own  _hls_ sequences. In fact, using **ffmpeg** you can convert your sequences in **MPEG2TS** format and the segmenter will split them and create the associated m3u8 playlist.

# References #

- **HTML5WebView Wrapper** ([http://www.tandroid.org/html5webview ]) **:** wrapper used to integrate HTML5 in webview and support ''Dash'' video playback using _HTML5_ video tags.

- **Adaptive Bit Rate Video Streaming** ([http://mashable.com/2011/01/25/adaptive-bit-rate-video-streaming/ ]) **:** why Delivery Will Matter More Than Codec.

- **Motorola Application Tutorials** (http://developer.motorola.com/docstools/library/) **:** interesting set of tutorial on android apps  development.

- **Android Build Tips And Tricks** (http://www.bittoggler.com/2010/06/android-build-tips-and-tricks.html) : some useful info on android make command.

- **Ordering of LOCAL\_STATIC\_LIBRARIES** (http://groups.google.com/group/android-ndk/browse_thread/thread/2577021150137c1d) **:** interesting notes on linking order.

- **Create HLS sequences** (http://www.priyaontech.com/2011/11/generating-http-live-streaming-content-for-ios-devices/) **:** link with all the instruction to generate HLS sequences using mediasegmenter provided by apple.