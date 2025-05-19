
Rutes absolutes: Cron no reconeix rutes relatives. Sempre posa la ruta completa:​

0 4 * * * /home/usuari/scripts/backup.sh # ✅ Correcte ​  
0 4 * * * backup.sh     # ❌ Error (no trobarà el script) ​

Variables d'entorn: Cron no carrega el teu entorn per defecte. Si necessites variables, defineix-les al propi script o al crontab.​​

Registres (logs): Redirigeix la sortida per depurar errors:
0 5 * * * /ruta/script.sh > /ruta/log.log 2>&1 ​

Permisos: Assegura't que el script és executable:​
chmod +x /ruta/script.sh ​