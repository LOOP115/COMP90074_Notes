# Buffer Overflows



### Buffer

* Temporary memory storage location
* Sometimes holds information during transaction from one area to another



### Buffer Overflow

* One of the first digital hacking techniques created
* It is the act of overfilling a buffer until you overwrite memory locations, causing changes to the application flow
* Typically we attempt to take over EIP as it gives us control of the programs execution flow

<img src="img\17\1.png" alt="1" style="zoom:67%;" />

<img src="img\17\2.png" alt="2" style="zoom: 80%;" />

<img src="img\17\3.png" alt="3" style="zoom:80%;" />

<img src="img\17\4.png" alt="4" style="zoom:80%;" />



### Detect

* Very easy to detect using source code analysis (if you have source code)
* Look for a strcpy or equivalent without bounds checking / length checking
* Otherwise, input large payloads into the application (like 1000 ‘A’s)
* People choose the letter A for detection as it is simple to remember \x41 is the hex representation of A
* e.g. `gcc -fno-stack-protector`



### Mitigations

* Using Address Space Randomisation (ASLR) to randomise the addresses of memory locations
  * It is still possible to bypass these protections, however it is a bit harder (and annoying)
* Using Data Execution Prevention (DEP) to ensure certain areas of memory are not able to execute.
  * Typically this is enforced upon user input regions.
* Bounds checking and copying of information with length checks. This ensures that more information than expected is not being handled, mitigating the issue.

