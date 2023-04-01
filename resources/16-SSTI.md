# Server-Side Template Injection



### Backend

* Resources typically not visible to the public and users
* Usually resources that hold information related to users
* Can be like a database

### Frontend

* Resources typically visible to the public and users
* Usually the pretty part of the application
* Typically will contain HTML, CSS, JS, etc. for websites



### Template Engine

* Software used to render templates easily
* Considered a safe(?) way to process information and fit data from the backend into pages in the front end
* Some features:
  * Variables and functions execution
  * Text replacement
  * Reusable file inclusions
  * Conditional logic and loops
  * Can provide XSS filters and protections
  * Unfortunately, not idiot proof
* For details on how to exploit these bugs to the utmost extent:
  * https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection



### Jinja2

```python
@app.route("/page")
def page():
    name = request.values.get('name')
    output = Jinja2.from_string('Hello ' + name + '!').render()
    return output
```

#### Legit request:

```
$ curl -g https://example.com/page?name=sajeeb
Hello sajeeb! Welcome to example.com!
```

#### Malicious request:

```
$ curl -g https://example.com/page?name=sajeeb{{7*7}}
Hello sajeeb49! Welcome to example.com!
```



### How to test for SSTI

* Attempt to input values within formula placeholders like:
  * `$x`
  * `{{ value here }}`

* I recommend forming multiple unique detection strings, aiming to decrease false positives, like:
  * Input: hello {{123456*555}}
    Output: hello 68518080
  * Input: hello {{31337*111}}
    Output: hello 3478407
  * Input: hello {{‘7’ * 7}}
    Output: hello 7777777



### Exploiting SSTI in the wild

* Follow these steps:
  * Detect the vulnerability
  * Verify the vulnerability exists
  * Identify which engine is in use (you can use something like tplmap)
  * Build your exploit (attempt to show highest impact)



### Mitigations

* Don’t allow users to input information directly into a template
* Always sanitise user input
* Use a WAF