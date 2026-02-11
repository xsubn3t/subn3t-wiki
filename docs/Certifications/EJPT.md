# [Review] eJPTv2 - Junior Penetration Tester

<p align="center">
  <img src="../../assets/ejpt-cert.png" alt="Certification eJPT" width="400">
</p>

| Organisme | Format | Environnement | Durée |
| :--- | :--- | :--- | :--- |
| **INE Security** | 100% Pratique (Black Box) | Browser-Based (Kali) | 48 Heures |

---

## 🎯 Contexte & Approche
Contrairement aux CTF classiques type "Capture The Flag", l'eJPTv2 simule un véritable engagement de pentest professionnel. Je n'ai pas eu à chercher des fichiers `root.txt` cachés sans logique, mais à répondre à des questions concrètes d'audit (versions de services, mots de passe utilisateurs, données exfiltrées).

**Le défi :** Une lettre d'engagement, une plage d'IPs, et 48h pour compromettre une DMZ et pivoter vers le réseau interne.

---

## 🔍 Phase 1 : Reconnaissance & Énumération
L'examen met l'accent sur la capacité à cartographier un réseau inconnu. J'ai dû identifier plusieurs machines (Windows & Linux) avec des surfaces d'attaque très différentes.

### Services Rencontrés
Mes scans ont révélé une infrastructure mixte nécessitant de la polyvalence :

* **Web & CMS :** Identification de serveurs Apache/IIS hébergeant des CMS comme **WordPress** et **Drupal**. L'énumération via `wpscan` et l'analyse des plugins étaient cruciales.
* **Partages de Fichiers :** Découverte de services **FTP** mal configurés (accès Anonymous autorisé) et de partages **SMB/Samba** ouverts.
* **Accès Distants :** Présence de services SSH et RDP sur des serveurs Windows Server (2012/2019) et Linux (Ubuntu).

!!! tip "Méthodologie"
    L'erreur fatale est de foncer sur Metasploit. J'ai passé les premières heures à analyser manuellement chaque port. Un simple fichier oublié sur un FTP Anonyme peut contenir les crédentiels pour toute la suite.

---

## ⚔️ Phase 2 : Exploitation & Post-Exploitation
Une fois les vecteurs identifiés, l'exploitation a demandé de combiner outils automatisés et compréhension des failles.

### Techniques Utilisées
1.  **Brute-Force Ciblé :** Utilisation de **Hydra** pour compromettre des accès SSH/RDP après avoir identifié des noms d'utilisateurs potentiels lors de l'énumération.
2.  **Exploitation Web :** Injection SQL et exploitation de failles connues sur les CMS pour obtenir un premier accès shell (`www-data`).
3.  **Privilege Escalation :** Énumération locale (SUID, Kernel, Mauvaises configurations) pour passer Root/System.

### Le Challenge du Pivoting
C'est le cœur de la v2. Une fois la première machine compromise, il fallait accéder à d'autres réseaux invisibles depuis ma machine d'attaque.
* **Outil :** Utilisation du module `autoroute` de Metasploit et de `proxychains`.
* **Objectif :** Router mon trafic à travers la machine compromise pour scanner et attaquer les serveurs de base de données internes.

---

## 🛠️ Mon Arsenal (Tech Stack)

J'ai principalement utilisé les outils standards de Kali Linux, maitrisés durant la préparation :

| Catégorie | Outils Clés |
| :--- | :--- |
| **Network & Discovery** | `Nmap` (Scripts NSE), `fping`, `Wireshark` |
| **Enumeration** | `Enum4linux` (SMB), `Smbmap`, `Burp Suite` |
| **Exploitation** | `Metasploit Framework` (Multi/Handler), `SQLMap` |
| **Cracking** | `Hydra`, `John The Ripper` |

---

## 💡 Retour d'Expérience & Conseils

Si vous préparez cette certification, voici mes recommandations basées sur mon examen :

1.  **L'Énumération est Reine :** Ne négligez aucun port. Un service HTTP sur un port non standard (ex: 8080, 8000) cache souvent l'entrée critique.
2.  **Maîtrisez le Routing :** Si vous ne savez pas faire un scan Nmap à travers une session Meterpreter (Pivoting), vous serez bloqué à la moitié de l'examen.
3.  **Notez Tout :** J'ai utilisé CherryTree/Obsidian pour documenter chaque IP. Avec plusieurs machines et réseaux, on se perd vite sans notes rigoureuses.

!!! success "Conclusion"
    L'eJPTv2 est une excellente validation des compétences opérationnelles. Elle prouve qu'on sait non seulement lancer des outils, mais surtout **comprendre** le réseau et **pivoter** pour atteindre l'objectif final.

---
[⬅️ Retour aux Home](../index.md)
