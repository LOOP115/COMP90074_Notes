# Cross-Origin Resource Sharing (CORS)

* Q1. Can you run an XSS payload and use ajax cross domain (XSS on google.com, AJAX to yahoo.com)?
  * A1. No, due to protection in the browser
* Q2. Can you do AJAX requests from your own website to any other website?
  * A2. No, due to protections in the browser
* Q3. Why is clickjacking ever needed?
  * A3. As you can’t do AJAX to everything, due to protections in the browser

### CORS

* Cross-Origin Resource Sharing
* Mechanism used by browsers to restrict interaction with other websites
* Is used as a security mechanism protecting against malicious AJAX requests
* Can require pre-flight request in some cases
* Allows websites to specify who can interact using AJAX requests

<img src="img\8\1.png" alt="1" style="zoom:80%;" />

#### Preflight

<img src="img\8\2.png" alt="2" style="zoom:80%;" />

#### Main

<img src="img\8\3.png" alt="3" style="zoom:80%;" />