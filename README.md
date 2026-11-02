# cf2d-claude-config

Exemple de configuration Claude Anthropic novembre 2026

## WSL sous Windows 11

Pour utiliser cf2d-claude-config sous Windows 11, il est recommandé d'utiliser WSL (Windows Subsystem for Linux). Voici les étapes pour configurer votre environnement :

**Installez WSL** : Ouvrez PowerShell en tant qu'administrateur et exécutez la commande suivante pour installer WSL avec Ubuntu :

   ```powershell
   wsl --install -d Ubuntu
   ```
## Installez les dépendances nécessaires

Vérifiez l'existence de PHP et installez-le si nécessaire. Vous pouvez vérifier la version de PHP avec la commande suivante :

   ```bash
   php -v
   ```

Installez Composer, un gestionnaire de dépendances pour PHP, en suivant les instructions sur le site officiel : [https://getcomposer.org/download/](https://getcomposer.org/download/)

Continuons avec git. Vérifiez si git est installé avec la commande suivante :

   ```bash
   git --version
   ```

Vérifiez si Node.js est installé avec la commande suivante :

   ```bash
   node -v
   ```

Installez Node.js si nécessaire en suivant les instructions sur le site officiel : [https://nodejs.org/](https://nodejs.org/)   

Vérifiez si npm est installé avec la commande suivante :

   ```bash
   npm -v
   ```

Installez npm si nécessaire en suivant les instructions sur le site officiel : [https://www.npmjs.com/get-npm](https://www.npmjs.com/get-npm)

Vérifiez si Python est installé avec la commande suivante :

   ```bash
   python3 --version
   ```

Installez Python si nécessaire en suivant les instructions sur le site officiel : [https://www.python.org/downloads/](https://www.python.org/downloads/)    

Vérifiez si docker est installé avec la commande suivante :

   ```bash
   docker --version
   ```

Installez Docker si nécessaire en suivant les instructions sur le site officiel, prenez la version Windows, puis y activer le WSL : [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)