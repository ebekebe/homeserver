
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
``` ServerAliveInterval 100 ```

#### Terminal tests
Test terminal speed
``` Bash
time seq -f 'blah blah %g' 100000
```
Print out colors used in vim
``` vim
:so $VIMRUNTIME/syntax/hitest.vim
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg3MDEyNzAxMywtNjUzNzc2MjY2XX0=
-->