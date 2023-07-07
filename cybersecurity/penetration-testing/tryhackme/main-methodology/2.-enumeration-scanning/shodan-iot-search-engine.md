# Shodan - IOT Search Engine

### Introduction

Shodan.io is a search engine for the Internet of Things. Shodan scans the whole internet and indexes the services run on each IP address.



### **Finding services**

* We need to grab their IP address. We can do this using `ping`.
* We can ping website and the ping response will tell us their IP address.
* Then once we do this, we put the IP address into Shodan to get the services
* If services like Cloudflare acts as a proxy between website and their real servers, this isn’t helpful. We need some way to get their IP addresses.
* We can do this using Autonomous System Numbers.



### **Autonomous System Numbers**

* An autonomous system number (ASN) is a global identifier of a range of IP addresses.
* If you are an enormous company like Google you will likely have your own ASN for all of the IP addresses you own.
* We can put the IP address into an ASN lookup tools, Which tells us the ASN number.
* On Shodan.io, we can search using the ASN filter. The filter is `ASN:[number]`



### **Banners**

* To get the most out of Shodan, it’s important to understand the search query syntax.
* Devices run services, and Shodan stores information about them. The information is stored in a banner.
* An example banner looks like:
  * ```json
    {
    		"data": "Moxa Nport Device",
    		"Status": "Authentication disabled",
    		"Name": "NP5232I_4728",
    		"MAC": "00:90:e8:47:10:2d",
    		"ip_str": "46.252.132.235",
    		"port": 4800,
    		"org": "Starhub Mobile",
    		"location": {
    				"country_code": "SG"
    		}
     }
    ```



### **Filters**

* On the Shodan.io homepage, we can click on “explore” to view the most up voted search queries. The most popular one is webcams.
  * https://www.shodan.io/explore
* It is legal to view a publicly accessible webcam, it is illegal to try to break into a password protected one.
* we can actually combine 2 searches into 1 using multiple queries.



### **API**

* The API lets us programmatically search Shodan and receive a list of IP addresses in return. If we are a company, we can write a script to check over our IP addresses to see if any of them are vulnerable.



### **Shodan Monitor**

* Shodan Monitor is an application for monitoring your devices in your own network.
  * Keep track of the devices that you have exposed to the Internet. Setup notifications, launch scans and gain complete visibility into what you have connected.



### **Shodan Dorking**

* Shodan has some lovely webpages with Dorks that allow us to find things. Their search example webpages feature some.
* For instance
  * `has_screenshot:true encrypted attention`
  * Which uses optical character recognition and remote desktop to find machines compromised by ransomware on the internet.
  * Another command for getting labelled ss is `screenshot.label:ics`
* You can find more Shodan Dorks on GitHub.



### **Shodan Extension**

* Shodan also has an extension.
* When installed, you can click on it and it’ll tell you the IP address of the webserver running, what ports are open, where it’s based and if it has any security issues.
* this is a good extension for any people interested in bug bounties, being quickly able to tell if a system looks vulnerable or not based on the Shodan output.

