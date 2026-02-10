# T06: Configuració del Domini

## 📋 Descripció de la Tasca

En aquesta tasca hem desplegat el domini **translogic26.test** després de la seva creació inicial. L'objectiu principal era organitzar els objectes del domini (usuaris, grups i equips) utilitzant Unitats Organitzatives (OU), crear grups de seguretat, implementar plantilles d’usuari i integrar un equip client Windows 11 al domini per a verificar el seu correcte funcionament.

## 🎯 Objectius

- Crear una estructura d’OU coherent i justificada.
- Definir grups de seguretat per a diferents departaments (`gestio`, `magatzem`, `gerencia`, `personal`).
- Crear plantilles d’usuari per a cada grup, configurant la pertinença al grup i la carpeta personal.
- Generar usuaris de prova a partir de les plantilles.
- Aprovisionar un equip `PC1` i unir-lo al domini.
- Verificar l’accés al domini des de l’equip client amb els usuaris de prova.

## 🛠️ Tecnologies Utilitzades

- **Windows Server 2022** (Controlador de Domini: DC26)
- **Active Directory Domain Services (AD DS)**
- **Active Directory Users and Computers**
- **Windows 11 Enterprise LTSC** (VM client)
- **VirtualBox** (per a la VM)
- **Xarxa NAT** amb DNS configurat manualment

## 📂 Estructura del Domini

```
translogic26.test/
├── usuaris/                    (OU principal d'usuaris)
│   ├── gestio/                 (OU per a usuaris de gestió)
│   ├── magatzem/               (OU per a usuaris de magatzem)
│   ├── gerencia/               (OU per a usuaris de gerència)
│   ├── plantilles/             (OU per a plantilles d'usuari)
│   └── OU groups/              (OU per a grups de seguretat)
└── equips/                     (OU per a equips del domini)
```

## 👥 Grups de Seguretat

| Nom del Grup | Àmbit      | Tipus      | Descripció                                  |
|--------------|------------|------------|--------------------------------------------|
| gestio       | Global     | Seguretat  | Usuaris del departament de gestió          |
| magatzem     | Global     | Seguretat  | Usuaris del departament de magatzem        |
| gerencia     | Global     | Seguretat  | Usuaris del departament de gerència        |
| personal     | Global     | Seguretat  | Grup que conté `gestio`, `magatzem`, `gerencia` |

## 👤 Plantilles d’Usuari

| Plantilla      | Grup Assignat | Carpeta Personal                       |
|----------------|---------------|----------------------------------------|
| TPL gestio     | gestio        | \\DC26\homes\TPL_gestio               |
| TPL magatzem   | magatzem      | \\DC26\homes\TPL_magatzem             |
| TPL gerencia   | gerencia      | \\DC26\homes\TPL_gerencia             |

## 🧪 Usuaris de Prova

| Usuari         | Plantilla     | Grup Assignat | Carpeta Personal                       |
|----------------|---------------|---------------|----------------------------------------|
| prova gestio   | TPL gestio    | gestio        | \\DC26\homes\prova_gestio             |
| prova magatzem | TPL magatzem  | magatzem      | \\DC26\homes\prova_magatzem           |
| prova gerencia | TPL gerencia  | gerencia      | \\DC26\homes\prova_gerencia           |

## 🖥️ Configuració de la VM Client

- **Nom:** PC1
- **Sistema Operatiu:** Windows 11 Enterprise LTSC
- **RAM:** 4 GB
- **Xarxa:** NAT amb DNS manual (`10.0.2.4` → DC26)
- **Unió al domini:** `translogic26.test`

## ✅ Comprovacions Realitzades

1. ✅ Inici de sessió als tres usuaris de prova des de `PC1`.
2. ✅ Assignació automàtica de la carpeta personal (`H:`).
3. ✅ Identificació correcta del perfil d’usuari del domini.
4. ✅ Accés als recursos compartits del servidor (`\\DC26\homes`).
5. ✅ Funcionament de la pertinença als grups de seguretat.

## 📸 Captures de Pantalla

Totes les captures estan ordenades i penjades a la carpeta `img_T06/`:

- `captura1.png` a `captura64.png`

## 📚 Competències Assolides

### Competències Tècniques (SOX)
- **RA2:** Gestió d’usuaris i grups en entorns en xarxa.
- **RA3:** Administració de dominis amb eines específiques.
- Configuració de comptes d’usuari, perfils, grups i pertinences.
- Utilització d’unitats organitzatives per a models administratius.
- Integració d’equips clients en un domini Active Directory.

### Capacitats Clau
- **Autonomia** en la planificació i execució.
- **Organització** de recursos jeràrquics.
- **Resolució de problemes** de xarxa i permisos.
- **Responsabilitat** en la gestió d’identitats.

## 🚀 Procediment Pas a Pas

El procediment detallat es troba a la guia `guia.md`, que inclou:
1. Creació d’OU.
2. Definició de grups.
3. Creació de plantilles.
4. Generació d’usuaris de prova.
5. Configuració de la VM Windows 11.
6. Unió al domini i verificació.

## 📎 Entregables

- `README.md` (aquest document)
- `guia.md` (guia detallada en Markdown)
- Carpeta `img_T06/` amb totes les captures

---

**Autor:** [Miquel Vico]  
**Data:** 10 de Febrer de 2026  
**Curs:** 0224 Sistemes Operatius en Xarxa  
**Centre:** [Escola Pia Mataró]