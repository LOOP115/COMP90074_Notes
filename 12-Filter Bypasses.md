# Filter Bypasses

### Definition

* Like coffee filters! They take out the bad stuff
* Removing the of the user’s input that don’t seem right
* Can be done using regexes or any kind of string matching
* Plenty of packages that help implement this
* This is not a good mitigation for most vulnerabilities
* We will be learning how to bypass this, for our advantage!
* We won’t be discussing XSS auditors as they are ancient now (as of last year, no longer used)

<img src="img\12\1.png" alt="1" style="zoom:80%;" />

### Example 1

<img src="img\12\2.png" alt="2" style="zoom:80%;" />

```
Example Python code:
if "<script>" in user_input:
	user_input = user_input.replace("<script>", "")
print("user_input")

Example input:
user_input = "hello<script>world"

Script output:
helloworld
```

#### Bypassing the filter

```
Example input:
user_input = "hello<scri<script>pt>world"

Script output:
hello<script>world (Still Malicious)
```

### Example 2 (Fix error in example 1)

<img src="img\12\3.png" alt="3" style="zoom:80%;" />

```
Example Python code:
while "<script>" in user_input:
	user_input = user_input.replace("<script>", "")
print("user_input")

Example input:
user_input = "hello<scri<script>pt>world"

Script output:
helloworld
```

#### Bypassing the filter

```
Example input:
user_input = "hello<img>world"

Script output:
hello<img>world
```



### Why do we care about filters

* Filters are very common
* False sense of security for developers
* Bypassing can be easy exploitation
* Filtering is not only for XSS. We will likely run into it for all kinds of injection attacks!
* Great for bug bounties, as low-skilled attackers will miss bypasses



### Best ways to bypass filters

* See and understand what you are dealing with
* Analyse the response from the server
* Use a bypass cheatsheet like Rsnake’s or OWASPs:
  * https://owasp.org/www-community/xss-filter-evasion-cheatsheet



### Client-side filters

* Great for user experience (UX)
* Completely useless for security
* Can be bypassed using Inspect Element

#### Example

```
Example email field:
<input type=“email” name=“email”>
```

Tells browser to use a regex to deny all input that aren’t in the format of a valid email

Right-click, use inspect element. Change the type into text (type=“text”) and voila, bypassed!

Even easier if you use a proxy like BurpSuite!