# Advanced System Maintenance Suite - Edition Restructurée

[Menu de sauvegarde et de restauration](https://github.com/Abdelhakim-Baalla/Advanced-System-Maintenance-terminal/blob/main/menus/backup-recovery.bat)

## Présentation Générale

La suite Advanced System Maintenance Suite (ASMS) est un ensemble d’outils batch professionnels pour la maintenance, l’optimisation, la sécurité et l’administration avancée de Windows. Elle vise à automatiser les tâches courantes et avancées d’entretien système, tout en offrant une architecture modulaire et extensible pour les utilisateurs et les développeurs.

---

## Table des matières

- [Fonctionnalités principales](#fonctionnalités-principales)
- [Installation & Prérequis](#installation--prérequis)
- [Guide d’utilisation (utilisateur)](#guide-dutilisation-utilisateur)
- [Guide technique (développeur)](#guide-technique-développeur)
- [Architecture & Design](#architecture--design)
- [Personnalisation & Extension](#personnalisation--extension)
- [Avertissements & Support](#avertissements--support)
- [Auteur & Licence](#auteur--licence)

---

## Fonctionnalités principales

- **Maintenance système** : Nettoyage, réparation, vérification d’intégrité, gestion des logs, etc.
- **Optimisation** : RAM, SSD, CPU, GPU, réseau, démarrage, jeux, etc.
- **Sécurité** : Pare-feu, audit, suppression de bloatware, durcissement de la confidentialité.
- **Administration** : Variables d’environnement, services, tâches planifiées, gestion des partitions/disques.
- **Sauvegarde & Restauration** : Sauvegarde de fichiers, points de restauration, export de rapports système.
- **Outils avancés** : Analyse de drivers, logs, paquets, forensics, macros, etc.
- **Interface animée** : Menus interactifs, animations, couleurs, effets visuels.

---

## Installation & Prérequis

- **OS** : Windows 7/8/10/11 (x64 recommandé)
- **Droits administrateur** : nécessaires pour la plupart des scripts
- **Outils natifs** : cmd, PowerShell, utilitaires système (DISM, SFC, etc.)
- **Aucune installation externe** requise (sauf pour certains modules avancés : winget, etc.)

---

## Guide d’utilisation (utilisateur)

### Lancement global

1. **Menu principal**
   - Lancez `master-control.bat` pour accéder à l’interface principale.
   - Naviguez dans les menus pour choisir la catégorie d’outils.

2. **Outil individuel**
   - Double-cliquez sur le script `.bat` voulu dans `advanced-tools/` ou exécutez-le via l’invite de commandes.

### Conseils d’utilisation

- **Sauvegardez vos données** avant toute opération de nettoyage ou de réparation.
- **Lisez les messages à l’écran** : chaque script affiche des instructions ou avertissements.
- **Certains outils peuvent redémarrer le PC ou fermer des applications**.
- **Pour les outils marqués “À compléter”** : fonctionnalité en cours de développement, ne pas utiliser en production.

### Exemples d’outils courants

- `quick-cleanup.bat` : Nettoyage rapide du dossier Temp et de la corbeille.
- `nuclear-cleanup.bat` : Nettoyage approfondi de tous les fichiers temporaires système.
- `env-manager.bat` : Affichage des variables d’environnement.
- `event-log-viewer.bat` : Ouvre l’observateur d’événements Windows.
- `export-system-report.bat` : Exporte un rapport système sur le bureau.
- `feature-manager.bat` : Affiche la liste des fonctionnalités Windows activées/désactivées.
- `file-backup.bat` : Sauvegarde le dossier Documents sur le bureau.
- `firewall-config.bat` : Active le pare-feu Windows et configure les règles de base.
- `health-check.bat` : Vérifie l’intégrité système et la santé du disque.
- `network-opt.bat` : Optimisation TCP/IP et flush DNS.
- `sfc-scan.bat` : Analyse et réparation des fichiers système (SFC).

---

## Guide technique (développeur)

### Structure du projet

- `advanced-tools/` : scripts batch spécialisés (un outil = un script)
- `menus/` : scripts de menus interactifs
- `utils/` : utilitaires communs (animations, helpers)
- `custom/` : scripts personnalisés par l’utilisateur
- `backup/` : scripts de sauvegarde

### Bonnes pratiques de développement

- **Modularité** : chaque script doit être autonome, mais peut utiliser les utilitaires communs (`animation-utils.bat`).
- **Réutilisation** : centralisez les fonctions d’affichage, d’animation, de gestion des couleurs dans `animation-utils.bat`.
- **Commentaires** : documentez chaque script (but, usage, avertissements).
- **Sécurité** : validez les entrées utilisateur, évitez les suppressions irréversibles sans confirmation.
- **Extensibilité** : pour chaque nouveau module, suivez le modèle existant (intro, animation, action principale, pause/exit).

### Exemple de architecture pour un nouvel outil

```bat
@echo off
REM [Nom de l’outil] - Advanced Tool
call ..\animation-utils.bat :SHOW_DEVELOPER_INFO
call ..\animation-utils.bat :SPINNER_ANIMATION "Nom de l’outil"
cls
color 0X
echo [1/1] Description de l’action...
REM -- Placez ici la logique principale --
echo.
pause
exit /b
```

### Ajout d’un nouvel outil

1. Créez un nouveau fichier `.bat` dans `advanced-tools/`.
2. Utilisez le squelette ci-dessus.
3. Ajoutez votre outil dans le menu concerné (`menus/`).
4. Testez en mode administrateur.

### Utilisation des utilitaires communs

- `animation-utils.bat` : contient les fonctions d’animation, d’affichage, de couleurs, etc.
- `matrix.vbs` : animation Matrix pour l’intro.

---

## Architecture & Design

### Améliorations visuelles recommandées

- **Uniformisez les couleurs** par catégorie d’outil (ex : sécurité = magenta, optimisation = jaune, etc.).
- **Ajoutez des barres de progression** ou des animations pour les opérations longues.
- **Utilisez des cadres ASCII** pour structurer les menus et les sorties.
- **Ajoutez un logo ASCII** ou une bannière en haut de chaque script.

### Améliorations fonctionnelles

- **Ajoutez un système de logs** (fichier texte) pour tracer les actions effectuées.
- **Proposez une confirmation avant toute suppression ou modification système critique.**
- **Ajoutez des options de ligne de commande** pour automatiser certains outils (ex : `script.bat /silent`).
- **Centralisez la gestion des erreurs** et affichez des messages clairs en cas d’échec.

### Architecture modulaire

- **Utilisez des sous-programmes** (`:label` + `goto`) pour séparer l’affichage, la logique, la sortie.
- **Créez un fichier de configuration global** (ex : `config.bat`) pour les chemins, options par défaut, etc.
- **Préparez des hooks** pour permettre à l’utilisateur d’ajouter ses propres scripts dans les menus.

---

## Personnalisation & Extension

- **Ajoutez vos propres scripts** dans `custom/` et référencez-les dans les menus.
- **Modifiez les menus** dans `menus/` pour ajouter ou retirer des outils selon vos besoins.
- **Adaptez les couleurs et animations** dans `animation-utils.bat` pour correspondre à votre charte graphique.

---

## Avertissements & Support

- **Utilisation à vos risques et périls.**
- **Sauvegardez vos données** avant toute opération de nettoyage ou de réparation.
- **Contactez le développeur** pour toute suggestion ou bug (voir en-tête des scripts).

---

## Auteur & Licence

Développé par Abdelhakim Baalla  
Version : 2.5  
Licence : Usage personnel/professionnel autorisé, distribution interdite sans autorisation.

---

**Pour toute contribution, suivez les bonnes pratiques ci-dessus et proposez vos améliorations via un fork ou un patch.**
