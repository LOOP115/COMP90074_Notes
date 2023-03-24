# Tabnapping

* The equivalent of kidnapping a tab within a web browser
* Not a very well-known exploit
* Allows an attacker to:
  * Close tabs
  * Change a tabs location (URL it visits)
  * Perform phishing



### Example

```
<a href="https://0dd.zone" target="_blank">0dd Zone</a>
```

* If an attacker controls the landing page (https://0dd.zone), they can perform this attack.
* Using window.opener object to your advantage
* window.opener.location.replace("https://0dd.zone")
* Depending on browser: window.opener.close()



### Remediation

* Set the attributes rel="nofollow noopener noreferrer"
* Don’t use target=“\_blank”
* For example:

```
<a href=“http://google.com“ rel="nofollow noopener noreferrer" target=“_blank”>Google</a>
<a href=“http://google.com” target=“_parent”>Google</a>
```