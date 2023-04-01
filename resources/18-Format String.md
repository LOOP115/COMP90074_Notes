# Format String Attacks



### Format Printing

* Printing command / function provided by the language
* Makes printing easier for the developer
* Allows the developer to specify the data type of the variable and the location within the print string
* Developers can use this to print strings, integers, memory locations, etc.
* Example in C:
  * `printf("my name is : %s\n", “Sajeeb")`



### Format String Attack

* Occurs due to unsantised user input reaching a format printing command
* Misusing the ability to control what placeholders are kept in the string to be formatted
* Can cause:
  * Denial of service scenerios (due to long processing time or attempting to access protected memory)
  * Information leakage (this can aid in creating an exploit against systems with ASLR)
  * e.g. `./format %p%p%p%p%p%p`



### Mitigations

* Never let a user control a print statement that has the ability to format
* Default to %s if you can
* Validate input to ensure ‘%’ isn’t entered