
  

#  Obfuscation 


### OBF100
By navigate to view-source:https://obf100.secu-web.blackfoot.dev/ we can see the js code.
By copy pasting the code into this site https://lelinhtinh.github.io/de4js/, we have a human-readable result.
According to the result of deobfuscator, just need to enter "ggez" and the flag is served.

### SCRIPT_KIDDING
The goal here was to catch the script then reverse it and use it to get the flag.
By navigate to this page https://script-kidding.secu-web.blackfoot.dev/?showbackdoor we get the code executed. 
By adding the code line echo(gzinflate(base64_decode($a))), we have the human-readable version.
I use a PHP process on my pc to launch the code in local and print hints by for debugging.
Next, the step is to understand it and use it to make a command and get the flag.
I understand that we can use it by post or cookie way.
I opt for the cookie way. 
After some test and debug I understood the name of the cookie was "4ef63abe-1abd-45a6-913d-6fb99657e24b" and the value was a readable PHP strings containing specific json information.
In the json is attempted to get a property called "e" and the value of the property is the command we want to execute. 
The command have to be a base64 strings.
By using this command, we get the flag.
```var_dump(exec('cat * | xargs'));```
```
Name :
4ef63abe-1abd-45a6-913d-6fb99657e24b
```

```
Value:
YTozOntzOjI6ImFrIjtzOjE6ImkiO3M6MToiYSI7czoxOiJlIjtzOjE6ImQiO3M6MzI6InZhcl9kdW1wKGV4ZWMoJ2NhdCAqIHwgeGFyZ3MnKSk7Ijt9```