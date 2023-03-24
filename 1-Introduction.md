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
