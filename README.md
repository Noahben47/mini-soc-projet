# 🛡️ Mini-SOC Lab — Projet Cybersécurité

> Laboratoire Security Operations Center miniature déployé dans le cadre du M2 Cybersécurité & Sciences des Données à l'Université Paris 8.


## Contexte

Ce projet a été réalisé dans le cadre du Master 2 Cybersécurité & Sciences des Données (Université Paris 8). L'objectif était de concevoir, déployer et tester un **SOC miniature** capable de détecter, analyser et répondre à des incidents de sécurité en environnement virtualisé.

---

##  Objectifs

- Déployer une chaîne complète de détection (HIDS + NIDS) avec **Wazuh** et **Suricata**
- Centraliser les alertes dans une plateforme de gestion d'incidents (**TheHive**)
- Simuler des scénarios d'attaque réalistes et mesurer la capacité de détection
- Documenter les processus de réponse à incident

---

## Architecture

```
┌─────────────────┐         ┌──────────────────┐
│   Kali Linux    │────────▶│  Machines cibles │
│   (Attaquant)   │ Attaque │   (Windows/Linux)│
└─────────────────┘         └────────┬─────────┘
                                     │ Logs
                            ┌────────▼────────┐
                            │    Wazuh HIDS   │
                            │  Suricata NIDS  │
                            └────────┬────────┘
                                     │ Alertes
                            ┌────────▼────────┐
                            │    TheHive      │
                            │  (Gestion       │
                            │   d'incidents)  │
                            └─────────────────┘
```

---

##  Technologies utilisées

| Outil | Rôle | Version |
|-------|------|---------|
| **Wazuh** | HIDS — Détection d'intrusion côté hôte | 4.x |
| **Suricata** | NIDS — Détection d'intrusion réseau | 7.x |
| **TheHive** | Plateforme de gestion d'incidents (SIRP) | 5.x |
| **Wireshark** | Analyse de trafic réseau | — |
| **Kali Linux** | Environnement d'attaque | 2024.x |
| **VirtualBox / VMware** | Virtualisation | — |

---

##  Scénarios testés

### Scénario 1 — Attaque par force brute SSH
- **Objectif** : Détecter des tentatives massives de connexion SSH
- **Outil d'attaque** : Hydra depuis Kali Linux
- **Détection** : Wazuh (règle 5712 — authentification SSH échouée)
- **Résultat** :  Alerte remontée dans TheHive en < 30 secondes


### Scénario 2 — Scan réseau (reconnaissance)
- **Objectif** : Détecter un scan Nmap sur le réseau interne
- **Outil d'attaque** : Nmap (scan SYN, scan agressif)
- **Détection** : Suricata (règles ET OPEN)
- **Résultat** :  Signature détectée, alerte ingérée dans TheHive



---

##  Résultats et apprentissages

**Points clés** :
- Maîtrise du cycle complet de détection → alerte → investigation → réponse
- Prise en main des règles SIGMA et des signatures Suricata
- Compréhension des limites des solutions open-source en conditions réelles
- Importance de la corrélation d'événements entre HIDS et NIDS

**Axes d'amélioration identifiés** :
- Intégration d'un SIEM central (ex: Elastic SIEM)
- Automatisation de la réponse via des playbooks Cortex
- Ajout de sources de logs réseau (DNS, proxy)

---


##  Auteur

**Adem BENALI**
Étudiant M2 Cybersécurité & Sciences des Données — Université Paris 8
Data Engineer en alternance @ SNCF Réseau

-  [LinkedIn]([https://www.linkedin.com/in/ton-profil](https://www.linkedin.com/in/benali-adem-732193250/))
-  Disponible pour alternance **Data Engineer / Data Scientist / Data Analyst — septembre 2026**

---

##  Licence

Projet académique à but pédagogique. Voir [LICENSE](LICENSE).

