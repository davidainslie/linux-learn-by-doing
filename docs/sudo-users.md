# Sudo Users

```shell
sudo useradd -m gfreeman
sudo useradd -G wheel -m avance
```

```shell
sudo passwd gfreeman
# We'll provide the password: LAsudo321

sudo passwd avance
```

```shell
sudo visudo
```
We added `avance` to the group `wheel` who can run anything when `sudo` - We see the following in `visudo`:
```shell
## Allows people in group wheel to run all commands
%wheel  ALL=(ALL)       ALL
```

Let's `switch` (`su`: substitute user) to the user `avance` using `-` for a login shell:

```shell
cloud_user@ip-10-0-1-171 ~]$ sudo su - avance
[sudo] password for cloud_user:
[avance@ip-10-0-1-171 ~]$
```

User `avance` cannot view the file `/etc/shadow` but can sudo to raise their priviledge:
```shell
[avance@ip-10-0-1-171 ~]$ sudo cat /etc/shadow
[sudo] password for avance:

root:$6$SxRDOWvnv$gNp3s9H2h4nrk1/jKv5Z1emy9G7vF2I/ObDqhDCeC3Maxrr8bqkgfOTpKFzEAL9qhNyILzwxbCBJb9q9rACv/.:19230:0:99999:7:::
bin:*:17110:0:99999:7:::
daemon:*:17110:0:99999:7::
...
```

Next, we'll make `gfreeman` a web system administrator who can start/stop servers.
We'll create a new `sudoers` file:
```shell
sudo visudo -f /etc/sudoers.d/web_admin
```
and add the following:
```shell
Cmnd_Alias WEB = /bin/systemctl restart httpd.service, /bin/systemctl reload httpd.service

gfreeman ALL=WEB
```
Now log into the `gfreeman` account:
```shell
[cloud_user@ip-10-0-1-171 ~]$ sudo su - gfreeman
[gfreeman@ip-10-0-1-171 ~]$
```
Attempt to restart the web service:
```shell
sudo systemctl restart httpd.service
```