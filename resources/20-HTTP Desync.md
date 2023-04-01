# HTTP Desynchronisation Attacks



### Desynchronisation

* Also known as falling out of sync
* Imagine syncing files to dropbox, but it isn’t as good, and one of the computers don’t have internet for a bit.



### HTTP Desync Attacks

* Also known as HTTP desynchronisation attacks
* Discovered by James Kettle (albinowax) of PortSwigger
* Very complicated attack which few people can exploit
* Extremely modern (released publicly in 2019)
* Desynchronisation between the frontend and the backend server
* Usually relates to some kind of proxy or caching server
* Similar to buffer overflow (in the sense that you overflow the amount of information expected, into the next request), **but not the same attack**



<img src="img\20\1.png" alt="1" style="zoom:80%;" />

<img src="img\20\2.png" alt="2" style="zoom:80%;" />

<img src="img\20\3.png" alt="3"  />

* GPOST method isn’t recognised causing denial of service scenario.
* Has amazing impact opportunities when chained with other vulnerabilities, like reflected XSS
* It’s new and really cool!



<img src="img\20\4.png" alt="4"  />

* Application responds with XSS Payload, stealing their cookie



### Mitigations

* If you don’t have a CDN, reverse proxy, or load balancers, you are not vulnerable!
* Configure the frontend to exclusively use HTTP/2
* Check Content-Length header value against payload size

