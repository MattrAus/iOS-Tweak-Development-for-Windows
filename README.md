# iOS Tweak Development for Windows :iphone::memo::four::computer:
A simple guide on how to setup and configure your windows environment for developing Cydia tweaks.

---

## Get Cygwin 
	
32-bit version: https://cygwin.com/setup-x86.exe  
64-bit version: https://cygwin.com/setup-x86_64.exe  


## Installing Initial Cygwin Package
**Select Packages** and search for **lynx** and under **Web** will be *"lynx: A text-based Web Browser"*

Click on **lynx** once, and click **next**, let it download and install.

*Create icon on Desktop* for ease-of-access to **Cygwin**.


## Installing Additional Cygwin Packages  
After installing *lynx*, we can now install other packages much easier.


### Install apt-cyg
Put the following code into Cygwin.

	lynx -source rawgit.com/transcode-open/apt-cyg/master/apt-cyg > apt-cyg  
	install apt-cyg /bin  
	
<sup>Check out apt-cyg on [Github](https://github.com/transcode-open/apt-cyg)</sup>


### Installing Development Tools
Just copy and paste this whole block of text into **Cygwin** and let it download and install all of the Development-related tools.  
	
	apt-cyg install ca-certificates 
	apt-cyg install git  
	apt-cyg install make  
	apt-cyg install openssh  
	apt-cyg install perl  
	apt-cyg install python  
	apt-cyg install wget  


## Setting up $THEOS Directory
The default theos directory used throughout the rest of this guide

	export THEOS=/opt/theos

## Installing Theos
	
	git clone --recursive https://github.com/theos/theos.git $THEOS/


## Installing iOSToolchain4Win

	mkdir -p $THEOS/toolchain/windows  

### 32-Bit System
Only supports up to **iOS 8.4 SDK** with armv7 *(no support for arm64)*.
	
	git clone -b master https://github.com/coolstar/iOSToolchain4Win.git $THEOS/toolchain/windows/iphone  

### 64-Bit System
Supports up to **iOS 9.3 SDK** with armv7 and arm64. *(possibly iOS 10 SDK)*
	
	git clone -b x86_64 https://github.com/coolstar/iOSToolchain4Win.git $THEOS/toolchain/windows/iphone  


## Obtaining SDKs
Grab the necessary SDKs you need for development and download them.

### Creating SDK directory
	
	mkdir $THEOS/sdks  
	cd $THEOS/sdks  

### Installing SDK
*Replace* **X.X** *with the* **iOS version** *you wish to download*
	
~~wget https://sdks.website/dl/iPhoneOSX.X.sdk.tbz2~~

	wget http://resources.airnativeextensions.com/ios/iPhoneOSX.X.sdk.zip
	
<sup>Check out ~~[sdks.website](https://sdks.website)~~ [airnativeextensions.com](http://resources.airnativeextensions.com/ios/) for available SDKs.</sup>

### Extracting SDK
*Replace* **X.X** *with the* **iOS version** *you wish to extract*
	
	tar xvf iPhoneOSX.X.sdk.zip


## Installing Headers
Download Headers used to hook into iOS.  
	
	git clone https://github.com/theos/headers.git $THEOS/temp  
	mv $THEOS/temp/.git $THEOS/include/.git  
	rm -rf $THEOS/temp  
	  
	git clone https://github.com/coolstar/iOS-9.3-SpringBoard-Headers.git $THEOS/temp  
	mv $THEOS/temp/.git $THEOS/include/.git  
	rm -rf $THEOS/temp  

<sup>`/temp` is used to circumvent "non-empty directory" error.</sup>


## Remotely Connect to your iDevice
These commands put the export lines into your .bash_profile (Default: `C:\cygwin\home\%user%\.bash_profile`).  
	
	echo 'export THEOS=/opt/theos' >> ~/.bash_profile  
	echo 'export THEOS_DEVICE_IP=XXX.XXX.XXX.XXX THEOS_DEVICE_PORT=22' >> ~/.bash_profile  
	
<sup>Replace **XXX.XXX.XXX.XXX** with your **Device's IP**</sup>


## Projects Directory
	
	mkdir /opt/projects  
	cd /opt/projects  


## New Instance Creator
Templates for creating projects (such as tweaks)
	
	$THEOS/bin/nic.pl  

<sup>Select **iphone/tweak**, **11.** if you have used this guide.</sup>

## Begin Coding :page_facing_up:
I personally use:  
* [Visual Studio Code](https://www.visualstudio.com/products/code-vs)  
* [Visual Studio Enterprise](https://www.visualstudio.com/products/visual-studio-enterprise-vs) or  
* [Atom](https://atom.io/)  

--- 
<sup>
:books:		
https://coolstar.org/theos.pdf  
https://cygwin.com/  
https://github.com/coolstar/iOSToolchain4Win/  
https://github.com/theos/theos/  
https://github.com/theos/theos/wiki/Installation  
https://github.com/transcode-open/apt-cyg/  
https://iphonedevwiki.net/index.php/Theos/Setup  
https://sdks.website/  
https://sharedinstance.net/2013/12/build-on-windows/  
</sup>
---
<sup>
:money_with_wings:  
[Donate via PayPal](https://paypal.me/matthewtrigg/5aud)  
</sup>
