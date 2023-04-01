# HTTP Splitting (Smuggling)



### CRLF

* Carriage Return Line Feed
* Characters: \r\n
* URL Encoded: %0d%0a
* Used to terminate a line
* Can be used maliciously to split a response



### HTTP Splitting

* This attack has many different names like:
  * HTTP splitting
  * Carriage Return Line Feed (CRLF) attack
* It is basically splitting the response from a server maliciously, using the attacker’s input
* Usually found in unsanitised user input, reflected within the response
* Commonly found within cookies, redirection URLs, etc.

<img src="img\19\1.png" alt="1" style="zoom:80%;" />

<img src="img\19\2.png" alt="2" style="zoom:80%;" />



### HTTP Splitting to steal cookies

**XSS**: `%0d%0a%0d%0a<script>alert(document.cookie)</script>`



### Mitigations

* Sanitising user input
* Filtering user input to ignore \r\n and %0d%0a
* Using WAFs