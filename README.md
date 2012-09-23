### How to run pysiriproxy server on a jailbroken iPhone ###

*Please note that running pysiriproxy on an iPhone is not supported by the developer.  These instructions are provided for reference only and are not guaranteed to be accurate.  I am not affiliated with the author of pysiriproxy, and neither I nor the author of the pysiriproxy software are responsible for damages caused by the use of these instructions.  With that said, let's have some fun.*

1.	Install (these packages can be found in ```python-pkgs```):
	-	python (python_2.6.5-7_iphoneos-arm.deb)
	-	setuptools (py26-setuptools_0.6c11-3_iphoneos-arm.deb)
	-	zopeinterface (py26-zopeinterface_3.8.0-1_iphoneos-arm.deb)
	-	twisted (py26-twisted_12.0.0-1_iphoneos-arm.deb)
	-	cfpropertylist (cfpropertylist.zip or latest cfpropertylist downloaded from internet, run ```python setup.py install```)
	-	pyamp (pyamp_1.0.tar or latest pyamp downloaded from internet, run ```python setup.py install```)
	-	pyopenssl (py26-pyopenssl_0.11-3_iphoneos-arm.deb)
	-	biplist (sudo easy_install biplist)

2.	Edit pysiriproxy's setup.py to exclude dependency on twisted (iphone can't compile native extensions, so we manually install twisted and get rid of dependency).  In setup.py, change:

	```install_requires=[
	"biplist>=0.5",
	"twisted==12.1.0",
	"pyamp>=1.2",
	],```

	to:

	```install_requires=[
	"biplist>=0.5",
	"pyamp>=1.2",
	],```

3.	Install pysiriproxy (run ```python setup.py install```)

4.	Symlink directories:
	``` ln -s /usr/pysiriproxy /usr/local/pysiriproxy```

5.	Edit /etc/hosts to point guzzoni.apple.com to 127.0.0.1

6.	Edit ~/.pysiriproxy.cfg to change Host = "guzzoni.apple.com" to Host = "17.174.8.10"

7.	Run pysiriproxy

8.	[Optional, and untested.  Haven't yet been able to figure out how to get this running reliably.]  To make pysiriproxy run at startup, create a LaunchDaemon file named pysiriproxy.plist in /Library/LaunchDaemons:
```xml
<?xml version="1.0" encoding="UTF-8"?>                       
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST
1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	    <string>pysiriproxy</string>
	<key>ProgramArguments</key>
	    <array>
	        <string>/usr/bin/python</string>
	        <string>/var/mobile/Documents/pysiriproxy-0.0.6/siriproxy</string>
		</array>
	<key>RunAtLoad</key>
	    <true/>
	<key>KeepAlive</key>
		<true/>
</dict>
</plist>```