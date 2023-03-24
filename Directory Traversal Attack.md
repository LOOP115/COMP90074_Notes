## Directory Traversal Attack

* Allowing a user to control a file’s name / location, may allow them to traverse to different directories
* Injection class vulnerability
* Can be simple to exploit (in cases), however can require knowledge of the underlying file system
* Can lead to severe cases of information disclosure

* Example:
  * http://example.com/?download=test.txt
  *  Shows the contents of test.txt
  * http://example.com/?download=../../../../etc/passwd
  * Shows the contents of /etc/passwd



### Local File Inclusion (LFI)

* Allowing a user to specify which file to import
* Another injection type vulnerability
* Including local files only
* May require the attacker to know where files are located on the server’s file system
* This can sometimes be identified with information leakages
* Can use directory traversals to your advantage
* Can lead to severe information disclosure, or even code injection
* Can use different protocols to your advantage
* Example:
  * file:// - access files on the server
  * php://filter – used to encode information
  * phar:// - used to load phar files
  * zip:// - used to unzip a file on the fly
  * Only file:// and php:// will be used in examinable tasks (may be in the exam / assignments)

#### Example & Attack

```
<?php
if (isset($_GET['language'])) {
include($_GET['language'] . '.php');
}
?>
```

Legit example: https://example.com/login.php?language=english.php

* Output: English version of the website\
* Legit example: https://example.com/login.php?language=../user/upload/exploit
  * In PHP, string becomes: include(‘../user/upload/exploit.php');
  * Output: executes whatever code is within exploit.php
  * Can result in complete takeover of the web sever



LFI ZIP Attack example

zip://../../../user/uploads/saj.zip#style

#: reference to style.css