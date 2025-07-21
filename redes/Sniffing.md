# Sniffing, tcpdump i Wireshark: Explicació Exhaustiva

## Què és el Sniffing?

El **sniffing** és la tècnica de capturar i analitzar el tràfic de xarxa que circula per una interfície de xarxa. Aquesta pràctica permet veure les dades que s'envien i reben entre dispositius, incloent informació com adreces IP, ports, protocols i, en alguns casos, el contingut dels missatges.

### Tipus de sniffing

- **Passiu:** El sniffer només observa el tràfic sense modificar-lo. És difícil de detectar.
- **Actiu:** El sniffer pot modificar, injectar o redirigir el tràfic. Pot ser detectat més fàcilment.

### Amenaces relacionades amb el sniffing

- **Man in the Middle (MitM):** Un atacant intercepta i possiblement modifica la comunicació entre dos dispositius sense que aquests ho sàpiguen.
- **Robo d'informació:** Captura de credencials, dades personals o informació confidencial.
- **Suplantació d'identitat:** Utilització de la informació capturada per fer-se passar per un altre usuari.

## Què és tcpdump?

`tcpdump` és una eina de línia de comandes per capturar i analitzar paquets de xarxa en sistemes Unix/Linux. Permet veure el tràfic en temps real i aplicar filtres per analitzar només el que interessa.

### Característiques principals de tcpdump

- **Captura de paquets en temps real.**
- **Filtratge avançat** per protocol, IP, port, etc.
- **Exportació de captures** en format `.pcap`.
- **Visualització detallada** de capçaleres de protocols (TCP, UDP, ICMP, etc.).

### Ús bàsic

```bash
sudo tcpdump -i eth0
```
- `-i eth0`: Captura a la interfície `eth0`.

### Filtratge d'exemples

- Captura només tràfic HTTP:
    ```bash
    sudo tcpdump port 80
    ```
- Captura tràfic entre dues IPs:
    ```bash
    sudo tcpdump host 192.168.1.10 and 192.168.1.20
    ```

### Exportar a fitxer

```bash
sudo tcpdump -i eth0 -w captura.pcap
```

## Què és Wireshark?

`Wireshark` és una aplicació gràfica per a l'anàlisi de protocols de xarxa. Permet capturar, visualitzar i analitzar paquets amb una interfície intuïtiva i eines avançades.

### Característiques principals de Wireshark

- **Interfície gràfica** fàcil d'utilitzar.
- **Desglossament detallat** de cada paquet.
- **Filtratge potent** per protocol, IP, port, etc.
- **Exportació i importació** de fitxers `.pcap`.
- **Estadístiques i gràfics** de tràfic.

### Ús bàsic

1. Selecciona la interfície de xarxa.
2. Prem "Start" per començar la captura.
3. Utilitza filtres per analitzar tràfic específic (ex: `http`, `ip.addr == 192.168.1.10`).
4. Examina paquets i protocols amb detall.

### Filtratge d'exemples

- Tràfic HTTP:
    ```
    http
    ```
- Tràfic d'una IP concreta:
    ```
    ip.addr == 192.168.1.10
    ```

## Diferències entre tcpdump i Wireshark

| Característica      | tcpdump                  | Wireshark                |
|---------------------|--------------------------|--------------------------|
| Interfície          | Línia de comandes        | Gràfica                  |
| Filtratge           | Expressions BPF          | Expressions avançades    |
| Exportació          | `.pcap`                  | `.pcap`, `.csv`, etc.    |
| Anàlisi             | Bàsic                    | Detallat i visual        |

## Consideracions de seguretat

- Cal permisos d'administrador per capturar paquets.
- La captura pot exposar dades sensibles.
- Utilitza aquestes eines de manera ètica i legal.
- El sniffing en xarxes alienes sense permís és il·legal.

## Recursos addicionals

- [Documentació oficial de tcpdump](https://www.tcpdump.org/)
- [Documentació oficial de Wireshark](https://www.wireshark.org/docs/)
- [Wireshark: Tutorials i guies](https://wiki.wireshark.org/)
