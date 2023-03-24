# Cross-Site Scripting (XSS)



### User input

* Literally anything the user can control
* Examples:
  * IP addresses
  * Hosts
  * Cookies
  * Local storage
  * GET parameters
  * POST parameters
  * And many, many other things.



### Cross-Site Scripting (XSS)

* Execution of JavaScript within the client’s browser
* Attacker’s aim is to:
  * Steal cookies
  * Steal DOM
  * Steal localStorage
  * Manipulate AJAX calls to perform unauthorised operations (sending requests as the user)
* It uses the victim’s session tokens

#### Reflected XSS

<img src="img\2\1.png" alt="1" style="zoom:80%;" />



#### Stored XSS

<img src="img\2\2.png" alt="2" style="zoom:80%;" />



#### DOM XSS

<img src="img\2\3.png" alt="3" style="zoom:50%;" />



#### Injection Point

* Any place where a user can control input and inject their own malicious content, which is sent to the
  server

#### JavaScript (JS) Frameworks XSS

* e.g. AngularJS
* Acts as a client-side templating framework
* Aids with making the application seem more like a Single Page Application (SPA)
* Possible execution can be tested with the following test case:
  * Input: {{ 7 * 7 }}
  * Output: 49
* Note: This is client-side only



### Cookie/DOM/LocalStorage Stealing

<img src="img\2\4.png" alt="4" style="zoom:80%;" />

### XSS AJAX Calls

<img src="img\2\5.png" alt="5" style="zoom:80%;" />

### XSS Remediation

* Filtering using regex or strings (do not do this!)
* WAF (not really a remediation, but an extra layer)
* HTML encoding
* Content Security Policy
* X-XSS-Protection Header

#### Regexes

```
((alert|on\w+|function\s+\w+)\s*\(\s*(['+\d\w](,?\s*['+\d\w]*)*)*\s*\))|(<(script|iframe|embed|frame|frameset|object|img|applet|body|html|style|layer|link|ilayer|meta|bgsound))
```

Regexes I have seen used in real life. This is a TERRIBLE idea as people can bypass it using encoding tricks,
etc.

#### WAF

* Web Application Firewall
* Uses a set of rules called policies
* Protects against vulnerabilities by filtering malicious behaviour
* Can be useful to protect against hard-to-patch vulnerabilities
* Examples: Cloudflare, Akamai, F5
* Not a defence mechanism you use on its own
* Can be very easy to bypass

#### Encoding

* Converting information from one character representation to another

* Things like MP3, MP4, FLAC, etc.

* We will mainly be looking into:

  * URL encoding

  * Base64 encoding

  * HTML encoding

    * Shows up in the browser as the actual character (visually)

    * In the source code, displays as the encoded value

    * | Character | HTML Encoded |
      | --------- | ------------ |
      | &         | \&amp;       |
      | <         | \&lt;        |
      | >         | \&gt;        |
      | ''        | \&quot;      |
      | '         | \&apos;      |

#### Content Security Policy (CSP)

* Security mechanism dictated by the server, but enforced by the browser
* Browser complies with the server’s specification
* Declaration of approved sources of origin for content
* Used to mitigate XSS constantly
* Examples:
  * Content-Security-Policy: default-src 'self’ – own website only (no subdomains)
  * Content-Security-Policy: default-src 'self' *.trusted.com – all subdomains
  * Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com media2.com; script-src userscripts.example.com
  * Content-Security-Policy: default-src 'self'; report-uri http://reportcollector.example.com/collector.cgi - catching violations

#### X-XSS-Protection Header

* Enforced by the server
* Browser attempts to comply
* Used to ask browsers to enforce XSS auditor protections
* Loads page in a sandbox
* If it detects XSS on a page, it blocks the page from loading
* Bypassing used to be considered a sport
* Not present anymore in Chrome and Firefox (majorly deprecated)



### XSS Filter Bypasses

1. How do you bypass a filter stripping \<script> from the string
   A. Use a different HTML tag
   B. Do something like <scr\<script>ipt> (output will be \<script>)

2. How do you bypass a filter on \<img> and \<script>?
   A. Use a different tag like video

3. How do you bypass a filter for < ?
   A. Check and see if you can find an injection point within JS code, which can be used to your advantage!
   E.g. var name = “user’s_name_goes_here”;

