# Quick Start

```bash
lando start

lando composer create-project drupal/recommended-project /app/temp --no-install

cp ./temp/* ./drupal/

rm -rf ./temp/

rm ./drupal/web/.gitkeep

lando composer require "drush/drush" --no-update

lando composer install
```

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  standard \
  --locale=tr \
  --db-url=mysql://drupal9:drupal9@database:3306/drupal9 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```
