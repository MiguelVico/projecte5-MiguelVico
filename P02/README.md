
# P02: Llicenciament Windows Server 2025

## 📌 Breu descripció

Mentre inicieu la vostra aventura emprenedora, cal seguir pagant factures. Gràcies a la gran feina que vau desenvolupar a **EverPia**, els responsables de la consultora han decidit donar-vos suport, passant-vos encàrrecs de clients que ara mateix no estan en condicions d’acceptar.

L’empresa **TransLògic S.A.**, dedicada a la logística regional, vol renovar la seva infraestructura de servidors a la versió **Windows Server 2025**. Actualment disposen d’un servidor físic antic que ha quedat obsolet i volen virtualitzar tota la seva càrrega de treball per millorar la disponibilitat.

Com a consultors informàtics, haureu d’analitzar el model de llicenciament per nucli (core), calcular costos, determinar el tipus de CAL més econòmic i presentar la solució al client.

---

## 👤 Introducció al client

**Empresa:** TransLògic S.A. – logística regional

### Infraestructura actual proposada:

- **Servidor físic (Host):** 1 unitat amb **2 processadors (CPUs)**. Cada processador té **12 nuclis (cores) físics** → Total: **24 nuclis**.

### Càrrega de treball (Màquines Virtuals - VMs):

| Tipus de VM | Quantitat |
|-------------|-----------|
| Controlador de Domini (Active Directory) | 1 |
| Servidor de Fitxers | 1 |
| Servidor d’Impressores i Gestió Documental | 1 |
| SQL Server (Base de dades de l’ERP) | 1 |
| VMs de suport per a logística i terminals | 8 |
| **Total VMs amb Windows Server** | **12** |

### Usuaris i dispositius:

- **45 empleats en total**
  - **30 treballadors d’oficina** (cada un té PC propi + portàtil)
  - **15 mossos de magatzem** (comparteixen 5 tauletes robustes en 3 torns)

---

## 🎯 Objectius específics / Finalitat de la tasca

- **Seleccionar la versió concreta de sistema operatiu** (Windows Server 2025) que s’adapta a les necessitats del client, tenint en compte requisits tècnics i aspectes econòmics.
- **Calcular el cost total** segons les dues opcions principals: **Standard** vs **Datacenter**.
- **Determinar quin tipus de CAL** (User CAL vs Device CAL) és més econòmic per a l’empresa.
- **Justificar la decisió final** basant-se en costos, escalabilitat futura i funcionalitats (Storage Spaces Direct, SDN, etc.).
- **Presentar la solució al client** mitjançant una presentació (5-10 minuts) per a un perfil no tècnic (el gerent de TransLògic).

> Objectius secundaris: elaboració de presentacions i exposició oral.

---

## 🧠 Competències treballades

| Competència | Descripció |
|-------------|-------------|
| **k)** | Elaborar pressupostos de sistemes a mida complint els requeriments del client. |
| **l)** | Assessorar i assistir al client, canalitzant a un nivell superior els supòsits que ho requereixin per trobar solucions adequades. |
| **o)** | Utilitzar els mitjans de consulta disponibles, seleccionant-ne el més adequat per resoldre supòsits no coneguts i dubtes professionals. |

**Capacitats clau:**
- Autonomia, Innovació, Relació interpersonal, Organització del treball, Responsabilitat, Treball en equip, Resolució de problemes.

---

## 📚 Resultats d’aprenentatge (RA) i Criteris d’avaluació (CA)

| Mòdul | RA | CA | Descripció |
|-------|----|----|-------------|
| 0224 SOX | RA1 | 1.1 | Instal·la sistemes operatius en xarxa. Realitza l’estudi de compatibilitat del sistema informàtic. |
| 1713 Projecte | RA2 | 2.1 | Planteja solucions a les necessitats del sector tenint en compte viabilitat i costos. Identifica les necessitats. |
| 1713 Projecte | RA5 | 5.1, 5.2 | Transmet informació amb claredat, de manera ordenada i estructurada. Manté actitud ordenada. Transmet informació verbal horitzontal i verticalment. |

**Continguts (C):**
- Sistemes Operatius en Xarxa propietaris
- Elaboració de presentacions

---

## 📝 Instruccions de realització

### 1. Analitzar el model de llicenciament per nucli (core) de Windows Server 2025

- Investiga com funciona el llicenciament actual de Microsoft per a Windows Server 2025 (o la versió equivalent més recent si la 2025 encara no està publicada, s’utilitzarà la documentació de Windows Server 2022 com a base).
- Cada servidor físic requereix llicenciar **tots els nuclis físics** (mínim 8 llicències de 2 nuclis per servidor i mínim 16 nuclis per servidor).
- Recorda que les VMs s’executen sobre el mateix host físic.

### 2. Calcular el cost total per a les dues opcions

- **Standard:** permet fins a 2 VMs per llicència completa (quan es llicencien tots els nuclis). Per a més VMs, calen llicències addicionals.
- **Datacenter:** permet un nombre il·limitat de VMs amb la mateixa llicència de nuclis.
- Fes càlculs per a **24 nuclis** i **12 VMs**.

### 3. Determinar el tipus de CAL més econòmic

- **User CAL:** cada empleat que accedeix al servidor necessita una CAL.
- **Device CAL:** cada dispositiu que accedeix al servidor necessita una CAL.
- Analitza les dades de l’empresa (45 empleats, 30 tenen PC+portàtil = 60 dispositius d’oficina, 5 tauletes compartides per 15 mossos).
- Calcula quin model surt més a compte.

### 4. Justificar la decisió final

- Considera:
  - Cost total inicial (llicències + CALs).
  - Escalabilitat futura (si volen afegir més VMs).
  - Funcionalitats avançades de Datacenter (Storage Spaces Direct, SDN, Shielded VMs, etc.) que no estan a Standard.

### 5. Preparar la presentació al client

- Durada: **5-10 minuts**.
- Llenguatge clar, sense gaire tecnicisme, orientat al gerent de TransLògic.
- Estructura suggerida:
  - Context i necessitats del client.
  - Explicació senzilla del llicenciament per nuclis.
  - Comparació Standard vs Datacenter (costos i avantatges).
  - Recomanació de CAL (User vs Device).
  - Justificació final i pressupost resum.
  - Torn de preguntes.

---

## 🔗 Materials i links de suport

- **UD6.AA1. Introducció a Windows Server** (Moodle 0224 SOX)
- **Microsoft. Precios y licencias de Windows Server** – enllaços proporcionats pel professor (simulació o documentació oficial)

> Utilitza eines com [Microsoft Product Terms](https://www.microsoft.com/licensing/terms) o simuladors de llicenciament.

---

## ✅ Criteris d’avaluació (orientatius)

| Aspecte | Puntuació |
|---------|------------|
| Càlcul correcte de llicències per nucli (Standard vs Datacenter) | 25% |
| Càlcul i justificació del tipus de CAL (User vs Device) | 20% |
| Justificació econòmica i tècnica de la decisió final | 20% |
| Qualitat de la presentació (estructura, claredat, adequació al client) | 20% |
| Exposició oral (durada, to, respostes a preguntes) | 15% |
| **Total** | **100%** |

---

## 📤 Lliurament

- **Producte final a entregar:** presentació (PowerPoint, Google Slides, Canva, PDF).
- **Termini de lliurament:** mirar temporització (consultar Moodle o calendari del curs).
- **Lloc de lliurament:** enllaç a la presentació a la tasca corresponent del Moodle.

---

## ⏱️ Hores associades

| Mòdul | Hores |
|--------|-------|
| 0224 Sistemes Operatius en Xarxa | 2 h |
| 1713 Projecte Intermodular | 4 h |
| Tutoria | (no especificat) |

---

## 🔗 Mòduls relacionats

| Mòdul | RA afectats |
|--------|--------------|
| 0224 SOX | RA1–RA6 |
| 0226 Seguretat Informàtica | RA1–RA5 |
| 0227 Serveis de Xarxa | RA1–RA8 |
| 0228 Aplicacions web | RA1–RA5 |
| 1708 Sostenibilitat | RA1–RA5 |
| 1710 Itinerari Ocupabilitat II | RA1–RA6 |
| 1713 Projecte Intermodular | RA1–RA5 |

---

## 💡 Exemple de càlcul ràpid (orientatiu)

> **Nota:** Els preus són simulats per a l’exercici. Consulta fonts actualitzades de Microsoft.

- **Nuclis:** 24 → necessites 12 llicències de 2 nuclis (cada llicència cobreix 2 nuclis).
- **Standard:** Cada llicència completa (16 nuclis) permet 2 VMs. Amb 24 nuclis = 1,5 llicències completes → 3 VMs per llicència? No exacte. Realment: cal llicenciar tots els nuclis (24). Amb Standard, per cada conjunt de 16 nuclis llicenciats tens dret a 2 VMs. Com que tens 24 nuclis = 1,5 unitats de 16 nuclis → 1,5 * 2 VMs = 3 VMs. Per a 12 VMs necessites 4 vegades més llicències de nuclis (és a dir, llicenciar els 24 nuclis **4 vegades** → 24*4=96 nuclis llicenciats).
- **Datacenter:** llicències els 24 nuclis una sola vegada i tens VMs il·limitades.
- **CALs:** 45 usuaris vs 65 dispositius (30*2=60 PC+portàtil + 5 tauletes = 65). Si User CAL és més barata que Device CAL, surt a compte User. Si Device CAL és més barata, cal comparar 45 usuaris vs 65 dispositius.


Si vols que adapti algun càlcul concret, afegeixi una rúbrica més detallada o generi una plantilla de presentació, digues-m’ho. Estic preparat per al següent anunci.
