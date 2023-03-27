# Log Injection



### Definition

* Another type of injection attack
* Once again, overly trusted and not properly sanitised user input
* Injecting malicious information into a server’s logs
* Later attempting to access the server’s log externally, triggering the vulnerability
* Usually causes XSS, information leakage, or RCE
* Can chain with code injection really well to gain RCE

(SIEM)

<img src="C:\Users\cjhm0\Desktop\COMP90074_Notes\img\14\1.png" alt="1" style="zoom:80%;" />

#### Log injection chained

<img src="C:\Users\cjhm0\Desktop\COMP90074_Notes\img\14\2.png" alt="2" style="zoom:80%;" />



### Mitigation

* Don’t expose logs to a user. They shouldn’t need to ever see them!
* Sanitise user input prior to storing in the log
* Don’t allow the user to control the path / file name of the log