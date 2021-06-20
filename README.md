This is a script written in bash that lets you automatically connect and refresh connections to Vodafone Hotspots in Italy (although it should work for other countries too with few changes to the url and the parameters which i didn't bother to do since i haven't had the need to use this abroad).
If your internet provider is Vodafone and you use their provided Vodafone Station you can enable a setting in the router which allows for your unused bandwidth to be shared with other people who are Vodafone customers through a secondary wireless interface that broadcasts a standard SSID "Vodafone-WiFi".
The prerequisites to use this are:
1. Being a Vodafone subscriber (you need to register for a Vodafone community account on their website to get your credentials) or have some friend give you their credentials.
2. Having activated the option on the Vodafone Station to share your bandwidth (or have your friend who gave you their credentials do it).
3. Access to a unix system with a POSIX shell, wget, grep and cut.

New:
Added support for vodafone roam users:
If you are nearby a vodafone router and see a Vodafone-WiFi you can connect and buy connection time by registering through the captive portal for a vadofone account. Support was added to this script for use in such cases. Make sure to subscribe and pay for connection time and then set the respective parameters in the script.

Then you just need to set the parameters in the script (username and password must be url encoded, you can use any tool you like or use [this](https://www.urlencoder.org/) website.
This was written on Arch linux and tested on Arch, Ubuntu 18.04.x and Openwrt 18.06.x to 19.07.7.

Note: If you want a completely automated connection manager based on this (like running it on the router) you need to setup the proper scripts at boot (in openwrt for example you could place a script in /etc/hotplug.d/iface/XX-something where you run the script when your desired interface goes up) and setup a cron job every 5 minutes (which is the lease time the Vodafone Station gives every dhcp client).
Also note that if you want to run this on boot you need to set the parameter "SSL" to no in the script; that's because at boot and before a connection is available the devices without a real time clock need to synchronize their time through NTP. So if you rely on this for connectivity your time won't be synched and wget SSL verification will fail. On openwrt i might suggest to use the package [travelmate](https://github.com/openwrt/packages/blob/master/net/travelmate/files/README.md) to automate the connection to the wireless hotspots.

Note 2: On some openwrt devices (those with little flash storage) the default wget is uclient-fetch which is not enough for this script to run, you need to install wget from opkg in order for this to work on those devices.
