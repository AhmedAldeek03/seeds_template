# Seeds template

A Seeds site whose features are added from the admin UI.

Installing the template sets up **Seeds base** (the Seeds foundation, replacing the Seeds install
profile) and **Project Browser**. All our feature recipes come with it, already downloaded, and
are listed under **Extend > Browse > Recommended add-ons**. An admin adds a feature with one
click on **Install**.

| Add-on | Adds |
|---|---|
| News & Events | News and Event types, home and compiled blocks, Seeds UI cards |
| Local Reach | Key figures, progress bars, ring charts, country flags, institution summary (Canvas) |
| Slider | Slide type and carousel |
| FAQ | FAQ type with categories, accordion block |
| Gallery | Photo and video albums |
| Partners | Partner and client logos |
| Team | Staff and board members |
| Publications | Annual reports and studies with files |
| Contact form | "Contact us" form at `/contact-us` |
| Newsletter | Simplenews setup (asks for the sender address and name) |

Installed add-ons show **Installed** and can be reapplied.

## Install a new site

1. Require the template with Composer. All the feature recipes come with it:

   ```bash
   composer require drupal/seeds_template
   ```

2. Add this line to `settings.php`. The one-click **Install** button uses core's Package
   Manager, which is still experimental in Drupal 11.4 and must be allowed explicitly:

   ```php
   $settings['testing_package_manager'] = TRUE;
   ```

3. Install the site from the template:

   ```bash
   drush site:install ../recipes/seeds_template --account-name=admin --site-name="My site"
   ```

With DDEV, put `ddev` before the commands.

## Adding a feature without the UI

Every add-on is a normal recipe, so developers can also apply it with Drush:

```bash
drush recipe ../recipes/faq_recipe
```

## Changing the list

The add-ons list is `content/file/recommended-add-ons.yaml`. Each entry needs the recipe's
Composer package name and must also be required in this recipe's `composer.json`, so it is
already downloaded when an admin clicks Install.

## Requirements

- All recipes must sit in the same `recipes/` folder (Composer puts them there), because recipes
  include each other by name.
- The project needs the two Seeds module patches listed in the Seeds base README
  (`seeds_toolbar` install crash, `restrict_ip` with Canvas).
