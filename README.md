# Homeserver setup
## Terminal and vim

### Keep ssh connection alive (on client side)
``` Bash
sudo vi /etc/ssh/ssh_config
```
Insert
``` ServerAliveInterval 100 ```

``` Bash
#### Test terminal speed

time seq -f 'blah blah %g' 100000

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI5MDU2NDAzNSwtNjUzNzc2MjY2XX0=
-->