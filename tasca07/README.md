# T07: Acadèmia feta amb Moodle

## 📋 Breu descripció
Pràctica **individual i tancada** on demostraràs la capacitat d'instal·lar, personalitzar, configurar i gestionar Moodle com ho faries en un encàrrec real.

**Client**: Escola d'ensenyament secundari "Escola Júlia"  
**Necessitat**: Portal d'aprenentatge online per facilitar la comunicació i l'aprenentatge entre professorat i alumnat.

## ⚠️ Normativa d'entrega IMPORTANT
- **No es lliura com a fitxer únic** al final
- Es lliura per **demostració i defensa**, part per part
- Treball en local a l'ordinador de l'escola
- **QUAN ACABIS CADA PART**: avisa el professor/a perquè validi que ho tens tot correcte
- L'avaluació es fa **"en directe"**: has d'ensenyar cada part i defensar-la

## 📁 Estructura de la pràctica (5 parts)
**Part 1**: Base de la instal·lació (ha d'estar completada i operativa)  
**Parts 2-5**: S'han d'ensenyar obligatòriament al professor/a quan s'acabin

## 🎯 Objectius específics

### **Part 1**: Instal·lar un sistema de gestió d'aprenentatge a distància
1. **Instal·lar Moodle** al servidor web local
   - Crear base de dades MySQL (nom: `moodle`, usuari: `root`, contrasenya: `root`)
   - Crear compte d'administrador: `admin` / `Administrador_1`
   - Completar dades personals (email, població, país)

2. **Configurar idioma** català com a predefinit

3. **Configurar primera pàgina** del lloc:
   - Nom complert: "Escola d'Ensenyament Secundari Júlia"
   - Nom curt: "Escola Júlia"
   - Descripció detallada (copiada d'una escola real)
   - Configurar visibilitat

4. **Personalitzar aparença**:
   - Afegir i aplicar nou tema (diferent als per defecte)
   - Modificar favicon per un personalitzat
   - Mostrar logo de l'escola

### **Part 2**: Crear comptes d'usuari i definir privilegis
1. Crear **4 categories de cursos**: 1er ESO, 2on ESO, 3er ESO, 4rt ESO

2. Crear **comptes de professors** (5):
   - Pedro Ruiz Gomez
   - Benito Wolff Ruiz  
   - Angel Lobo Mateo
   - Claudia Blazquez Tomas
   - Vicente Puñal Pineda
   - Segons configuració de l'arxiu adjunt 1

3. Assignar a **Pedro Ruiz Gomez** el rol de creador de cursos

4. Modificar rol de creador de cursos per gestionar categories

5. **Com Pedro Ruiz Gomez**, crear cursos:
   - **Matemàtiques 1** (MAT_1ESO) - 5 temes, format per pàgines
   - **Taulell d'anuncis 1** (TAU_1ESO) - format social
   - **Informàtica 1** (INF_1ESO) - 12 setmanes, treball en grups

6. Configurar **inscripcions automàtiques**:
   - Matemàtiques 1: contrasenya `mates1`
   - Informàtica 1: contrasenya `info1`
   - Taulell d'anuncis 1: accés visitants amb `guest`

7. Activar **autenticació per correu electrònic**

### **Part 3**: Manipular Moodle afegint continguts (Matemàtiques 1)
1. Configurar **5 temes** del curs Matemàtiques 1

2. Afegir **etiqueta inicial** amb nom del curs i imatge

3. Crear **fòrum de Matemàtiques 1**

4. Crear **glossari** amb 3 entrades

5. Configurar **xat del professor** (sessions setmanals)

6. Afegir **enquesta COLLES**

7. Enllaç a **XTEC - Matemàtiques**

8. Pàgina amb **criteris d'avaluació** (taula ponderacions)

9. Reordenar elements del curs

### **Part 4**: Manipular Moodle afegint més continguts
1. Dividir tema "Nombres" en 3 parts amb etiquetes

2. Crear **consulta** amb exercici pràctic

3. Crear **lliçó** sobre nombres racionals (4 pàgines + 4 preguntes)

4. Crear **qüestionari** d'avaluació amb 5 preguntes

5. Afegir **tasca de text en línia**

6. Afegir **tasca de penjar fitxer**

### **Part 5**: Afegir i configurar components i plugins
1. Afegir i configurar **blocs**:
   - Calendario (visible a totes pàgines)
   - Eventos próximos (visible a totes pàgines)
   - Usuarios en línea
   - Mis cursos
   - Comentarios
   - Entrada aleatoria del glosario
   - Canal RSS remoto (El periódico i La vanguardia)
   - Text amb enllaços externs

2. Afegir **gadgets** via blocs Text:
   - Rellotge javascript
   - Gadget per pàgines web

3. Crear **3 insígnies** (badges) amb Canva:
   - Activitat 1, Activitat 2, Activitat 3
   - Configurar condicions per guanyar-les

4. Crear **còpia de seguretat** del curs
5. **Restaurar còpia** en nou curs "Matemàtiques 1 backup"

## 🛠 Competències treballades
- Instal·lació i configuració de sistemes LMS
- Gestió d'usuaris i rols
- Creació i gestió de continguts educatius
- Personalització d'entorns d'aprenentatge
- Administració de plugins i components

## 📊 Avaluació per parts
Cada part (2-5) es valida **independentment** en el moment de la demostració:
- **Part 1**: Base operativa (sense validació específica, però necessària)
- **Part 2**: Gestió d'usuaris i cursos
- **Part 3**: Continguts bàsics del curs
- **Part 4**: Activitats avançades
- **Part 5**: Plugins i funcionalitats addicionals

## 🔧 Requisits tècnics
- Servidor web local (XAMPP, WAMP, etc.)
- Accés a internet per descarregar plugins
- Coneixements bàsics de Moodle
- Accés a editor d'imatges per insígnies

## 📝 Consells per la demostració
1. **Prepara't per explicar** cada configuració que has fet
2. **Tingues obertes** totes les pantalles necessàries
3. **Mostra el funcionament** de cada element demanat
4. **Justifica decisions** de configuració
5. **Prova tot abans** de cridar el professor

## ⏰ Temps estimat
- **Part 1**: 1-2 hores
- **Parts 2-5**: 6-8 hores totals

---
**Recorda**: Aquesta pràctica simula un entorn real de treball. Els coneixements adquirits són directament aplicables a la instal·lació i gestió de plataformes educatives en empreses i institucions.

**Estudiant:** [Miquel vico]    
**Data de Realització:** 22 de Gener de 2026 