# Quick Start for Drupal 9 and Lando

All of the bash commands in this document must be run in repo root.

After cloning the repo, you're free to delete the `.git` directory.

```bash
rm -rf ./.git/
```

## Prepare Code base

```bash
lando start
```

After starting Lando, you will see the URLs. Please do not visit them at this moment.

![URLs](https://i.imgur.com/LlN94Ls.png)

Continue running the command below:

```bash
lando composer create-project drupal/recommended-project /app/temp --no-install

rsync -rtv --remove-source-files ./temp/ ./drupal/

find ./temp -type d -empty -delete # or run `rm -rf ./temp/`

rm ./drupal/web/.gitkeep

lando composer install # do not forget to confirm plugins when prompted
```

Note: This is resolved. Please see [Composer v2.2 prompts to authorize plugins](https://www.drupal.org/project/drupal/issues/3255749) and [Composer 2.2+ Authorized Plugins](https://www.drupal.org/node/3294646).

![Allow plugins](https://i.imgur.com/AKjMevW.png)

Install drush

```bash
lando composer require "drush/drush"

# Test drush
lando drush --version
```

## Install Site

### Manual Installation via Browser

You can now visit the URLs mentioned above and perform an installation via browser:

![Drupal Installation](https://i.imgur.com/M3YcTOL.png)

### Automated Installation via drush

#### Standard Drupal Installation

This will perform a standard Drupal installation:

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  standard \
  --site-name='Drupal using Lando' \
  --locale=en \
  --db-url=mysql://drupal9:drupal9@database:3306/drupal9 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

#### Standard Drupal Installation in Another Language

If you want to perform a standard Drupal installation with a different language, change the `locale` option (in this example `tr` (Turkish) is used):

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  standard \
  --site-name='Drupal using Lando' \
  --locale=tr \
  --db-url=mysql://drupal9:drupal9@database:3306/drupal9 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

#### Install Umami Demo Profile

This is a multi-lingual Drupal demo containing realistic content:

```bash
# Ref: https://drushcommands.com/drush-9x/site/site:install/
# drush si --db-url=mysql://root:pass@localhost:port/dbname
lando drush site-install \
  demo_umami \
  --site-name='Umami Food Magazine' \
  --db-url=mysql://drupal9:drupal9@database:3306/drupal9 \
  --account-name=admin \
  --account-pass=admin \
  --yes
```

## Admin Interface

Visit `https://dev-drupal9.lndo.site/user/login`.

If 'Automated Installation via drush' is used for installation, use `admin` for both username and password.

## Environment Information

The operating system and other software used are as follows:

```txt
lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 20.04.4 LTS
Release:	20.04
Codename:	focal

lando version
v3.6.4

docker --version
Docker version 20.10.17, build 100c701

docker-compose --version
docker-compose version 1.29.1, build c34c88b2
```
