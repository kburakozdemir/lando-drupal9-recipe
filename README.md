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

rsync -rtv --remove-source-files ./temp/ ./drupal/

find ./temp -type d -empty -delete # or run `rm -rf ./temp/`

rm ./drupal/web/.gitkeep

lando composer install

lando composer require "drush/drush"

# Test drush
lando drush --version
```

## Install Site

This will perform a standard Drupal installation:

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  standard \
  --locale=en \
  --db-url=mysql://drupal9:drupal9@database:3306/drupal9 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

If you want to perform a standard Drupal installation with a different language, change the `locale` option (in this example `tr` (Turkish) is used):

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

## Environment Information

The operating system and other software used are as follows:

```txt
lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 18.04.6 LTS
Release:        18.04
Codename:       bionic

lando version
v3.4.2

docker --version
Docker version 20.10.11, build dea9396

docker-compose --version
docker-compose version 1.29.1, build c34c88b2
```
