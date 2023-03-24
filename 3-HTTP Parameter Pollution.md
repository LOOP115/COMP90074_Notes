# HTTP Parameter Pollution



* Causes applications to misinterpret parameters provided

* Can bypass input validation using it

* Majorly depends on web technologies in use

* Example of how applications handle parameter pollution:

  | Web Application Server Backend | Parsing Result                            | Example               |
  | ------------------------------ | ----------------------------------------- | --------------------- |
  | ASP.NET / IIS                  | All occurrences concatenated with a comma | color = red,blue      |
  | ASP / IIS                      | All occurrences concatenated with a comma | color = red,blue      |
  | PHP / Apache                   | Last occurrence only                      | color = blue          |
  | Python / Zope                  | All occurrences in List data type         | color = ['red','blue] |

  

### Example in real life - Blogger

```
POST /add-authors.do HTTP/1.1

security_token=attackertoken&blogID=attackerblogidvalue&blogID=victimblogidvalue&authorsList=goldshlager19test%40gmail.com(attacker email)&ok=Invite
```

First was used for authorisation checks, second used for actual operation

Impact was “Severe”, providing the ability to take over another user’s blog without permission.



### Remediation

* Check the number of parameters you get
* Ensure that you do not assume data type of input (ever!)



### How to Test for HTTP Parameter Pollution

* http://example.com/?q=kittens
  * Output should be kittens
* http://example.com/?mode=admin&q=kittens&num_results=100
  * Output should be kittens
* http://example.com/?mode=admin&q=kittens&num_results=100&q=puppies
  * If vulnerable, output will be puppies or cause an error