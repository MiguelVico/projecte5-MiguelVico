# Tasca 03: Serveis de Transferència de Fitxers

## 📁 Descripció
Aquesta pràctica consisteix en la instal·lació, configuració i administració d'un servidor **FTP** (File Transfer Protocol) utilitzant **vsftpd** en un entorn Ubuntu, amb l'objectiu d'entendre el funcionament bàsic dels protocols de transferència de fitxers, els modes de connexió, i les mesures de seguretat bàsiques com el *chroot*.

## 🎯 Objectius
- Instal·lar i configurar un servidor FTP amb **vsftpd**.
- Crear usuaris i directoris per a l'accés local i anònim.
- Configurar restriccions de seguretat mitjançant **chroot**.
- Provar connexions FTP des de terminal i client gràfic (FileZilla).
- Analitzar el trànsit de xarxa amb **Wireshark** per entendre la manca de xifrat en FTP.

## 🛠️ Tecnologies Utilitzades
- **Sistema Operatiu:** Ubuntu Server
- **Servidor FTP:** vsftpd (Very Secure FTP Daemon)
- **Eines de xarxa:** Wireshark
- **Client FTP:** Terminal FTP, FileZilla
- **Protocols:** FTP (port 21), TCP/IP

## 📂 Estructura del Projecte
```
tasca03/
│
├── img_T03/                    # Captures de pantalla de la pràctica
│   ├── captura1.png
│   ├── captura2.png
│   ├── ...
│   └── captura30.png
│
├── guia.md                     # Guia completa pas a pas
└── README.md                   # Aquest fitxer
```

## 🚀 Procediment Resumit

### 1. Instal·lació i Configuració Inicial
```bash
sudo apt update
sudo apt upgrade -y
sudo apt install vsftpd
sudo systemctl status vsftpd
```

### 2. Configuració del Directori FTP
```bash
sudo mkdir -p /srv/ftp
sudo chown nobody:nogroup /srv/ftp
sudo chmod 755 /srv/ftp
```

### 3. Creació d’Usuaris
```bash
sudo adduser prova1
sudo adduser prova2
```

### 4. Configuració de Seguretat (chroot)
Editar `/etc/vsftpd.conf`:
```bash
chroot_local_user=YES
allow_writeable_chroot=YES
```
Reiniciar el servei:
```bash
sudo systemctl restart vsftpd
```

### 5. Prova de Connexió
```bash
ftp localhost
# Usuari: prova1
# Comandes: ls, put, get, cd
```

### 6. Connexió des de Client Extern
```bash
ftp 192.168.56.101
```

### 7. Anàlisi amb Wireshark
```bash
sudo apt install wireshark
# Capturar trànsit al port 21
```

### 8. Client Gràfic FileZilla
- Descàrrega i instal·lació de FileZilla
- Configuració de connexió amb IP, usuari i contrasenya
- Transferència gràfica de fitxers

## 🔐 Aspectes de Seguretat Implementats
- **Accés anònim desactivat** per defecte.
- **Chroot activat** per confinar usuaris als seus directoris home.
- **Permisos restringits** als directoris públics.
- Ús de **mode passiu** per a transferències.

## ⚠️ Conclusions i Aprendre
- **FTP és ràpid però insegur**: les dades viatgen en text clar.
- El **chroot** és una mesura bàsica però efectiva per limitar l'accés dels usuaris.
- Per a entorns reals, és recomanable utilitzar **SFTP** o **FTPS** per a transferències xifrades.
- Els clients gràfics com **FileZilla** simplifiquen la gestió de fitxers.

## 📚 Competències Adquirides
- Instal·lació i configuració de serveis multiusuari.
- Administració d'usuaris i permisos en entorns de xarxa.
- Diagnosi de funcionament mitjançant eines de xarxa.
- Aplicació de mesures de seguretat bàsiques.

## 📄 Llicència
Aquest projecte és part d'una formació pràctica en serveis de xarxa i es distribueix per a fins educatius.

---
**Realitzat per:** [Miquel Vico]  
**Data:** 2026  
**Curs:** Serveis de Xarxa  