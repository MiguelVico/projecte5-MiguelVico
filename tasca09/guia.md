# **T09: Seguretat: les vulnerabilitats dels sistemes**  
### Guia pas a pas amb totes les captures i comandes

Aquesta guia explica com configurar i utilitzar eines per detectar vulnerabilitats en sistemes, concretament amb **Metasploitable** i **OpenVAS (Greenbone)** dins d’un entorn virtualitzat amb VirtualBox. Tot això ho fem per entendre com es poden explotar i identificar vulnerabilitats en sistemes reals.

---

## **1. Preparació dels entorns virtuals**

### **Captura 1: VirtualBox amb les màquines virtuals**
![Llistat de màquines virtuals](/tasca08/img_T06/captura1.png)

Aquí es veu el **Oracle VirtualBox Manager** amb totes les MV que tenim preparades:
- `metasploitable-linux` (objectiu per escanejar vulnerabilitats)
- `OPENVAS-FREE-24.10.9-VirtualBox` (eina de detecció de vulnerabilitats)
- Altres màquines (FTP, Windows, etc.) que no utilitzarem ara.

**Anàlisi:**  
Aquest és el punt de partida. Totes les màquines estan aturades. Caldrà engegar-les i configurar-les perquè es vegin entre elles.

---

### **Captura 2: Configuració de xarxa de Metasploitable**
![Configuració de xarxa de Metasploitable](/tasca08/img_T06/captura2.png)

Aquí estem dins dels ajustos de la MV `metasploitable-linux`.  
A l’apartat **Xarxa → Adaptador 1** veiem:
- **Connectat a:** Xarxa NAT  
Això vol dir que la màquina tindrà accés a Internet i rebrà una IP automàtica del router virtual de VirtualBox, però no serà accessible des d’altres màquines de la xarxa interna.

**Anàlisi:**  
Si volem que OpenVAS pugui escanejar Metasploitable, caldrà que estiguin a la mateixa xarxa. Per això més endavant haurem de canviar aquesta configuració.

---

### **Captura 3: Inici de sessió a Metasploitable**
![Login a Metasploitable](/tasca08/img_T06/captura3.png)

Engeguem la MV `metasploitable-linux` i ens demana credencials:
- **Usuari:** `msfadmin`
- **Contrasenya:** `msfadmin`

Si intentem amb `admin` falla, perquè l’usuari per defecte és `msfadmin`.

**Anàlisi:**  
Aquesta màquina està dissenyada amb vulnerabilitats conegudes per practicar pentesting. És com un “camp de proves” controlat.

---

### **Captura 4: Sessió iniciada a Metasploitable**
![Sessió de terminal oberta](/tasca08/img_T06/captura4.png)

Un cop dins, veiem el missatge de benvinguda i el prompt:
```
msfadmin@metasploitable:~$
```

**Anàlisi:**  
Ja som dins del sistema. Ara podrem executar comandes per explorar la configuració de xarxa, serveis obertes, etc.

---

### **Captura 5: Comprovació de la IP amb `ip a`**
![Execució de ip a](/tasca08/img_T06/captura5.png)

Executem:
```bash
ip a
```
I veiem les interfícies de xarxa:
- `lo`: loopback (127.0.0.1)
- `eth0`: té la IP `10.0.2.6/24`

**Anàlisi:**  
Aquesta IP (`10.0.2.6`) és de la xarxa NAT de VirtualBox. És accessible des de la mateixa màquina i pot sortir a Internet, però des d’una altra MV (com OpenVAS) no la podrem veure si no canviem la configuració de xarxa.

---

### **Captura 6: Configuració de xarxa d’OpenVAS**
![Configuració de xarxa d’OpenVAS](/tasca08/img_T06/captura6.png)

Ara entrem als ajustos de la MV **OPENVAS-FREE**:
- **Xarxa → Adaptador 1:**  
  - Connectat a: **Adaptador de només l'amfitrió**  
  - Nom: VirtualBox Host-Only Ethernet Adapter

**Anàlisi:**  
Amb aquesta configuració, la MV OpenVAS estarà en una xarxa privada només entre el host i les altres MV que també estiguin connectades a aquest adaptador. Però caldrà que Metasploitable també estigui en aquesta xarxa perquè es vegin entre elles.

---

### **Captura 7: Inici de Greenbone OS**
![Login a Greenbone OS](/tasca08/img_T06/captura7.png)

Engeguem la MV OpenVAS i ens demana login:
- **Usuari:** `admin`
- **Contrasenya:** (per defecte buida? o caldrà posar-ne una)

També indica que la interfície web està disponible a:
```
http://127.0.1.1
```

**Anàlisi:**  
Greenbone OS és la distribució que porta OpenVAS/GVM preinstal·lat. Un cop dins, podrem accedir via web per configurar escaneigs de vulnerabilitats.

---

### **Captura 8: Setup Wizard de Greenbone**
![Setup Wizard](/tasca08/img_T06/captura8.png)

Ens apareix un assistent de configuració inicial. Premem **Yes** per completar la configuració.

**Anàlisi:**  
Aquest assistent ens guiarà per crear un usuari admin, configurar l’actualització de feeds de vulnerabilitats, etc.

---

### **Captura 9: Crear usuari admin web**
![Creació d’usuari admin](/tasca08/img_T06/captura9.png)

Ens pregunta si volem crear un **global web admin**. Premem **Yes**.

**Anàlisi:**  
Aquest usuari servirà per accedir a la interfície web de Greenbone. Sense ell no podríem gestionar els escaneigs.

---

### **Captura 10: Formulari de nou usuari**
![Formulari nou usuari](/tasca08/img_T06/captura10.png)

Omplim:
- **Account name:** `usauri` (o el nom que vulguem)
- **Password:** (posem una contrasenya segura)
- **Confirmació:** (la mateixa)

**Anàlisi:**  
Aquest usuari tindrà rol d’**Admin**, amb accés complet a totes les funcions de Greenbone.

---

### **Captura 11: Clau de subscripció Enterprise Feed**
![Configuració de feed](/tasca08/img_T06/captura11.png)

Ens demana una clau de subscripció per al **Greenbone Enterprise Feed**.  
Tenim dues opcions:
- **Skip:** Utilitzar el feed comunitari (menys actualitzat però funcional)
- **Introduir clau:** Si tenim una llicència enterprise

**Anàlisi:**  
Per aquesta pràctica podem fer **Skip** i continuar amb el feed comunitari. Tot i així, per entorns de producció caldria una llicència de pagament.

---

### **Captura 12: Selfcheck del sistema**
![Resultat del selfcheck](/tasca08/img_T06/captura12.png)

Després de la configuració, el sistema fa una auto-comprovació:
- **Graceful shutdown:** Hi ha hagut un apagat brusc (normal en una MV).
- **Feed desactualitzat:** Ens avisa que el feed té més de 10 dies.

**Anàlisi:**  
Aquests són avisos normals en una instal·lació nova. Podrem actualitzar el feed després des de la interfície web.

---

### **Captura 13: Configuració de interfície de xarxa**
![Elecció d’interfície de xarxa](/tasca08/img_T06/captura13.png)

Ens demana configurar una interfície de xarxa. Triem **eth0**.

**Anàlisi:**  
Cal configurar la xarxa perquè la MV OpenVAS tingui IP accessible des del navegador del host.

---

### **Captura 14: Configuració IPv4 amb DHCP**
![Configuració eth0](/tasca08/img_T06/captura14.png)

Veiem la configuració de **eth0**:
- **IPv4:** enabled
- **DHCP:** enabled
- La resta deshabilitat

**Anàlisi:**  
Amb DHCP activat, la MV obtindrà una IP automàticament de la xarxa host-only. Després podrem saber quina IP li ha tocat per accedir via web.

---

Ara seguim amb la configuració de xarxa de les MV, l’accés a la interfície web de Greenbone i l’execució d’un escaneig de vulnerabilitats sobre Metasploitable.

---

## **15. Configuració de la interfície eth1 d’OpenVAS**

![Configuració eth1](/tasca08/img_T06/captura15.png)

Després de configurar eth0, el sistema també mostra **eth1** amb DHCP activat.  
Això vol dir que OpenVAS té dues interfícies:
- **eth0:** connectada a la xarxa host-only (per escanejar altres MV)
- **eth1:** possiblement també host-only o una altra xarxa

**Anàlisi:**  
Dues interfícies poden ser útils per separar tràfic, però per aquesta pràctica amb una n’hi ha prou.

---

## **16. Adreces IP assignades a OpenVAS**

![IPs d’OpenVAS](/tasca08/img_T06/captura16.png)

Aquí veiem les IPs que ha obtingut OpenVAS:
- **eth0:** `10.0.2.7/24` (xarxa NAT)
- **eth1:** `192.168.56.104/24` (xarxa host-only)

**Anàlisi:**  
Important: **`192.168.56.104`** és la IP que farem servir per accedir des del navegador del host a la interfície web de Greenbone.  
Recordem que Metasploitable té `10.0.2.6`. Com que tots dos estan a la mateixa xarxa NAT (`10.0.2.0/24`), **es poden veure entre ells** i per tant OpenVAS podrà escanejar Metasploitable.

---

## **17. Creació d’un nou host a Greenbone**

![Afegir host a Greenbone](/tasca08/img_T06/captura17.png)

Dins de la interfície web de Greenbone (accedida des de `http://192.168.56.104`), anem a **Assets → Hosts** i creem un nou host:
- **IP Address:** `10.0.2.6`
- **Comment:** `Linux`

**Anàlisi:**  
Estem registrant la màquina objectiu dins de Greenbone per poder-la seleccionar després a l’hora de crear tasques d’escaneig.

---

## **18. Llistat de hosts a Greenbone**

![Llistat de hosts](/tasca08/img_T06/captura18.png)

Veiem el host que hem afegit:
- **IP:** `10.0.2.6`
- **Nom:** `Linux`
- **Modificat:** 27/01/2026

**Anàlisi:**  
Ara tenim el host registrat i preparat per ser escanejat. El següent pas serà crear credencials si volem fer verificacions autenticades (per SSH per exemple).

---

## **19. Creació de credencials SSH**

![Credencials SSH](/tasca08/img_T06/captura19.png)

Anem a **Configuration → Credentials** i creem una credencial SSH:
- **Name:** `ssh`
- **Type:** Username + Password
- **Username:** `msfadmin`
- **Password:** `msfadmin`

**Anàlisi:**  
Amb aquestes credencials, OpenVAS podrà autenticar-se via SSH a Metasploitable i fer comprovacions més profundes (com comprovar versions de paquets, configuracions locals, etc.).

---

## **20. Creació d’un nou target**

![Nou target](/tasca08/img_T06/captura20.png)

Ara anem a **Configuration → Targets** i creem un nou target:
- **Manual:** `10.0.2.6`
- **Port List:** All IANA assigned TCP
- **SSH Credential:** Seleccionem `ssh` al port 22

**Anàlisi:**  
Un “target” és el conjunt d’hosts i ports que volem escanejar. Aquí estem dient que volem escanejar `10.0.2.6` en tots els ports TCP estàndard, i que utilitzi les credencials SSH per les verificacions autenticades.

---

## **21. Creació d’una nova tasca d’escaneig**

![Nova tasca](/tasca08/img_T06/captura21.png)

Anem a **Scans → Tasks** i creem una nova tasca:
- **Name:** `Vulnerable Linux`
- **Scan Targets:** Seleccionem el target creat anteriorment
- **Scanner:** OpenVAS Default

**Anàlisi:**  
La tasca és el “treball” que farà OpenVAS: agafa un target, un perfil d’escaneig i el llança. Aquí l’anomenem `Vulnerable Linux` per identificar fàcilment de què es tracta.

---

## **22. Llistat de tasques (abans de llançar)**

![Llistat de tasques](/tasca08/img_T06/captura22.png)

Veiem la tasca creada a la llista. Encara està en estat **N/A** (no executada).

**Anàlisi:**  
Ara només caldrà prémer el botó de “▶ Start” per començar l’escaneig.

---

## **23. Tasca en execució**

![Tasca en execució](/tasca08/img_T06/captura23.png)

Un cop iniciada, la tasca canvia d’estat a **Running** i ens mostra un progresse del **38%**.

**Anàlisi:**  
L’escaneig està en marxa. Greenbone està provant ports, serveis i vulnerabilitats conegudes sobre la IP `10.0.2.6`. Això pot durar uns minuts.

---

## **24. Tasca completada**

![Tasca completada](/tasca08/img_T06/captura24.png)

Quan l’escaneig acaba, l’estat canvia a **Done** i apareixen resultats classificats per severitat.

**Anàlisi:**  
Ja tenim resultats! Veiem que hi ha vulnerabilitats de tipus **Critical**. Això era d’esperar, ja que Metasploitable està dissenyada per ser vulnerable.

---

## **25. Llistat de vulnerabilitats crítiques detectades**

![Vulnerabilitats crítiques](/tasca08/img_T06/captura25.png)

A la vista de **Results** veiem algunes de les vulnerabilitats trobades:
- **TWiki < 4.2.4 Multiple XSS / Command Execution**
- **Possible Backdoor: Ingresslock**
- **Operating System End of Life**
- **rlogin Passwordless Login**
- **rexec service running**
- **Distributed Ruby RCE**
- **vsftpd Backdoor Vulnerability**

**Anàlisi:**  
Aquestes són vulnerabilitats reals i conegudes que es troben a Metasploitable. Moltes tenen **CVSS 10.0 (Critical)**, el nivell més alt de perillositat.

---

## **26. Distribució de resultats per severitat**

![Resultats per severitat](/tasca08/img_T06/captura26.png)

El gràfic mostra la distribució de les **177 vulnerabilitats** trobades:
- **Critical:** La majoria
- **High:** Algunes
- **Medium / Low:** Poques

**Anàlisi:**  
Metasploitable és una màquina extremadament vulnerable, això es reflecteix en la quantitat de resultats crítics. En un entorn real, això seria molt perillós.

---

## **27. Informe complet de l’escaneig**

![Informe de l’escaneig](/tasca08/img_T06/captura27.png)

A l’apartat **Reports** podem veure un resum de l’escaneig:
- **Hosts escanejats:** 1
- **Ports oberts detectats:** 18 de 23
- **Vulnerabilitats trobades:** 632 resultats (67 de severitat alta)
- **Durada de l’escaneig:** 33 minuts

**Anàlisi:**  
Aquest informe és el “producte final” de la detecció de vulnerabilitats. Es pot exportar en PDF, HTML o XML per analitzar-lo o compartir-lo.

---

## **28. Detall d’una vulnerabilitat crítica: Ingresslock backdoor**

![Detall Ingresslock](/tasca08/img_T06/captura28.png)

Si cliquem sobre una vulnerabilitat, per exemple **“Possible Backdoor: Ingresslock”**, veiem:
- **Port:** 1524/tcp
- **CVSS:** 10.0
- **Descripció:** Hi ha una backdoor instal·lada que respon a comandes remotes.
- **Solució:** Neteja completa del sistema infectat.

**Anàlisi:**  
Aquesta backdoor permet executar comandes amb privilegis de root des de fora. És una de les vulnerabilitats més greus que es poden trobar en un servidor.

---

## **Resum final de la tasca**

1. **Hem configurat dues MV** a VirtualBox:
   - Metasploitable (objectiu vulnerable)
   - OpenVAS/Greenbone (eina de detecció)
2. **Hem connectat les dues a la mateixa xarxa** (NAT) perquè es puguin veure.
3. **Hem accedit a la interfície web de Greenbone** i configurat un host, target i tasca d’escaneig.
4. **Hem executat l’escaneig** i analitzat els resultats.
5. **Hem identificat múltiples vulnerabilitats crítiques**, incloent backdoors, serveis insegurs i sistemes obsolets.

---

## **Conclusió**

Amb aquesta pràctica hem après:
- **Què és una vulnerabilitat** i com impacta en la seguretat.
- **Com utilitzar eines com OpenVAS** per detectar vulnerabilitats de manera automatitzada.
- **Com interpretar els resultats** d’un escaneig (CVSS, severitat, solució).
- **La importància de mantenir els sistemes actualitzats** i tancar ports i serveis innecessaris.

Ara ja pots incorporar aquesta guia al teu GitHub amb les captures corresponents i el vocabulari fresc però formal que demanes. Si cal afegir més detalls o ajustar alguna cosa, m’ho dius! 🔍💻