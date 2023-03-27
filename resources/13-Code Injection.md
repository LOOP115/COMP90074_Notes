# Code Injection



### Definition

* Another type of injection attack (we are getting close to finishing a majority of them!)
* Once again, overly trusted and not properly sanitised user input
* Injecting code that is interpreted and executed by the application (in our case, on the server, however this may differ for thick clients)
* This attack can also be blind (you cannot see output from the server)
* For blind attacks, always remember to try introduce either time delays (sleeps) or external server interaction!



### Example

```
def GET(self):
	# Capture parameters
	get_input = web.input()
	# Assign the value of the param1 parameter to param1
	param1 = get_input['param1'] if 'param1' in get_input else None
	# If param1 exist, eval it
	if (param1):
		x = eval(param1) <- Malicious payload executes here
	return "I'm Vulnerable"

https://example.com/command?param1=print(“hello”)
Output: “helloworldthis is sajeeb” is somewhere in the response
```



### Remote Code Execution (RCE) using code injection in python

```
Execute commands in python, using a single line of code:
__import__(‘os’).system(‘COMMAND’)

Sleep for 5 seconds in python, using a single line of code:
__import__(‘time’).sleep(5)

To import a package in python code, within a single like, using the magic function __import__
```



### Mitigation

* Simply don’t evaluate whatever a user inputs! (this is the preferred)
  * In other words, use functions in a smart manner like using a package specifically built for such interactions
* Validate user input (not a good method)
* Sanitise or encode user input (usually a good method, but not in this case!)
* Use a WAF