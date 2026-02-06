# T04: Instal·lació Windows Server 2025

**Data:** 22/01/2026  
**Autor:** El teu nom  
**Descripció:** Guia pas a pas per instal·lar i configurar Windows Server 2025 en una màquina virtual, segons els requisits de TransLògic S.A.

---

## 1. Preparació de la Màquina Virtual

Abans de començar la instal·lació, hem de crear una màquina virtual amb les especificacions següents:

- **RAM:** 8 GB
- **Processadors:** 2
- **Disc principal:** 32 GB (per al sistema operatiu)
- **Disc secundari:** 10 GB
- **Interfícies de xarxa:** 
  1. Xarxa NAT
  2. Xarxa només amfitrió (Host-only)

### Comparativa amb els requisits oficials de Microsoft

Segons la documentació de Microsoft, els requisits mínims per a Windows Server 2025 són:

- **Processador:** 1.4 GHz, 64-bit
- **RAM:** 512 MB (mínim), 2 GB (recomanat)
- **Espai en disc:** 32 GB

**Conclusió:** La nostra configuració amb 8 GB de RAM i 2 processadors supera amb escreix els requisits mínims, cosa que assegurarà un bon rendiment. El disc principal de 32 GB coincideix amb el mínim, però tenim un disc secundari addicional de 10 GB per dades o funcions extra.

---

## 2. Procés d'Instal·lació

### Pas 1: Inici de la instal·lació i selecció d'idioma

En iniciar la màquina virtual des del ISO de Windows Server 2025, el primer pas és triar l'idioma i la configuració regional.

![Pantalla de selecció d'idioma i format hora/moneda](/tasca04/imgT04/captura1.png)

**Anàlisi:**  
Aquí configurem:
- **Idioma per instal·lar:** English (United States) → El sistema estarà en anglès.
- **Format d'hora i moneda:** Spanish (Spain, International Sort) → La data, hora i moneda seran en format espanyol.

És important triar el teclat correcte també, que veiem en una altra pantalla:

![Selecció del teclat espanyol](/tasca04/imgT04/captura4.png)

**Anàlisi:**  
Seleccionem **Spanish** com a mètode d'entrada del teclat. Així, tot i que el sistema és en anglès, podrem escriure amb accents i caràcters especials en espanyol sense problemes.

---

### Pas 2: Opció d'instal·lació

![Pantalla per triar entre instal·lar o reparar](/tasca04/imgT04/captura5.png)

**Anàlisi:**  
Seleccionem **"Install Windows Server"** per fer una instal·lació nova. L'opció "Repair my PC" és només per solucionar problemes en un sistema ja instal·lat. Acceptem que es borraran tots els arxius i aplicacions existents (cosa normal en una instal·lació nova en una màquina virtual buida).

---

### Pas 3: Selecció de la imatge del sistema operatiu

![Pantalla per triar l'edició de Windows Server 2025](/tasca04/imgT04/captura6.png)

**Anàlisi:**  
Trieu **"Windows Server 2025 Standard Evaluation (Desktop Experience)"**.  
- **Standard vs Datacenter:** Per a aquesta prova, triem Standard, que és suficient per a la majoria de servidors.
- **Desktop Experience:** Això instal·larà la interfície gràfica (GUI). És més fàcil per començar, encara que ocupi una mica més d'espai al disc.

---

### Pas 4: Creació del compte d'administrador

![Pantalla per definir la contrasenya de l'administrador](/tasca04/imgT04/captura7.png)

**Anàlisi:**  
Aquí definim la contrasenya per al compte **Administrator**. És el compte més poderós del sistema, així que cal triar una contrasenya complexa i segura (majúscules, minúscules, números, símbols) i recordar-la bé.

---

### Pas 5: Canviar el nom de l'equip

Un cop dins del sistema, anem a **Server Manager > Local Server > Properties** i fem clic a **"Change..."** al costat del nom de l'equip.

![Server Manager mostrant les propietats del servidor](/tasca04/imgT04/captura2.png)

**Anàlisi:**  
El nom actual és **DC26**. Segons la tasca, ha de ser **DCxx** (on xx és el teu número de llista). Si el teu número fos, per exemple, 26, ja estaria bé. Si no, canvia'l aquí. Després del canvi, **cal reiniciar el servidor** perquè s'apliqui.

---

### Pas 6: Configuració de la xarxa i DNS

Anem a **Settings > Network & internet** i configurem les interfícies. Per a la interfície interna (host-only), podem posar una IP fixa si cal. També és important verificar la configuració DNS.

![Configuració del DNS a l'adaptador de xarxa](/tasca04/imgT04/captura3.png)

**Anàlisi:**  
Aquí veiem que el **DNS preferit** està posat a **127.0.0.1**. Això vol dir que el servidor s'utilitzarà a ell mateix com a servidor DNS (cosa comuna quan després instal·lem el rol Active Directory Domain Services). De moment, si no tens un servidor DNS intern, pots posar aquí una adreça pública com la de Google (8.8.8.8) o la del teu router.

---

### Pas 7: Actualitzar el sistema

Un cop configurat, anem a **Windows Update** i busquem actualitzacions. Instal·lem totes les actualitzacions importants disponibles. Després, és recomanable **pausar les actualitzacions** durant un temps per evitar reinicis inesperats mentre estem provant coses.

**Com fer-ho (des de la GUI):**
1. Obre **Settings > Windows Update**.
2. Fes clic a **"Pause updates"**.
3. Trieu la durada màxima possible (normalment 5 setmanes).

---

## 3. Verificacions finals

Després de tot, comprovem:

1. **Nom de l'equip:** Ha de ser DCxx.
2. **Configuració de xarxa:** Hi ha dues interfícies, una amb NAT (per sortir a Internet) i una host-only (per xarxa interna).
3. **Espai en disc:** Obre **"This PC"** i verifica que hi hagi dos discs (C: de 32 GB i D: de 10 GB aproximadament).
4. **Actualitzacions:** Estan instal·lades i després pausades.

---

## 4. Conclusions

Hem aconseguit instal·lar Windows Server 2025 amb èxit seguint els passos de la guia. La configuració de la màquina virtual és coherent amb els requisits de Microsoft i fins i tot superior en RAM i CPU, la qual cosa garantirà un bon rendiment. Hem documentat cada pas amb captures per tenir una referència clara per a futures instal·lacions al client TransLògic S.A.

La propera fase seria afegir rols com Active Directory, DNS o DHCP, però això ja és per a una altra tasca.

---

**📌 Recursos:**
- [Requisits de hardware per a Windows Server (Microsoft Learn)](https://learn.microsoft.com/es-es/windows-server/get-started/hardware-requirements)