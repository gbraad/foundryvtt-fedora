Install Foundry VTT on Fedora
=============================



Foundry VTT
-----------

  1. download archive
  1. `unzip [archive].zip -d /opt/foundryvtt`
  1. `mkdir ~/foundrydata` (optional: if run as systen service)
  1. `dnf install nodejs`


### Install as a system service

`/etc/systemd/system/foundryvtt.service`
```ini
[Unit]
Description=Foundry VTT service
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1
User=[username]
ExecStart=/usr/bin/env node /opt/foundryvtt/resources/app/main.js --dataPath=/home/[username]/foundrydata

[Install]
WantedBy=multi-user.target
```

```shell
$ systemctl enable foundryvtt
$ systemctl start foundryvtt
```


### Install as a user service

```shell
$ loginctl enable-linger [username]
```

`~/.config/systemd/user/foundryvtt.service`
```ini
[Unit]
Description=Foundry VTT service

[Service]
Type=simple
Restart=always
RestartSec=1
ExecStart=/usr/bin/env node /opt/foundryvtt/resources/app/main.js --dataPath=/home/[username]/.local/share/FoundryVTT
```

```shell
$ systemctl --user start foundryvtt
$ systemctl --user status foundryvtt
```

Note: for the dekstop application the path is `"/home/[username]/.local/share/FoundryVTT"`


### After install

You can now start the Foundry VTT setup and registration by navigating to the server as http://[ip]:30000.

Note: it is suggested to run this behind a proxy, like Apache, nginx or caddy, so you do not expose the node service directly to the Internet. An alternative that I use is Tailscale (or Zerotier) to only share the server on a shared virtual network.