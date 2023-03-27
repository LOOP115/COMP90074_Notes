# OS Command Injection



### Definition

* Also known as command injection
* Another type of injection attack
* Once again, overly trusted and not properly sanitised user input
* Injecting operating system commands as user input



### Example

##### Script to unzip user uploaded files:

```
import os
user_input = web.input()
os.system(“unzip “ + user_input)
```

##### Legit input:

```
hello.zip
```

##### Malicious input:

```
hello.zip; whoami; #
```

unzip hellp.zip and run whoami



### Mitigations

* Validating against a whitelist of permitted values.
* Validating that the input is a number (if input is expecting numbers)
* Validating that the input contains only alphanumeric characters, no other syntax or whitespace.
* Don’t allow user input to reach an operating system command! Rearchitect the software to avoid this! You are asking for trouble!