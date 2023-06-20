# OWASP ZAP - WebApp Testing

### **Introduction**

OWASP Zap (Zed Attack Proxy) is a security testing framework much like Burp Suite. It acts as a very robust enumeration tool. It’s used to test web applications.

#### Benifits

* It’s completely open source and free.
* **Automated Web Application Scan**: This will automatically passively and actively scan a web application, build a sitemap, and discover vulnerabilities. This is a paid feature in Burp.
* **Web Spidering**: You can passively build a website map with Spidering. This is a paid feature in Burp.
* **Unthrottled Intruder**: You can bruteforce login pages within OWASP as fast as your machine and the web-server can handle. This is a paid feature in Burp.
* **No need to forward individual requests through Burp**: When doing manual attacks, having to change windows to send a request through the browser, and then forward in burp, can be tedious. OWASP handles both and you can just browse the site and OWASP will intercept automatically. This is NOT a feature in Burp.

#### Features Translation from Burp Suite to OWASP ZAP

<figure><img src="../../../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

***

### **Automated Scan**

The automated scan performs both passive and automated scans to build a sitemap and detect vulnerabilities.

On the next page you may see the options to select either to use “traditional spider” or “Ajax spider”.

#### Traditional Spider

A traditional spider scan is a passive scan that enumerates links and directories of the website. It builds a website index without brute-forcing. This is much quieter than a brute-force attack and can still net a login page or other juicy details, but is not as comprehensive as a bruteforce.

#### Ajax Spider

The Ajax Spider is an add-on that integrates in ZAP a crawler of AJAX rich sites called Crawljax. You can use it in conjunction with the traditional spider for better results. It uses your web browser and proxy.

The easiest way to use the Ajax Spider is with **HTMLUnit**.

* To install HTML Unit use the command
  * `sudo apt install libjenkins-htmlunit-core-js-java`
* And then select `HtmlUnity` from the Ajax Spider Dropdown.

***

### **Manual Scanning**

Like Burp, you should set-up your proxy between OWASP ZAP and your Browser. We’ll be using Firefox.

#### Proxy Settings

Goto `Options -> Local Proxies`, Change Local Firefox Proxy settings to the above.

#### Add ZAP Certificated

Without importing ZAP Certificates, ZAP is unable to handle simultaneous Web request forwarding and intercepting. Goto `Options -> Dynamic SSL Certificates` and save the certificate which should later be imported into firefox.

***

### Scanning Authenticated Web Applications

Without your Zap application being authenticated, it can't scan pages that are only accessible when you've logged in.

We're going to pass our authentication token into ZAP so that we can use the tool to scan authenticated webpages.

In ZAP open the HTTP Sessions tab with the new tab button, and set the authenticated session as active.

Now re-scan the application. You’ll see it’s able to pick up a lot more.

***

### Brute-Force Directories

If the passive scans are not enough, you can use a wordlist attack and directory bruteforce through ZAP just as you would with gobuster. This would pick up pages that are not indexed.

1. First. Go into your `ZAP Options`, navigate to `Forced Browse`, and add the Custom Wordlist. You can also add more threads and turn off recursive brute-forcing.
2. Then, right click the `site->attack->forced browse site`
3. Select your imported wordlist from the list menu, and then hit the play button!

***

### Brute-Force Web Login

If you wanted to do this with BurpSuite, you'd need to intercept the request, and then pass it to Hydra. However, this process is much easier with ZAP!

1. Send Manual Login Request to the Website
2. Find the GET request and open the Fuzz menu.
3. Then highlight the password you attempted and add a wordlist. This selects the area of the request you wish to replace with other data.
4. After running the fuzzer, sort the state tab to show Reflected results first. Sometimes you will get false-positives, but you can ignore the passwords that are less than 8 characters in length.

***

### **ZAP Extensions**

Want to further enhance ZAPs capabilities? Look at some of it’s downloadable extensions! [Zap-Extensions](https://github.com/zaproxy/zap-extensions)

#### Bugcrowd HUNT

[Link](https://github.com/bugcrowd/HUNT) This will passively scan for known vulnerabilities in web applications.&#x20;

<figure><img src="../../../../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

***
