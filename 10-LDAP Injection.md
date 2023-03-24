# LDAP Injection



### LDAP

* Lightweight Directory Access Protocol
* Helps with sharing information about users, servers, networks, services, etc.
* Like WhitePages, with phone numbers, home addresses, etc.
* Commonly used to authenticate users and validate privileges
* Stores user’s credentials (username, password)



### LDAP Injection

* Very similar to SQLi
* Manipulating LDAP queries to do what you want
* This is not a very prevalent vulnerability but is good to know.
* Not going to be a big focus for us.

#### Example

```
String filter = “(&(USER = ” + user_name + “) (PASSWORD = “ + user_password + “))”;
```

Legit input:

```
https://example.com/login?user=sajeeb&password=pass
```

Variable value:

```
“(&(USER = sajeeb) (PASSWORD = pass))”;
```

Malicious input:

```
https://example.com/login?user=sajeeb)(%26))&password=pass
```

Variable value:

```
“(&(USER = sajeeb)(&))) (PASSWORD = pass))”;
```

(&) is a tautology and will authenticate as user sajeeb



### Mitigations

* Validate input
* Encode the user’s input
* Harden directory authorisations (use the principle of least privilege)