# Quick Start for Drupal 9 and Lando

All of the bash commands in this document must be run in repo root.

After cloning the repo, you're free to delete the `.git` directory.

```bash
rm -rf ./.git/
```

## Prepare Code base

```bash
lando start

lando composer create-project drupal/recommended-project /app/temp --no-install

cp ./temp/* ./drupal/

rm -rf ./temp/

rm ./drupal/web/.gitkeep

lando composer install

lando composer require "drush/drush"

# Test drush
lando drush --version
```

## Install Site

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
