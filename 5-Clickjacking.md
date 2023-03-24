# Clickjacking



* Usually not a very harmful attack
* Very deceptive to users
* Overlays a UI on top of a target web application to perform operations without authorisation

<img src="C:\Users\cjhm0\Desktop\COMP90074_Notes\img\5\1.png" alt="1" style="zoom:80%;" />

### Remediation

* X-Frame-Options: deny
  * Completely disables loading of a page in a frame
* X-Frame-Options: sameorigin
  * Allow iframes from the same origin only
* X-Frame-Options: allow-from https://www.example.com/
  * Allow from a specific URI