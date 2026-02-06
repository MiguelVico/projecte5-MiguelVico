# README – T05: Instal·lació del domini translogic26.test

## 📌 Descripció de la tasca  
En aquesta pràctica hem instal·lat i configurat un **domini Active Directory** sobre un Windows Server 2025. L'objectiu era crear un entorn de prova per al client **TransLògic**, on el domini es diu **translogic26.test** (el número 26 correspon al meu número de llista).  

A més de la instal·lació manual, hem extret un **script de PowerShell** que permet automatitzar tot el procés per si en el futur cal repetir-lo o fer-lo en un altre servidor.

---

## 🎯 Objectius aconseguits  
✅ Instal·lar els rols necessaris al servidor (Active Directory Domain Services).  
✅ Crear un domini nou en un bosc nou amb el nom **translogic26.test**.  
✅ Establir el nivell funcional del domini i del bosc a **Windows Server 2025**.  
✅ Promocionar el servidor com a controlador de domini amb **DNS** i **Global Catalog**.  
✅ Documentar tot el procés amb captures de pantalla i explicacions pas a pas.  
✅ Generar i guardar l’script de PowerShell per automatitzar la instal·lació.

---

## 🛠️ Tecnologies utilitzades  
- **Sistema operatiu**: Windows Server 2025 Standard Evaluation  
- **Rol principal**: Active Directory Domain Services (AD DS)  
- **Eines d’administració**: Server Manager, PowerShell  
- **Protocols/serveis**: DNS, NetBIOS, SYSVOL  

---

## 📂 Estructura de l'entrega  
A la carpeta del repositori trobareu:

```
tasca05/
├── README.md                       # Aquest fitxer
├── guia.md                         # Guia completa de la instal·lació
├── imgT05/
│   ├── captura4.png                # Selecció tipus instal·lació
│   ├── captura5.png                # Selecció servidor
│   ├── captura6.png                # Selecció rol AD DS
│   ├── captura7.png                # Progrés instal·lació
│   ├── captura8.png                # Deployment Configuration
│   ├── captura9.png                # Domain Controller Options
│   ├── captura10.png               # DNS Options
│   ├── captura11.png               # Nom NetBIOS
│   ├── captura12.png               # Paths
│   ├── captura13.png               # Review Options
│   ├── captura14.png               # Prerequisites Check
│   ├── captura15.png               # Results
│   └── captura16.png               # Login després del reinici
└── script_install_ADDS.ps1         # Script PowerShell generat
```

---

## 🚀 Procediment resumit  
1. **Obrir Server Manager** i afegir rols i funcions.  
2. **Seleccionar el servidor** DC26 (IP 10.0.2.4).  
3. **Instal·lar el rol Active Directory Domain Services** amb totes les eines d’administració.  
4. **Executar l’assistent de configuració** i seleccionar *Add a new forest*.  
5. **Posar el nom del domini**: `translogic26.test`.  
6. **Configurar nivell funcional 2025**, activar DNS i Global Catalog, posar contrasenya DSRM.  
7. **Revisar opcions** i passar la comprovació de prerrequisits.  
8. **Instal·lar** i esperar el reinici automàtic.  
9. **Iniciar sessió** amb el compte del domini: `TRANSLOGIC26\Administrator`.  
10. **Guardar el script de PowerShell** per a futures automatitzacions.

---

## 📜 Script de PowerShell generat  
Durant la configuració vam extreure el següent script, que replica tot el procés:

```powershell
Install-ADDSForest `
-DomainName "translogic26.test" `
-DomainNetbiosName "TRANSLOGIC26" `
-ForestMode "WinThreshold" `
-DomainMode "WinThreshold" `
-InstallDns:$true `
-NoRebootOnCompletion:$false `
-Force:$true
```

---

## 🔍 Competències treballades  
- **c) Instal·lar i configurar programari bàsic i d’aplicació**, assegurant-ne el funcionament en condicions de qualitat i seguretat.  
- **f) Instal·lar, configurar i mantenir serveis multiusuari**, aplicacions i dispositius compartits en un entorn de xarxa local.

---

## 📎 Notes importants  
- El servidor **es reiniciarà automàticament** després de la promoció a controlador de domini.  
- És recomanable (però no obligatori per la prova) assignar una **IP estàtica** abans de començar.  
- El nom NetBIOS es genera automàticament, però es pot canviar si cal.  
- El script de PowerShell es pot modificar per adaptar-lo a altres dominis o configuracions.

---

**Autor**: [Miquel Vico]  
**Data**: [21/1/2026]  
**Curs**: 0224 Sistemes Operatius en Xarxa