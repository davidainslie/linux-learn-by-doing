# Managing Users

- Add `tstark`, `cdanvers`, `dprince`.
- Create `superhero` group.
- Make `tstark` a `superuser` by replacing his group with `wheel`.
- Add our users to `superhero`.
- Lock `dprince` as she has temporarily left to fight evil.

```shell
ssh cloud_user@54.87.241.128
```

```shell
[cloud_user@ip-10-0-1-10 ~]$ useradd tstark
useradd: Permission denied.
.
[cloud_user@ip-10-0-1-10 ~]$ sudo -i
[sudo] password for cloud_user:

[root@ip-10-0-1-10 ~]# useradd tstark
[root@ip-10-0-1-10 ~]# useradd dprince
[root@ip-10-0-1-10 ~]# useradd cdanvers
```

```shell
[root@ip-10-0-1-10 ~]# groupadd superhero
```

```shell
[root@ip-10-0-1-10 ~]# usermod -g wheel tstark

[root@ip-10-0-1-10 ~]# id tstark
uid=1002(tstark) gid=10(wheel) groups=10(wheel)
```

```shell
[root@ip-10-0-1-10 ~]# usermod -aG superhero tstark
[root@ip-10-0-1-10 ~]# usermod -aG superhero dprince
[root@ip-10-0-1-10 ~]# usermod -aG superhero cdanvers
```

```shell
[root@ip-10-0-1-10 ~]# id cdanvers
uid=1004(cdanvers) gid=1004(cdanvers) groups=1004(cdanvers),1005(superhero)
```

```shell
[root@ip-10-0-1-10 ~]# usermod -L dprince
```