# Raccourcis

## Dans WSL2
Ouvrir le fichier `~/.bashrc` avec nano :

        nano ~/.bashrc

### Les aliases à ajouter à la fin du fichier `~/.bashrc` :

```bash
# Docker Compose
alias dup='docker compose up -d --build'
alias ddo='docker compose down'
alias uphp='docker compose exec php sh'
alias dphp='docker compose exec -it php bash'
```

Dans le conteneur PHP, il faut ajouter les commandes suivantes, vous pouvez ensuite utiliser après un `uphp` les commandes suivantes :

```bash
# Symfony
alias pbc='php bin/console'
alias pbcc='php bin/console cache:clear'
alias fl='php bin/console doctrine:fixtures:load --group=app --no-interaction'
alias asset='php bin/console cache:clear --env=dev && php bin/console importmap:install && php bin/console asset-map:compile --env=dev'
alias lint='php bin/console lint:twig templates/ && php bin/console lint:yaml config/ && php bin/console lint:container'
```
## Dans Mingw64 de git 

        nano ~/.bashrc

```bash
# git
alias gs='git status'
alias ga='git add .'
alias gc='git commit'
alias gps='git push'
alias gpu='git pull'
alias gr='git remote -v'
alias gb='git branch'
alias gf='git fetch --all'
```