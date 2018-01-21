
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
``` ServerAliveInterval 100 ```

#### Terminal and vim debug info
Test terminal speed
``` Bash
time seq -f 'blah blah %g' 100000
```
Print out colors used in vim
``` vim
:so $VIMRUNTIME/syntax/hitest.vim
```
Print used colorscheme
:color

rint colorgroups
:hi

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczMDAzNzM2MCwtNjUzNzc2MjY2XX0=
-->