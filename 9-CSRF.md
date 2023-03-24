# Cross-Site Request Forgery (CSRF)

* Cross-Site Request Forgery (some pronounce it as ‘sea-surf’)
* Tricking a user into performing malicious requests
* User’s usually don’t know what is happening
* Occurs when you visit a website controlled by an attacker
* Uses the user’s cookies that are already in the browser
* **User must be authenticated (or have a unique identifier) for this attack to work**
* **Not an injection class vulnerability**
* Example: ING Direct bank has a CSRF vulnerability which allowed an attacker to transfer money, by simply being authenticated within your bank account and visiting the attackers page.

<img src="img\9\1.png" alt="1" style="zoom:80%;" />

### Methods to CSRF

* Via AJAX (requires preflight if any HTTP method other than GET)
* Via HTML form (can only do GET and POST, but doesn’t require preflight)
* You can use JS to submit the form though ;)
* Via flash swf files



### CSRF Mitigations

* Using CSRF tokens:

  * Unpredictable with high entropy, as for session tokens in general.

  * Tied to the user's session.

  * Strictly validated in every case before the relevant action is executed.

  * Dynamic per load of any page

  * Impossible to predict

* Additional to the CSRF token, whitelist specific referrers only (if allowed by business cases)
* Only allow trusted origins!
  * Don’t do: `Access-Control-Allow-Origin: *`

