# Introduction

### Ethics in Penetration Testing

##### Attackers Mindset

* Web based attacks aren’t going to stop any time soon
* Attacks constantly evolving
* Types of “hackers”:
  * Black hat – bad people, no permission
  * Grey hat – can be good people, but still no permission
  * White hat – good people, have written permission

##### Permission & Vulnerability Disclosure Policy

* The major difference between ethical and unethical is a document like this!
* Make sure to follow their policy correctly:
  * How to report the vulnerability
  * When you are allowed to disclose
  * The scope you are allowed to test

##### Vulnerability Disclosure Policy (VDP) Format

A VDP should have the following:

* Guidelines
* Hosted on the company / department’s website or resources
* Scope of testing allowed
* Exclusions (things you aren’t allowed to do or touch)
* Expectations of handling
* A way to contact the organisation

A consulting firm’s scoping document is quite similar:

* Defines the scope of the job
* Same as VDPs, but in a contract form and not public



### Basic Web Architecture

#### Terminology

| Term                         | Description                                                  |
| :--------------------------- | :----------------------------------------------------------- |
| Server                       | Computer which receives requests and holds information       |
| Client                       | Computer or browser requesting information from a server     |
| Connection                   | Method of communication to a network                         |
| Internet                     | A really big network! (A network of networks)                |
| Network Interface Card (NIC) | An adapter or piece of hardware, connected to a network, and can receive network packets for the host system |
| Spoof                        | Disguising yourself to look like something else (spy disguise) |
| Protocol                     | A set of rules software must abide by                        |

<img src="img\1\1.png" alt="1" style="zoom: 80%;" />

#### Domain Name Service (DNS)

* UDP packets (unordered)
* Phone book of the internet
* Translates domain name into IP addresses or other domain names

##### DNS Records

| DNS Record Type | Description           |
| --------------- | --------------------- |
| A               | Address Record        |
| AAAA            | IPv6 Address Record   |
| CNAME           | Canonical Record Name |
| MX              | Mail Exchange Record  |
| TXT             | Text Record           |
| NS              | Name Server Record    |

#### Internet Protocol (IP) Address

* Location on the internet
  * Can find geographic location using public IP address
* Private and public
* Has 2 versions:
  * v4
  * v6 (not in scope)
* Format:
  * 4 sets of numbers between 0 and 255, split by “.”
  * E.g. 8.8.8.8
  * First number can’t start with a 0

#### Media Access Control (MAC) Address

* Unique identifier for a Network Interface Card (NIC)
* Each card will have a specific identifier
* Easy to spoof
* Helps the switch know which NIC gets packets
* Mainly used within the internal network

<img src="img\1\2.png" alt="2" style="zoom:80%;" />



### HTTP Basics

##### HTTP

* HTTP stands for Hypertext Transfer Protocol
* It is unencrypted
* This can be listened in on, if you are on the same network subnet

##### HTTPS

* HTTPS stands for Hypertext Transfer Protocol Secure
* It is encrypted!
* This can not be listened in on, if you are on the same network subnet, unless there are vulnerabilities in the connection

##### CA Certificates

* Certificate Authority (CA)
* Root CA’s are built into OSs and browsers
* Trusted root CAs help verifying the authenticity of a certificate and the organisation that owns it.

<img src="img\1\3.png" alt="3" style="zoom: 80%;" />

#### HTTP Requests

<img src="img\1\4.png" alt="4" style="zoom:80%;" />

<img src="img\1\5.png" alt="5" style="zoom:80%;" />



### Proxy

* Piece of software that captures traffic sent through it
* We will use it to view and alter HTTP requests when performing attacks
* Can make automation easier
* Can hook into a browser very easily!

#### Interception Proxies

* A proxy that has the ability to stop a request from being sent out, awaiting the user to forward the request
* Proxies require a root certificate to be installed within the client (your browser in this case)
* Allows the proxy to decrypt the connection and re-encrypt it as required

#### Burp Suite

* Proxy software written by PortSwigger
* An industry norm
* Alternative software is OWASP ZAP (we will not be providing support for ZAP)



### How do browsers work

#### Browser

* Short for Web Browsers
* Runs on the client
* Used to locate, retrieve, and display content
* Webpages, images, videos, etc.
* Uses HTML and CSS majorly for visuals
* Uses JavaScript mainly for interactivity

#### HTTP Cookies

#### LocalStorage

* Websites can store information within your browser for later
* Can be used for managing state
* No expiration
* Accessible via JS
* Persists after browser closes
* Was an old method for enforcing bans on websites
* Maximum storage space is 5MB

#### DOM

* Document Object Model
* Parsing of HTML and XML
* Object-oriented representation of web pages
* Can be controlled by scripting languages like JS
* Document object in JS



### Cookies Explained

#### HTTP Cookies

* Aka web cookie, or browser cookie
* Used for tracking, authentication, etc.
* Common way to identify whether the user is logged in
* Have different security measures within the browsers:

| Attribute | Definition                                                  |
| --------- | ----------------------------------------------------------- |
| HTTPOnly  | JS cannot access it, unless the browser has vulnerabilities |
| Secure    | Must be send over SSL / TLS                                 |
| Expires   | Expiry time of the cookie client-side                       |
| Domain    | Domain it relates to                                        |
| Path      | Path within the web application                             |

* Cookie expiry sets a date
* If the Expiry is not set, or is set to “Session”, the browser will remove the cookie upon closing
* Cookie expiration must be done both client-side and server-side
* The browser is responsible for the client-side termination
* If the server does not terminate the cookie properly, anyone with the cookie value would be able to use it to authenticate as your user
