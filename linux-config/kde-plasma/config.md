# Config KDE Plasma Autologin

1. Open `sddm.conf` with nano

```bash
sudo nano /etc/sddm.conf
```

2. Add config for Autologin

```.conf
[Autologin]
User=juan
Session=plasma.desktop
```
