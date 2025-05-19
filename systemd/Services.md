
```toml
[Unit]
Description=Servidor web NGINX
After=network.target

[Service]
ExecStart=/usr/bin/nginx
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
- \[Unit\]: Descripció i dependències (per exemple, que s’iniciï després de la xarxa).​
- \[Service\]: Com executar el servei.​
- \[Install\]: On s’habilita el servei.​
