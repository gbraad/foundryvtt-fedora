Install Foundry VTT on Fedora
=============================



Foundry VTT
-----------

  1. download archive
  2. `unzip [archive].zip -d /opt/foundryvtt`
  3. `mkdir ~/foundrydata`
  4. add systemd unit

`/etc/systemd/system/foundryvtt.service`
```
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

```
$ systemctl enable foundryvtt
$ systemctl start foundryvtt
```