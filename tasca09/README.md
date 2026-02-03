# **T09: Seguretat - Les vulnerabilitats dels sistemes**

![OpenVAS vs Metasploitable](https://img.shields.io/badge/Scan-Critical-red) 
![VirtualBox](https://img.shields.io/badge/Virtualization-VirtualBox-orange)
![Greenbone](https://img.shields.io/badge/Scanner-OpenVAS%2FGreenbone-green)
![Metasploitable](https://img.shields.io/badge/Target-Metasploitable-blue)

Una pràctica completa de **detecció de vulnerabilitats** utilitzant OpenVAS/Greenbone contra una màquina virtual Metasploitable. Aprendrem a identificar, analitzar i entendre els riscos associats a sistemes amb vulnerabilitats conegudes.

## 📋 **Descripció de la Tasca**

Aquesta tasca forma part del mòdul de **Seguretat Informàtica** on explorem:
- Què són les vulnerabilitats dels sistemes
- Com impacten en la seguretat
- Eines per detectar-les i analitzar-les
- Els primers passos per mitigar els riscos trobats

**Competències treballades:** 
- Aplicar protocols i normes de seguretat
- Treballar en equip amb responsabilitat
- Realitzar actualitzacions periòdiques per corregir vulnerabilitats

## 🎯 **Objectius**

- [x] Configurar un entorn virtualitzat amb VirtualBox
- [x] Preparar una màquina objectiu vulnerable (Metasploitable)
- [x] Instal·lar i configurar una eina de detecció (OpenVAS/Greenbone)
- [x] Realitzar un escaneig complet de vulnerabilitats
- [x] Analitzar i interpretar els resultats
- [x] Identificar vulnerabilitats crítiques i les seves implicacions

## 🛠 **Tecnologies Utilitzades**

| Tecnologia | Versió | Propòsit |
|------------|---------|----------|
| Oracle VirtualBox | 7.x | Virtualització |
| Metasploitable Linux | 2.0 | Sistema objectiu vulnerable |
| Greenbone OS (OpenVAS) | 24.10.9 | Eina de detecció de vulnerabilitats |
| Ubuntu (Metasploitable) | 8.04 | Sistema operatiu base |

## 📁 **Estructura del Projecte**

```
tasca09-vulnerabilitats/
│
├── img_T06/                          # Captures de pantalla
│   ├── captura1.png                  # VirtualBox amb les MV
│   ├── captura2.png                  # Configuració xarxa Metasploitable
│   ├── ...                           # 28 captures en total
│   └── captura28.png                 # Detall vulnerabilitat crítica
│
├── guia_completa.md                  # Guia detallada pas a pas
└── README.md                         # Aquest arxiu
```

## 🚀 **Procediment Pas a Pas**

### **Fase 1: Preparació de l'entorn**
1. **Configuració de VirtualBox**
   - Creació de dues màquines virtuals:
     - Metasploitable (objectiu)
     - OpenVAS (scanner)
   - Configuració de xarxa per a comunicació entre MV's

2. **Configuració de Metasploitable**
   - Inici de sessió amb credencials per defecte (`msfadmin/msfadmin`)
   - Obtenció de la IP amb `ip a` → `10.0.2.6`

### **Fase 2: Configuració d'OpenVAS/Greenbone**
1. **Primer inici**
   - Login amb `admin` (sense contrasenya inicial)
   - Assistents de configuració inicial

2. **Creació d'usuari web**
   - Usuari: `usauri`
   - Rol: Administrador

3. **Configuració de feeds**
   - Utilització del feed comunitari (gratuït)
   - Configuració de xarxa amb DHCP

### **Fase 3: Escaneig de Vulnerabilitats**
1. **Definició del target**
   - IP: `10.0.2.6` (Metasploitable)
   - Ports: Tots els TCP estàndard

2. **Configuració de credencials**
   - SSH: `msfadmin/msfadmin`
   - Per a verificacions autenticades

3. **Creació i execució de la tasca**
   - Nom: "Vulnerable Linux"
   - Durada: ≈ 33 minuts
   - Resultats: 632 vulnerabilitats detectades

## 📊 **Resultats Obtinguts**

### **Estadístiques de l'Escaneig**
| Mètrica | Valor |
|---------|-------|
| Hosts escanejats | 1 |
| Ports oberts detectats | 18/23 |
| Vulnerabilitats totals | 632 |
| Vulnerabilitats Crítiques (CVSS 9.0-10.0) | 177 |
| Temps d'escaneig | 33 minuts |

### **Vulnerabilitats Crítiques Destacades**
1. **Possible Backdoor: Ingresslock** (CVSS 10.0)
   - Port: 1524/tcp
   - Permet execució remota de comandes com root

2. **TWiki < 4.2.4 Multiple XSS / Command Execution** (CVSS 10.0)

3. **rlogin Passwordless Login** (CVSS 10.0)

4. **vsftpd Backdoor Vulnerability** (CVSS 9.8)

5. **Operating System End of Life** (CVSS 10.0)

## 🔍 **Anàlisi dels Resultats**

### **Observacions Clau**
- **Sistema obsolet**: Ubuntu 8.04 (EOL des de 2011)
- **Serveis insegurs**: rlogin, rexec oberts sense autenticació
- **Backdoors**: Múltiples ports amb accés no autoritzat
- **Configuracions perilloses**: Permisos excessius, passwords per defecte

### **Implicacions de Seguretat**
Si aquest sistema estigués en producció:
- ❌ **Exposició total** a atacs externs
- ❌ **Pèrdua de dades** garantida
- ❌ **Compromís de xarxa** (salt a altres sistemes)
- ❌ **Incompliment de LOPD/RGPD**

## 🛡 **Recomanacions de Mitigació**

### **Immediates**
1. **Desactivar serveis innecessaris**
   - rlogin, rexec, vsftpd vulnerable
2. **Actualitzar el sistema operatiu**
   - Migrar a una versió suportada
3. **Canviar credencials per defecte**
   - Especialment usuaris amb privilegis

### **A Mig Termini**
1. **Implementar firewall**
   - Només ports estrictament necessaris
2. **Monitorització contínua**
   - Escaneigs regulars de vulnerabilitats
3. **Polítiques de hardening**
   - Seguir guies CIS Benchmark

## 📚 **Aprenentatges Clau**

### **Tècnics**
- Configuració d'eines professionals de pentesting
- Interpretació de CVSS i nivells de severitat
- Configuració de xarxes virtuals complexes
- Anàlisi d'informes de vulnerabilitats

### **Conceptuals**
- Entendre l'impacte de les vulnerabilitats
- Valorar la importància de les actualitzacions
- Conèixer les millors pràctiques de seguretat
- Aprendre a prioritzar riscos

## 🎓 **Competències Adquirides**

| Competència | Nivell Assolit |
|-------------|----------------|
| Detecció de vulnerabilitats | ⭐⭐⭐⭐⭐ |
| Configuració d'eines de seguretat | ⭐⭐⭐⭐ |
| Anàlisi de riscos | ⭐⭐⭐⭐⭐ |
| Virtualització avançada | ⭐⭐⭐⭐ |
| Documentació tècnica | ⭐⭐⭐⭐⭐ |

## 📈 **Avaluació de Resultats**

**Resultat de l'escaneig:** **ALTAMENT VULNERABLE**  
**Recomanació:** **REINSTAL·LACIÓ COMPLETA DEL SISTEMA**

Aquesta pràctica demostra la importància crítica de:
1. **Manteniment regular** dels sistemes
2. **Escaneigs periòdics** de vulnerabilitats
3. **Formació contínua** en seguretat
4. **Cultura de seguretat** a les organitzacions

## 🤝 **Contribucions**

Aquesta guia ha estat desenvolupada com a part del projecte del cicle formatiu de **Administració de Sistemes Informàtics en Xarxa**, integrant coneixements de:
- Sistemes Operatius en Xarxa
- Seguretat Informàtica
- Serveis de Xarxa
- Projecte Intermodular

## 📄 **Llicència**

Material educatiu - Ús lliure per a finalitats acadèmiques.

---
**Realitzat per:** [El teu nom]  
**Data:** Febrer 2026  
**Curs:** ASIX - Seguretat Informàtica  

> *Recorda: La seguretat no és un producte, és un procés continu.*

[![OpenVAS](https://img.shields.io/badge/Powered%20by-OpenVAS-brightgreen)](https://www.openvas.org/)
[![Metasploitable](https://img.shields.io/badge/Target-Metasploitable%202.0-lightgrey)](https://docs.rapid7.com/metasploit/metasploitable-2/)