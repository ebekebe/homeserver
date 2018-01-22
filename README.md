
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
``` ServerAliveInterval 100 ```

### _Terminal and vim debug info_
Test terminal speed
``` Bash
time seq -f 'blah blah %g' 100000
```
Print out colors used in vim
``` vim
:so $VIMRUNTIME/syntax/hitest.vim
```
Print used colorscheme
``` vim
:color
```
Print colorgroups
``` vim
:hi
```
Print terminal  colortheme colors
``` Bash
#!/bin/bash

#Terminal color table printout

T='gYw'   # The test text

echo -e "\n                 40m     41m     42m     43m\
     44m     45m     46m     47m";

for FGs in '    m' '   1m' '  30m' '1;30m' '  31m' '1;31m' '  32m' '1;32m' '  33m' '1;33m' '  34m' '1;34m' '  35m' '1;35m'  '  36m' '1;36m' '  37m' '1;37m';
  do FG=${FGs// /}
  echo -en " $FGs \033[$FG  $T  "
  for BG in 40m 41m 42m 43m 44m 45m 46m 47m;
    do echo -en "$EINS \033[$FG\033[$BG  $T  \033[0m";
  done
  echo;
done
echo
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MTQ4MzEzNjksLTY1Mzc3NjI2Nl19
-->