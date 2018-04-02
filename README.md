# zimbraUbuntuDistUpgrade
Easy steps to upgrade Ubuntu with Zimbra

We start Ubuntu dist-upgrade on VMWare 6.5 ESXi.
A.- Snapshot the VM in VCSA 

1.- Stop zimbra
```
/etc/init.d/zimbra stop
```
2.- Make the necessary steps so that make the dist-upgrade
```
apt-get update && sudo apt-get upgrade
apt-get install update-manager-core
do-release-upgrade
```
3.- Enable the zimbra's third party resources when the upgrade asks about it. Of course, in other session.
```
Third party sources disabled

Some third party entries in your sources.list were disabled. You can re-enable them after the upgrade with the 'software-properties' tool or your package manager.
```
Open other session (screen -R)

```
# deb [arch=amd64] https://repo.zimbra.com/apt/87 xenial zimbra # disabled on upgrade to xenial
# deb-src [arch=amd64] https://repo.zimbra.com/apt/87 xenial zimbra # disabled on upgrade to xenial
```

to

```
deb [arch=amd64] https://repo.zimbra.com/apt/87 xenial zimbra # disabled on upgrade to xenial
deb-src [arch=amd64] https://repo.zimbra.com/apt/87 xenial zimbra # disabled on upgrade to xenial
```

4.- In my case, the VM appears with ens160 as interface name, I changed the udev files in order to get eth0 as interface name.
I've followed the next steps, [link here](https://github.com/unai-ss/linux-udev-network-modify)

5.- After the recovering of the network interfaces
```
su  zimbra
zmcontrol status
zmcontrol start
```

