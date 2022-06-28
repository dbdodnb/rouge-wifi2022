#RogueWifi
![alt tag](http://i.imgur.com/1VlMf44.png)

Once authenticated, both passwords ([first-attempt] and [second-attempt]) are dumped into "passwords.txt" along with the email/username and type of 
authentication (Google, Facebook, Twitter and Linkedin) and the user is granted access to the internet. 

###IMPORTANT: You need to add the line:

**www-data ALL=(ALL:ALL) NOPASSWD: /sbin/iptables, /usr/sbin/arp**

to 

/etc/sudoers.  

![alt tag](http://i.imgur.com/uz6DfnG.png)

NOTE: /sbin/ and /usr/sbin/ may not be the locations of arp/iptables for you, so do a "whereis arp && whereis iptables" to find the correct path.
dbconnect will need to add routes to iptables based on the MAC address trying to connect, without sudo rights, this will not work.

This was built on Kali Linux on a VM, so most of the dependencies to run this "out of box" are already installed, except hostapd. On other versions of linux you 
may need to install php5, dnsmasq and some other php dependencies, along with apache2. Also the below assumes you have your internet connection through eth0. If you
are using two wifi cards, just switch out eth0 (in my below example) for {internet interface}. The internet facing interface can be wired or wireless, but obviously
the AP interface needs to be a wireless interface.

**To run:**  
Just place all files in /var/www/html/, run the command chown `www-data:www-data ./*` (may want to limit it to the html, js, passwords.txt and images if running on a large
network) and run:
`wifi.sh wlan0 eth0 {network name}` without brackets and enjoy!

**Some final notes -**  
If the script runs but you dont see the network, you may have some driver issues with hostapd and alpha - just make sure you have the correct driver set running
and it should work. You can troubleshoot by running: `hostapd -dd /etc/hostapd/hostapd.conf` and looking at the error messages
If you want to run this using something other than dnsmasq or using a different IP scheme, you may need to edit index.html and dbconnect.php and remove "10.0.0.1" 
from a few lines. They aren't really required for this to work.
  
Special thanks to jeretc for his HTML templates! https://github.com/jeretc/cfp

![alt tag](http://i.imgur.com/lsMvE7p.jpg)
