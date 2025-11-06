<!--
  - SPDX-FileCopyrightText: 2024 Nextcloud GmbH and Nextcloud contributors
  - SPDX-License-Identifier: AGPL-3.0-or-later
-->
# Guide d'Installation

Ce guide vous aidera à installer l'application Nextcloud Assistant sur votre instance Nextcloud.

## Prérequis

- Nextcloud version 30 ou supérieure (jusqu'à la version 33)
- PHP et serveur web configurés pour Nextcloud
- Accès administrateur à votre instance Nextcloud

## Méthodes d'Installation

### Méthode 1 : Via la boutique d'applications Nextcloud (Recommandé)

C'est la méthode la plus simple et recommandée pour la plupart des utilisateurs :

1. Connectez-vous à votre instance Nextcloud en tant qu'administrateur
2. Cliquez sur votre avatar utilisateur dans le coin supérieur droit
3. Sélectionnez **Applications** dans le menu déroulant
4. Dans la page Applications, sélectionnez la catégorie **IA** ou **Intégration** dans la barre latérale gauche
5. Trouvez **Nextcloud Assistant** dans la liste
6. Cliquez sur le bouton **Télécharger et activer**

L'application sera automatiquement téléchargée, installée et activée.

### Méthode 2 : Installation manuelle depuis une version publiée

Si vous préférez installer manuellement ou si la boutique d'applications n'est pas disponible :

1. Téléchargez la dernière version depuis la [page des versions GitHub](https://github.com/nextcloud/assistant/releases)
2. Extrayez l'archive
3. Téléversez le dossier `assistant` dans le répertoire `apps` de votre Nextcloud :
   ```bash
   cp -r assistant /chemin/vers/nextcloud/apps/
   ```
4. Définissez les permissions correctes :
   ```bash
   chown -R www-data:www-data /chemin/vers/nextcloud/apps/assistant
   ```
5. Activez l'application en utilisant la commande `occ` :
   ```bash
   sudo -u www-data php /chemin/vers/nextcloud/occ app:enable assistant
   ```
   Ou activez-la depuis l'interface web de Nextcloud (page Applications)

### Méthode 3 : Installation depuis les sources (Pour les développeurs)

Si vous souhaitez contribuer ou tester la dernière version de développement :

1. Clonez le dépôt :
   ```bash
   cd /chemin/vers/nextcloud/apps/
   git clone https://github.com/nextcloud/assistant.git
   cd assistant
   ```

2. Installez les dépendances et compilez l'application :
   ```bash
   make build
   ```
   
   Cela va :
   - Installer les dépendances PHP via Composer
   - Installer les dépendances JavaScript via npm
   - Compiler les ressources frontend

3. Définissez les permissions correctes :
   ```bash
   chown -R www-data:www-data /chemin/vers/nextcloud/apps/assistant
   ```

4. Activez l'application :
   ```bash
   sudo -u www-data php /chemin/vers/nextcloud/occ app:enable assistant
   ```

## Configuration Post-Installation

### Installation des fournisseurs IA

L'application Assistant nécessite des applications de fournisseurs IA pour fonctionner. Vous devez installer au moins une application de fournisseur pour le traitement de texte, la génération d'images ou la transcription audio.

#### Fournisseurs de traitement de texte

- **[Modèle de langage local (LLM)](https://github.com/nextcloud/llm2)** - Exécutez des modèles IA localement
- **[Intégration OpenAI/LocalAI](https://apps.nextcloud.com/apps/integration_openai)** - Utilisez les services OpenAI ou LocalAI

#### Fournisseurs de génération d'images

- **[Intégration OpenAI/LocalAI](https://apps.nextcloud.com/apps/integration_openai)**
- **[Text2Image Stable Diffusion](https://apps.nextcloud.com/apps/text2image_stablediffusion)**

#### Fournisseurs de transcription audio (Speech-to-Text)

- **[Intégration OpenAI/LocalAI](https://apps.nextcloud.com/apps/integration_openai)**
- **[Local Whisper Speech-To-Text](https://apps.nextcloud.com/apps/stt_whisper)**

Installez ces fournisseurs depuis la boutique d'applications Nextcloud de la même manière que vous avez installé l'application Assistant.

### Vérification de l'installation

1. Après l'installation, vous devriez voir une nouvelle icône dans le menu d'en-tête en haut à droite (à côté de votre avatar utilisateur)
2. Cliquez sur cette icône pour ouvrir l'interface de l'Assistant
3. Si aucun type de tâche n'apparaît, vous devez installer et configurer des applications de fournisseurs IA (voir ci-dessus)

## Dépannage

### L'application n'apparaît pas dans la liste des Applications

- Assurez-vous que votre version de Nextcloud est entre 30 et 33
- Vérifiez les journaux Nextcloud pour toute erreur : `/chemin/vers/nextcloud/data/nextcloud.log`

### L'icône de l'Assistant n'apparaît pas dans l'en-tête

- Videz le cache de votre navigateur
- Vérifiez que l'application est activée : `sudo -u www-data php occ app:list`
- Vérifiez que l'application a été correctement compilée si elle a été installée depuis les sources

### Aucun type de tâche disponible

- Installez au moins une application de fournisseur IA (voir Configuration Post-Installation ci-dessus)
- Configurez l'application de fournisseur dans les paramètres Nextcloud

### Erreurs de permissions

Assurez-vous que l'utilisateur du serveur web (généralement `www-data`, `nginx` ou `apache`) possède les fichiers de l'application :
```bash
chown -R www-data:www-data /chemin/vers/nextcloud/apps/assistant
```

## Ressources supplémentaires

- [Documentation utilisateur](./user) - Comment utiliser l'Assistant
- [Documentation développeur](./developer) - Intégration et documentation de l'API
- [Documentation administrateur](https://docs.nextcloud.com/server/latest/admin_manual/ai/index.html) - Configuration IA de Nextcloud
- [Problèmes GitHub](https://github.com/nextcloud/assistant/issues) - Signaler des bugs ou demander des fonctionnalités

## Désinstallation

Pour désinstaller l'application Assistant :

1. Via l'interface web : Allez sur la page Applications, trouvez Assistant, et cliquez sur **Supprimer**
2. Via la ligne de commande :
   ```bash
   sudo -u www-data php /chemin/vers/nextcloud/occ app:disable assistant
   sudo -u www-data php /chemin/vers/nextcloud/occ app:remove assistant
   ```
