# T02: Control de versions. Treballant amb git

## 📋 Breu descripció
Fins ara hem gestionat el control de versions utilitzant directament el repositori des de la web de GitHub. Aquesta metodologia presenta diverses limitacions que ens impedeixen treballar de forma eficient:
- **Lentitud** a l'hora d'editar (editor web limitat vs editors locals com VS Code)
- **Dificultat** en la gestió del repositori (afegir arxius, carpetes, etc.)
- **Accions ineficients** que requereixen múltiples passos

Per superar aquestes limitacions, començarem a treballar com es fa al món real: **combinant el control de versions local amb git amb un gestor de repositoris remot** (GitHub).

## 🎯 Objectius específics
- Gestionar el projecte mitjançant el control de versions amb git
- Utilitzar el flux de treball local-remot estàndard de la indústria
- Dominar les operacions bàsiques de git (clone, add, commit, push, pull)

## 📚 Materials i links de suport
1. **Introducció a GitHub**: https://github.com/SMX2n/IntroGitHub
2. **Guia Control de Versions**: https://github.com/SMX2n/ControlVersions

## 🔄 Flux de treball amb git
El nostre flux de treball partirà sempre d'un repositori a GitHub i seguirem aquests passos:

### 1. **Inicialització**
```bash
# Clonar repositori remot a local
git clone https://github.com/usuari/repositori.git
```

### 2. **Cicle de treball diari**
```bash
# Abans de començar: actualitzar repositori local
git pull origin main

# Fer canvis als arxius...

# Afegir canvis a l'àrea de preparació
git add .
# o per arxius específics
git add arxiu1.md arxiu2.js

# Confirmar canvis amb missatge descriptiu
git commit -m "Descripció clara dels canvis realitzats"

# Pujar canvis al repositori remot
git push origin main
```

### 3. **Comandes essencials**
```bash
# Veure estat del repositori
git status

# Veure històric de commits
git log --oneline

# Desfer canvis (segons necessitat)
git restore arxiu.md          # Descartar canvis no stageados
git reset HEAD arxiu.md       # Treure de l'àrea de preparació
git commit --amend            # Modificar últim commit
```

## 🛠 Configuració inicial (primer cop)
```bash
# Configurar identitat (nom i email)
git config --global user.name "El teu nom"
git config --global user.email "el.teu@email.com"

# Configurar editor preferit (opcional)
git config --global core.editor "code --wait"
```

## 📁 Estructura recomanada del repositori
```
projecte/
├── docs/           # Documentació
├── src/           # Codi font
├── assets/        # Recursos (imatges, etc.)
├── README.md      # Document principal
└── .gitignore     # Arxius a ignorar
```

## 📝 Arxius .gitignore
És important crear un fitxer `.gitignore` per excloure arxius que no han d'estar al control de versions:
```
# Arxius del sistema
.DS_Store
Thumbs.db

# Arxius d'entorns virtuals
venv/
env/
node_modules/

# Arxius de configuració local
*.local
*.env

# Arxius de logs
*.log
```

## 🔍 Solució de problemes freqüents

### **Conflict en merge**
```bash
# Si git pull genera conflictes
git status                      # Veure arxius en conflicte
# Editar arxius i resoldre conflictes manualment
git add arxiu_conflicte.md      # Marcar com resolt
git commit -m "Resolució conflicte"
git push origin main
```

### **Desfer canvis incorrectes**
```bash
# Recuperar versió anterior d'un arxiu
git checkout -- arxiu.md

# Eliminar commits no publicats
git reset --soft HEAD~1    # Manté canvis a l'àrea de treball
git reset --hard HEAD~1    # Elimina completament
```

## 🎖 Bones pràctiques
1. **Commits freqüents i atomics**: Cada commit ha de representar un canvi lògic i complet
2. **Missatges descriptius**: Utilitzar l'estil convencional: 
   - Línia 1: Resum (màx 50 caràcters)
   - Línia 2: Buida
   - Línia 3+: Descripció detallada
3. **Sempre fer pull abans de push**: Evitar conflictes
4. **No commit de dades sensibles**: Passwords, claus, etc.
5. **Branques per funcionalitats**: Per treballar en funcions noves sense afectar main

## 📊 Competències treballades
- **j)** Elaborar documentació tècnica i administrativa del sistema
- **m)** Organitzar i desenvolupar el treball assignat mantenint relacions professionals adequades

## 🎯 Resultats d'aprenentatge (RA)
**RA5**. Transmet informació amb claredat, de manera ordenada i estructurada
- **5.1** Manté una actitud ordenada i metòdica en la transmissió de la informació
- **5.2** Transmet informació verbal tant horitzontal com verticalment

## 💻 Capacitats clau
- Autonomia
- Innovació
- Relació interpersonal
- Organització del treball
- Responsabilitat
- Treball en equip
- Resolució de problemes

## 📅 Informació de lliurament
- **Producte final a entregar**: No hi ha entregable específic
- **Termini de lliurament**: Activitat contínua durant el curs
- **Avaluació**: Es valorarà l'ús correcte de git en el desenvolupament del projecte principal

## 💡 Consells addicionals
1. **Practica amb repositoris de prova** abans d'aplicar-ho al projecte principal
2. **Visualitza el graf de commits** amb `git log --oneline --graph --all`
3. **Utilitza GitHub Desktop** si prefereixes una interfície gràfica
4. **Documenta processos complexos** al README.md del projecte

---

**Recorda**: El control de versions és una eina fonamental per a qualsevol desenvolupador professional. Dominar git et donarà una gran avantatge en el teu futur professional.

**Estudiant:** [Miquel vico]    
**Data de Realització:** 22 de Gener de 2026 