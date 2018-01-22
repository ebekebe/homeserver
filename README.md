
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
```
ServerAliveInterval 100
```

### _Terminal and vim debug info_
#### Test terminal speed in bash
``` Bash
time seq -f 'blah blah %g' 100000
```
#### Print out colors used in vim
``` vim
:so $VIMRUNTIME/syntax/hitest.vim
```
#### Print used colorscheme in vim
``` vim
:color
```
#### Print colorgroups used in vim
``` vim
:hi
```
#### Print terminal  colortheme colors
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
```
### Install colortheme for windows WSL
Download colortool to c:\utils\colortool
https://github.com/Microsoft/console/

Download and copy c:\utils\colortool\schemes
https://github.com/mbadolato/iTerm2-Color-Schemes/raw/master/schemes/Builtin%20Dark.itermcolors
Execute in cmd.exe:
```colortool.exe -b Builtin_dark```

### Set up neovim and colortheme
Choose colortheme base16 here:
http://chriskempson.com/projects/base16/
#### Install neovim and  “plug” plugin manager
``` Bash
sudo apt install neovim
curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```






<!--stackedit_data:
eyJoaXN0b3J5IjpbNDYxMTM5OTIyLC02NTM3NzYyNjZdfQ==
-->