# 🛡️ AI-Driven Network Intrusion Detection System (NIDS)

## 📝 Vue d'ensemble (Overview)
Ce projet présente la conception de bout en bout d'un Système de Détection d'Intrusion Réseau (NIDS) propulsé par l'apprentissage automatique. Pour pallier le vieillissement des jeux de données publics, ce projet introduit une méthodologie hybride rigoureuse pour la création d'un dataset moderne et équilibré : la capture d'attaques réelles via des honeypots combinée à la génération de trafic bénin synthétique.

L'ingénierie des caractéristiques (Feature Engineering) suit scrupuleusement la méthodologie du célèbre dataset **UNSW-NB15**, rendant les données prêtes pour l'entraînement de modèles de détection avancés.

## 🚀 Méthodologie et Ingénierie des Données

### 1. Collecte des Menaces (Malicious Traffic)
Pour obtenir des vecteurs d'attaques modernes et réels (Zero-Day, Scans, Exploits), nous avons déployé une architecture de leurre.
*   **Plateforme :** **T-Pot** (Multi-Honeypot Platform).
*   **Action :** Exposition de l'environnement pour capturer les journaux et les captures de paquets (PCAP) d'attaquants réels sur une période définie.

### 2. Génération de Trafic Légitime (Benign Traffic)
Pour équilibrer les données de la cible et éviter le surapprentissage (overfitting) du modèle d'IA, un environnement contrôlé a été mis en place.
*   **Environnement :** Machine virtuelle sous environnement Debian/Linux.
*   **Outil d'automatisation :** Scripts Python utilisant **Scapy**.
*   **Action :** Simulation et génération de trafic réseau bénin réaliste (requêtes HTTP, requêtes DNS, connexions SSH) exporté au format PCAP.

### 3. Extraction des Caractéristiques (Argus & UNSW-NB15)
L'étape cruciale pour transformer le trafic brut en données exploitables par l'IA. La méthodologie s'aligne sur les standards de l'UNSW-NB15.
*   **Outil d'ingénierie :** **Argus** (Audit Record Generation and Utilization System).
*   **Processus :** Les fichiers PCAP (Attaques + Bénins) sont ingérés par le démon `argus`. Le client `ra` convertit ensuite ces paquets bruts en enregistrements de flux bidirectionnels détaillés.
*   **Caractéristiques (Features) :** Extraction des métadonnées critiques (durée du flux, volume d'octets source/destination, Time-to-Live, états TCP).
*   **Étiquetage :** Classification des flux exportés en format CSV (0 = Trafic Légitime, 1 = Attaque).

## 🛠️ Stack Technique
*   **Capture & Réseau :** T-Pot, Scapy, TCP/IP
*   **Ingénierie de données :** Argus (Audit Record Generation and Utilization System)
*   **Machine Learning :** Python 3, Pandas, Scikit-Learn / TensorFlow
*   **Infrastructure :** Linux/Debian Server, Virtualisation



