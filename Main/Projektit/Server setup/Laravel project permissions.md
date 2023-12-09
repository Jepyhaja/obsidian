## Default setup

Rquires user with group www-data [[add user to www-data group]]

Navigate to project root, for example: `/var/www/project/`

```bash 
sudo chown -R $USER:www-data .
```  
to change owner of all files and directories to current user and www-data group.

```bash
sudo find . -type f -exec chmod 664 {} \;
```
to change permissions of all files.

```bash
sudo find . -type d -exec chmod 775 {} \;
``` 
to change permissions of all directories

give www-data rights read, write and execute to storage and bootstrap/cache
```bash
sudo chgrp -R www-data storage 
```
```bash
sudo chgrp -R www-data bootstrap/cache 
```
```bash
sudo chmod -R ug+rwx storage
```
```bash
sudo chmod -R ug+rwx bootstrap/cache
```


