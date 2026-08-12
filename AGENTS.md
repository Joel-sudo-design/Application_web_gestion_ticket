# Gestion ticket — contexte durable

## Stack et environnement local

- Application Symfony sous PHP 8.4 et FrankenPHP.
- Frontend Webpack Encore avec Node.js 22 et Yarn.
- Données SQL sous MariaDB et données NoSQL sous MongoDB.
- Environnement Docker Compose : projet `appli_web_gestion_ticket`.
- URL locale documentée : `http://localhost:8000`.
- L'application n'est pas encore déployée. Le domaine prévu est `https://support.joeldermont.fr`, mais il ne doit pas être utilisé comme preuve d'un environnement existant.
- Conteneurs Compose : `appli_web_gestion_ticket`, `symfony_db_prod_appli_web_gestion_ticket`, `mongo_prod_appli_web_gestion_ticket`, `phpmyadmin_appli_web_gestion_ticket` et `mongo_express_appli_web_gestion_ticket`.

## Vérifications

- Installer les dépendances frontend : `yarn install --frozen-lockfile`.
- Compiler les assets : `yarn build`.
- Auditer le frontend : `yarn audit --level low`.
- Valider Composer : `composer validate --strict --no-check-publish`.
- Auditer Composer : `composer audit --locked`.
- Exécuter les tests : `php bin/phpunit`.
- Valider Compose : `docker compose config`.
- Construire l'image : `docker build --tag application_web_gestion_ticket:local .`.
- Après une modification d'interface, vérifier localement les formats ordinateur, tablette et mobile, la console et les requêtes réseau.

## CI, déploiement et données

- Le workflow `.github/workflows/deploy.yml` contient une procédure de déploiement, mais il est désactivé manuellement sur GitHub tant que l'application n'est pas déployée. Ne pas le réactiver sans demande explicite.
- Un déploiement normal doit préserver les volumes MariaDB, MongoDB, `public/ticket_image` et le fichier d'environnement de la cible.
- Les secrets restent dans l'environnement sécurisé ou les secrets GitHub et ne doivent jamais entrer dans le dépôt.
- Les migrations de MariaDB ou MongoDB exigent une sauvegarde vérifiée, un essai sur un volume jetable et une procédure de retour arrière.

## Maintenance des dépendances

- Dependabot couvre Composer, npm, Docker, Docker Compose et GitHub Actions.
- Toute proposition doit réussir les audits, les tests applicatifs et la construction de l'image avant fusion.
- Ne jamais fusionner une mise à jour uniquement parce qu'elle est générée automatiquement.
