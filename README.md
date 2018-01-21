# Homeserver setup
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
``` ServerAliveInterval 100 ```

#### Test terminal speed
``` Bash
time seq -f 'blah blah %g' 100000
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM3NzM2OTk1LC02NTM3NzYyNjZdfQ==
-->