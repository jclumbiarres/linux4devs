# Tipus de Xarxes

Les xarxes informàtiques es classifiquen segons la seva extensió geogràfica i la seva funcionalitat. A continuació s'explica cada tipus principal de xarxa i les capes implicades segons el model OSI.

## Xarxa LAN (Local Area Network)

Una LAN connecta dispositius dins d'una àrea geogràfica petita, com una oficina, escola o edifici. Permet compartir recursos com impressores, fitxers i connexió a Internet.

**Capes implicades:**
- **Capa física:** Cables, switches, routers.
- **Capa d'enllaç de dades:** Ethernet, Wi-Fi.
- **Capa de xarxa:** IP per a la comunicació entre dispositius.

## Xarxa WAN (Wide Area Network)

Una WAN cobreix una àrea geogràfica extensa, com ciutats, països o continents. Connecta diverses LANs mitjançant línies dedicades, fibra òptica o connexions satèl·lit.

**Capes implicades:**
- **Capa física:** Fibra òptica, línies telefòniques, satèl·lit.
- **Capa d'enllaç de dades:** Protocols com PPP, Frame Relay.
- **Capa de xarxa:** IP, MPLS per a la gestió del tràfic.

## Xarxa MAN (Metropolitan Area Network)

Una MAN cobreix una ciutat o una àrea metropolitana. S'utilitza per connectar diverses LANs dins d'una mateixa ciutat.

**Capes implicades:**
- **Capa física:** Fibra òptica, cables coaxials.
- **Capa d'enllaç de dades:** Ethernet, FDDI.
- **Capa de xarxa:** IP.

## Xarxa PAN (Personal Area Network)

Una PAN connecta dispositius personals en una àrea molt reduïda, com un ordinador, telèfon mòbil i impressora.

**Capes implicades:**
- **Capa física:** Bluetooth, USB.
- **Capa d'enllaç de dades:** Bluetooth, Zigbee.
- **Capa de xarxa:** IP (en alguns casos).

## Xarxa WLAN (Wireless Local Area Network)

Una WLAN és una LAN sense fils, utilitzant tecnologies com Wi-Fi per connectar dispositius dins d'una àrea local.

**Capes implicades:**
- **Capa física:** Ones de ràdio.
- **Capa d'enllaç de dades:** Wi-Fi (IEEE 802.11).
- **Capa de xarxa:** IP.

---

## Model OSI i les Capes

El model OSI (Open Systems Interconnection) defineix set capes per la comunicació en xarxes:

1. **Capa física:** Transmissió de bits per mitjà físic.
2. **Capa d'enllaç de dades:** Comunicació entre nodes adjacents.
3. **Capa de xarxa:** Adreçament i encaminament de paquets.
4. **Capa de transport:** Transferència fiable de dades.
5. **Capa de sessió:** Gestió de sessions entre aplicacions.
6. **Capa de presentació:** Format i encriptació de dades.
7. **Capa d'aplicació:** Interfície amb l'usuari final.

Cada tipus de xarxa utilitza diferents tecnologies i protocols en aquestes capes segons les seves necessitats i abast.
