# Guia T06: Configuració del Domini

En aquesta tasca, anem a configurar el nostre domini **translogic26.test** creant una estructura organitzada amb Unitats Organitzatives (OU), grups de seguretat i plantilles d’usuari. Tot això ho fem per a poder gestionar usuaris i permisos de manera eficient i segura.

---

## 1. Crear Unitats Organitzatives (OU)

Primer de tot, hem de crear una estructura d'OU coherent. La idea és tenir una OU principal anomenada **usuaris** i dins d’aquesta, crear diferents OUs per a organitzar els objectes del domini.

![Enterant a la creació de la OU usuaris](/tasca06/img_T06/captura1.png)

![Enterant a la creació de la OU usuaris](/tasca06/img_T06/captura2.png)

![Enterant a la creació de la OU usuaris](/tasca06/img_T06/captura3.png)

### 1.1 Crear la OU principal `usuaris`

![Crear OU usuaris](/tasca06/img_T06/captura4.png)

Aquí estem dins de **Server Manager > AD DS > Active Directory Users and Computers**.  
Seleccionem el domini `translogic26.test` i creem una nova OU anomenada **usuaris**.  
Això ens permetrà tenir tot allò relacionat amb usuaris i grups ben separat.

### 1.2 Crear OU `equips`

![Crear OU equips](/tasca06/img_T06/captura5.png)

Ara creem una OU fora de `usuaris`, directament al domini, anomenada **equips**. Aquí anirem afegint els equips que s’uneixin al domini, com per exemple el **PC1**.

### 1.3 Crear OUs dins de `usuaris`

Dins de la OU `usuaris`, creem les següents sub-OU:

- **gestio**
- **magatzem**
- **gerencia**
- **plantilles**
- **OU groups**

![Crear OU gestio](/tasca06/img_T06/captura6.png)  
![Crear OU magatzem](/tasca06/img_T06/captura7.png)  
![Crear OU gerencia](/tasca06/img_T06/captura8.png)  
![Crear OU plantilles](/tasca06/img_T06/captura9.png)  
![Crear OU groups](/tasca06/img_T06/captura10.png)

**Per què aquesta estructura?**  
Així tenim tot ben classificat:
- `gestio`, `magatzem`, `gerencia` → per a usuaris segons el seu departament.
- `plantilles` → per a guardar les plantilles d’usuari que farem després.
- `OU groups` → per a tots els grups de seguretat.
- `equips` → per a màquines unides al domini.

És més fàcil administrar permisos i polítiques si tot està ordenat.

---

## 2. Crear Grups de Seguretat

Ara anem a crear els grups de seguretat que demana la tasca. Tots es creen dins de la OU **OU groups**.

### 2.1 Grup `gestio`

![Crear grup gestio](/tasca06/img_T06/captura11.png)

- **Nom:** `gestio`
- **Àmbit:** Global
- **Tipus:** Seguretat

### 2.2 Grup `magatzem`

![Crear grup magatzem](/tasca06/img_T06/captura12.png)

- **Nom:** `magatzem`
- **Àmbit:** Global
- **Tipus:** Seguretat

### 2.3 Grup `gerencia`

![Crear grup gerencia](/tasca06/img_T06/captura13.png)

- **Nom:** `gerencia`
- **Àmbit:** Global
- **Tipus:** Seguretat

### 2.4 Grup `personal`

![Crear grup personal](/tasca06/img_T06/captura14.png)

- **Nom:** `personal`
- **Àmbit:** Global
- **Tipus:** Seguretat

**Recorda:** Els grups `gestio`, `magatzem` i `gerencia` després s’afegiran com a membres del grup `personal`. Això fa que `personal` sigui un grup “paraguas” que conté tots els altres, útil per a assignar permisos generals.

### 2.5 Afegir grups al grup `personal`

![Afegir membres a personal](/tasca06/img_T06/captura15.png)

A la pestanya **Members** del grup `personal`, afegim els grups `gestio`, `magatzem` i `gerencia`.  
D’aquesta manera, qualsevol permis que donem a `personal`, s’aplicarà automàticament als usuaris d’aquests tres grups.

### 2.6 Comprovació de grups creats

![Llista de grups](/tasca06/img_T06/captura16.png)

A la OU `OU groups` ja es veuen tots els grups creats: `gestio`, `magatzem`, `gerencia` i `personal`. Tot correcte.

---

## 3. Crear Plantilles d’Usuari

Les plantilles d’usuari serveixen per a crear usuaris ràpidament amb configuracions predefinides (grup, carpeta personal, etc.). Les crearem dins de la OU `plantilles`.

### 3.1 Plantilla `TPL gestio`

![Crear plantilla TPL gestio - pas 1](/tasca06/img_T06/captura17.png)  
![Crear plantilla TPL gestio - pas 2](/tasca06/img_T06/captura18.png)  
![Crear plantilla TPL gestio - pas 3](/tasca06/img_T06/captura19.png)

**Dades bàsiques:**
- Nom: `TPL gestio`
- Login: `TPL_gestio`
- Password: (el que posem)
- Opcions: **Password never expires** (per a plantilles, això és habitual)
- Ubicació: `translogic26.test/usuaris/plantilles`

Després, a les propietats de l’usuari, l’afegirem al grup `gestio` i li configurem la carpeta personal.

### 3.2 Plantilla `TPL magatzem`

![Crear plantilla TPL magatzem](/tasca06/img_T06/captura20.png)

- Nom: `TPL magatzem`
- Login: `TPL_magatzem`
- Ubicació: `translogic26.test/usuaris/plantilles`

Igual que l’anterior, després l’afegirem al grup `magatzem`.

---

## 3. Crear Plantilles d’Usuari (continuació)

### 3.3 Plantilla `TPL gerencia`

![Crear plantilla TPL gerencia - pas 1](/tasca06/img_T06/captura22.png)

Aquí estem creant la tercera plantilla, per al departament de **gerencia**:

- **Nom:** `TPL gerencia`
- **Login:** `TPL_gerencia`
- **Ubicació:** `translogic26.test/usuaris/plantilles`

Després li posem contrasenya i marquem **Password never expires**, igual que amb les altres plantilles.

![Crear plantilla TPL gerencia - pas 2](/tasca06/img_T06/captura23.png)

### 3.4 Comprovació de les tres plantilles creades

![Llista de plantilles creades](/tasca06/img_T06/captura24.png)

Dins de la OU `plantilles` ja veiem les tres plantilles:
- `TPL gestio`
- `TPL magatzem`
- `TPL gerencia`

Perfecte, totes tres estan creades.

---

## 4. Configurar Grup i Carpeta Personal per a les Plantilles

Ara hem d’afegir cada plantilla al seu grup corresponent i configurar la carpeta personal (home folder).

### 4.1 Afegir `TPL gestio` al grup `gestio`

![Afegir TPL gestio al grup gestio](/tasca06/img_T06/captura25.png)

Obrim les propietats de `TPL gestio` i anem a la pestanya **Member Of**.  
Fem clic a **Add…** i busquem el grup `gestio`.

![Seleccionar grup gestio](/tasca06/img_T06/captura26.png)

Seleccionem `gestio` i cliquem **OK**.

![Comprovació de membres](/tasca06/img_T06/captura27.png)

Ara `TPL gestio` és membre de:
- `Domain Users` (per defecte)
- `gestio` (el que hem afegit)

### 4.2 Configurar carpeta personal per a `TPL gestio`

![Configurar carpeta personal TPL gestio](/tasca06/img_T06/captura36.png)

A la pestanya **Profile** de les propietats de l’usuari:

- A **Home folder**, seleccionem **Connect**.
- Triem la unitat `H:` (per exemple).
- A **To:** posem `\\DC26\homes\TPL_gestio`

Això farà que quan l’usuari iniciï sessió, se li assigni una unitat de xarxa `H:` que apunti a la seva carpeta personal al servidor.

### 4.3 Fer el mateix per a `TPL magatzem`

![Afegir TPL magatzem al grup magatzem](/tasca06/img_T06/captura28.png)
![Comprovació de membres TPL magatzem](/tasca06/img_T06/captura29.png)

Igual que abans, afegim `TPL magatzem` al grup `magatzem`.

![Configurar carpeta personal TPL magatzem](/tasca06/img_T06/captura38.png)

I configurem la carpeta personal:
- **Connect:** `H:`
- **To:** `\\DC26\homes\TPL_magatzem`

### 4.4 Fer el mateix per a `TPL gerencia`

![Seleccionar grup gerencia](/tasca06/img_T06/captura30.png)

Afegim `TPL gerencia` al grup `gerencia`.

---

## 5. Preparar la Carpeta Compartida `homes` al Servidor

Abans que els usuaris puguin accedir a les seves carpetes personals, hem de crear una carpeta compartida al servidor amb els permisos adequats.

### 5.1 Crear la carpeta `homes` a `C:\`

![Crear carpeta homes - pas 1](/tasca06/img_T06/captura31.png)

Anem a **This PC > Local Disk (C:)** i creem una carpeta nova anomenada `homes`.

### 5.2 Compartir la carpeta `homes`

![Compartir carpeta homes](/tasca06/img_T06/captura32.png)

Fem clic dret a la carpeta `homes` > **Properties > Sharing > Advanced Sharing**.

Marcam **Share this folder** i posam com a **Share name:** `homes`.

### 5.3 Donar permisos als usuaris del domini

![Permisos de compartició](/tasca06/img_T06/captura33.png)
![Permisos per a Domain Users](/tasca06/img_T06/captura34.png)
![Permisos per a Everyone](/tasca06/img_T06/captura35.png)

A **Permissions** afegim:
- `Domain Users` → **Full Control** (perquè puguin crear les seves subcarpetes).
- `Everyone` → **Read** (opcional, per si volem accés públic de lectura).

D’aquesta manera, quan un usuari del domini intenti accedir a `\\DC26\homes\TPL_gestio`, podrà crear la carpeta si no existeix.

---

## 6. Crear Usuaris de Prova a partir de les Plantilles

Ara crearem usuaris reals per a provar-ho tot. Els crearem també dins de la OU `plantilles` per a mantenir l’ordre.

### 6.1 Usuari `prova gestio`

![Crear usuari prova gestio](/tasca06/img_T06/captura40.png)

- **Nom:** `prova gestio`
- **Login:** `prova_gestio`
- **Ubicació:** `translogic26.test/usuaris/plantilles`

Després, igual que amb les plantilles, l’afegirem al grup `gestio` i li configurarem la carpeta personal:
- **Carpeta personal:** `\\DC26\homes\prova_gestio`

---

## 6. Crear Usuaris de Prova a partir de les Plantilles (continuació)

### 6.2 Usuari `prova gerencia`

![Crear usuari prova gerencia](/tasca06/img_T06/captura42.png)

- **Nom:** `prova gerencia`
- **Login:** `prova_gerencia`
- **Ubicació:** `translogic26.test/usuaris/plantilles`

Li assignem una contrasenya i marquem les opcions que calguin (normalment **Password never expires** per a proves).

![Contrasenya per a prova gerencia](/tasca06/img_T06/captura43.png)

### 6.3 Usuari `prova magatzem`

![Crear usuari prova magatzem](/tasca06/img_T06/captura44.png)

- **Nom:** `prova magatzem`
- **Login:** `prova_magatzem`
- **Ubicació:** `translogic26.test/usuaris/plantilles`

![Contrasenya per a prova magatzem](/tasca06/img_T06/captura45.png)

### 6.4 Comprovació dels tres usuaris de prova creats

![Llista d'usuaris a la OU plantilles](/tasca06/img_T06/captura46.png)

Dins de la OU `plantilles` ara tenim:
- **Plantilles:** `TPL gestio`, `TPL magatzem`, `TPL gerencia`
- **Usuaris de prova:** `prova gestio`, `prova magatzem`, `prova gerencia`

✅ Perfecte, els tres usuaris de prova estan creats.

---

## 7. Crear l’Equip `PC1` dins de la OU `equips`

Abans d’unir una màquina al domini, és bona pràctica crear l’objecte de l’equip al Directori Actiu.

![Crear objecte PC1 al domini](/tasca06/img_T06/captura47.png)

- **Nom de l’equip:** `PC1`
- **Ubicació:** `translogic26.test/equips`
- **Permís per a unir-se al domini:** Deixem per defecte `Domain Admins`.

Això fa que quan vulguem unir la màquina real al domini, el servidor ja coneix l’equip `PC1` i permet la unió.

---

## 8. Crear i Configurar la VM Windows 11

### 8.1 Crear la VM amb VirtualBox

![Crear VM - configuració bàsica](/tasca06/img_T06/captura49.png)

- **Nom:** `PC1`
- **ISO:** `Windows11LTSC.iso`
- **Memòria RAM:** 4096 MB (4 GB)
- **Processadors:** 1 CPU

![Configurar xarxa NAT](/tasca06/img_T06/captura50.png)

- **Xarxa:** Adaptador 1 connectat a **NAT** (per a tenir connexió a internet i al servidor DNS del domini).

### 8.2 Instal·lar Windows 11

![Iniciar instal·lació de Windows 11](/tasca06/img_T06/captura51.png)

Seleccionem **Instalar Windows 11**.

![Instal·lació en procés](/tasca06/img_T06/captura52.png)

L’instal·lació es posa en marxa i pot trigar una estona.

### 8.3 Configurar DNS a la VM

Un cop instal·lat Windows 11, anem a la configuració de xarxa per a apuntar al servidor DNS del domini (el controlador de domini DC26).

![Configurar DNS manual](/tasca06/img_T06/captura53.png)

- **DNS preferit:** `10.0.2.4` (la IP del DC26 en xarxa NAT).
- **DNS alternatiu:** el deixem en blanc.

![Propietats de TCP/IPv4](/tasca06/img_T06/captura54.png)

A les propietats de l’adaptador Ethernet, configurem:
- **Obtener una dirección IP automáticamente** (DHCP).
- **Usar las siguientes direcciones de servidor DNS:** `10.0.2.4`

D’aquesta manera, la VM podrà resoldre el nom del domini `translogic26.test`.

---

## 9. Unir la VM al Domini

### 9.1 Canviar el nom de l’equip i unir-lo al domini

![Propietats del sistema - unir al domini](/tasca06/img_T06/captura55.png)

Anem a **Configuración > Sistema > Información del sistema > Cambiar configuración**.

A la pestanya **Nombre de equipo**:
- **Nombre de equipo:** `PC1`
- **Miembro del:** **Dominio** → `translogic26.test`

![Credencials d’administrador del domini](/tasca06/img_T06/captura56.png)

Ens demana les credencials d’un compte amb permisos per a unir equips al domini. Posem:
- **Usuari:** `Administrator` (o un altre admin del domini).
- **Contrasenya:** la contrasenya de l’administrador.

### 9.2 Confirmació de la unió

![Unió al domini correcta](/tasca06/img_T06/captura57.png)

Ens surt un missatge de confirmació: **Se unió correctamente al dominio translogic26.test**. Reiniciem la màquina.

---

## 10. Comprovar l’Accés amb Usuaris del Domini

### 10.1 Iniciar sessió amb `prova_gestio`

![Inici de sessió amb usuari del domini](/tasca06/img_T06/captura58.png)

A la pantalla d’inici de Windows 11, seleccionem **Otro usuario** i posem:
- **Usuari:** `translogic26.test\prova_gestio`
- **Contrasenya:** la que li vam posar.

### 10.2 Comprovar la carpeta personal (home folder)

![Carpeta personal assignada](/tasca06/img_T06/captura59.png)

Un cop dins, anem a **Este equipo** i veiem que la unitat `H:` està assignada i apunta a `\\DC26\homes\prova_gestio`. Això vol dir que la configuració de la carpeta personal funciona correctament.

### 10.3 Comprovar el perfil d’usuari

![Perfil d'usuari al sistema](/tasca06/img_T06/captura60.png)

A **Configuración > Cuentas** veiem que l’usuari està identificat com `prova_gestio@translogic26.test`. Tot correcte.

---

## 11. Resum del que hem fet en aquesta part

1. **Completar usuaris de prova:**
   - `prova gestio`, `prova magatzem`, `prova gerencia` creats i configurats.

2. **Crear l’objecte de l’equip al domini:**
   - `PC1` creat dins de la OU `equips`.

3. **Instal·lar i configurar la VM Windows 11:**
   - Memòria 4 GB, xarxa NAT, DNS apuntant al DC26.

4. **Unir la VM al domini:**
   - Canvi de nom a `PC1` i unió a `translogic26.test`.

5. **Comprovar l’accés:**
   - Inici de sessió amb `prova_gestio`.
   - Carpeta personal `H:` accessible.
   - Perfil d’usuari del domini actiu.

---

## 12. Pròxims passos (si hi hagués més captures)

- Comprovar l’accés amb `prova_magatzem` i `prova_gerencia`.
- Verificar que els permisos de grup funcionin.
- Fer proves de recursos compartits i polítiques de grup.

Però amb el que hem fet fins ara, la tasca principal ja està completada: **domini desplegat, estructura d’OU, grups, plantilles, usuaris de prova i equip client units al domini.**

---

# Última Part de la Guia T06: Configuració del Domini

Ara completem la tasca amb les últimes captures (61 a la 64), on comprovem que els altres usuaris de prova també poden accedir correctament al domini i tenen la seva carpeta personal assignada.

---

## 10. Comprovar l’Accés amb els Altres Usuaris de Prova

### 10.3 Iniciar sessió amb `prova_magatzem`

Després de reiniciar la VM `PC1` o canviar d’usuari, fem log in amb:

- **Usuari:** `translogic26.test\prova_magatzem`
- **Contrasenya:** la que vam assignar.

Un cop dins, comprovem que tot funciona:

![Carpeta personal de prova_magatzem](/tasca06/img_T06/captura61.png)

A **Este equipo** veiem que la unitat `H:` està assignada i apunta a `\\DC26\homes\prova_magatzem`. Això confirma que la configuració de la carpeta personal funciona per a aquest usuari també.

![Perfil d'usuari prova_magatzem](/tasca06/img_T06/captura62.png)

A **Configuración > Cuentas** es veu l’usuari `prova_magatzem@translogic26.test`. Tot correcte.

### 10.4 Iniciar sessió amb `prova_gerencia`

Fem el mateix amb el tercer usuari de prova:

- **Usuari:** `translogic26.test\prova_gerencia`

![Carpeta personal de prova_gerencia](/tasca06/img_T06/captura63.png)

La unitat `H:` ara apunta a `\\DC26\homes\prova_gerencia`. Perfecte.

![Perfil d'usuari prova_gerencia](/tasca06/img_T06/captura64.png)

A la configuració del compte, es mostra `prova_gerencia@translogic26.test`. Tot en ordre.

---

## 11. Resum Final de la Tasca T06

Hem completat **tots els objectius** de la tasca:

### ✅ 1. Estructura d’OU coherent
- **usuaris/** (amb sub-OU per a departaments i plantilles)
- **equips/** (per a màquines unides al domini)
- Justificació: organització clara per a usuaris, grups i equips.

### ✅ 2. Grups de seguretat definits
- `gestio`, `magatzem`, `gerencia` (grups departamentals)
- `personal` (grup que conté els tres anteriors)
- Tots creats com a **Global Security Groups**.

### ✅ 3. Plantilles d’usuari per a cada grup
- `TPL gestio`, `TPL magatzem`, `TPL gerencia`
- Cada plantilla amb:
  - Pertinença al seu grup corresponent.
  - Carpeta personal configurada (`H:` → `\\DC26\homes\nom_usuari`).

### ✅ 4. Usuaris de prova creats
- `prova gestio`, `prova magatzem`, `prova gerencia`
- Creats a partir de les plantilles, amb carpeta personal funcional.

### ✅ 5. Equip `PC1` dins de la OU `equips`
- Objecte creat al Directori Actiu abans de la unió.

### ✅ 6. VM Windows 11 creada i unida al domini
- 4 GB de RAM, xarxa NAT.
- Configurada amb DNS del DC26 (`10.0.2.4`).
- Unida al domini `translogic26.test` com a `PC1`.

### ✅ 7. Comprovació de funcionament
- Els tres usuaris de prova poden iniciar sessió a `PC1`.
- La carpeta personal (`H:`) s’assigna automàticament.
- El perfil d’usuari mostra la identitat del domini.

---

## 12. Competències i Capacitats Treballades

### Competències tècniques (segons el RA):
- **RA2:** Gestió d’usuaris i grups en xarxa.
- **RA3:** Gestió de dominis amb eines d’administració.
- **CA2.1–2.9:** Configuració de comptes, perfils, grups i pertinences.
- **CA3.6–3.8:** Ús d’agrupacions, anàlisi d’estructura i eines de domini.

### Capacitats clau:
- **Autonomia:** Planificar i executar la estructura.
- **Organització:** Mantindre l’ordre amb OUs.
- **Resolució de problemes:** Solucionar errors de DNS i permisos.
- **Responsabilitat:** Assegurar el funcionament del domini.

---

## 13. Conclusió

La tasca T06 ha estat un èxit. Hem passat de tenir un domini bàsic a un entorn **totalment desplegat i funcional**, amb:
- Estructura lògica d’OU.
- Grups de seguretat ben definits.
- Plantilles per a escalar la creació d’usuaris.
- Equips clients integrats i usuaris provant l’accés.

Tot això ens prepara per a tasques més avançades com polítiques de grup, permisos avançats i gestió centralitzada de recursos.

---

📁 **Arxius entregables:**
- Aquesta guia en Markdown.
- Captures de pantalla ordenades (`captura1.png` a `captura64.png`).
- Control pràctic (si s’escau).

