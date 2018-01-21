
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzM3NzU5MjIsLTY1Mzc3NjI2Nl19
-->