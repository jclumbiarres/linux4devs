```bash
sudo mount --make-rshared /
```

Automatizació amb SystemD:

```toml
[Unit]
Description=Make root filesystem rshared mount
DefaultDependencies=no
After=local-fs.target
Before=docker.service containerd.service podman.service

[Service]
Type=oneshot
ExecStart=/bin/mount --make-rshared /
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Path:
```bash
/etc/systemd/system/mount-rshared.service
```

Enable:
```bash
sudo systemctl enable mount-rshared.service
```

Start:
```bash
sudo systemctl enable mount-rshared.service
```
