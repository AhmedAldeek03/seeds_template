# Seeds template

A Seeds site whose features are added from the admin UI.

Installing the template sets up **Seeds base** (the Seeds foundation, replacing the Seeds install
profile), the Seeds SEO stack, **ECA** automation, a set of editor tools adopted from Drupal CMS,
and **Project Browser**. All our feature recipes come with it, already downloaded, and are listed
under **Extend > Browse > Recommended add-ons**. An admin adds a feature with one click on
**Install**.

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

## What the template turns on

| Area | Modules |
|---|---|
| Seeds | Seeds base (all Seeds modules and themes), Seeds Layouts, Seeds SEO, Seeds Administration |
| SEO | Metatag (with Open Graph), Simple XML Sitemap, Redirect, Length indicator, Yoast SEO, Token OR |
| Automation | ECA (Core, Base, Config, Content, Form, Misc, Render, UI, User) and the Workflow Modeler |
| Editor experience | Autosave Form, Scheduler, Media Library Bulk Upload, Media Library Edit, Media File Delete, SVG Image, SAM, Tagify, Dashboard, Login with email or username |
| Languages and navigation | Config Language Lock, Easy Breadcrumb |
| Site building | Field UI, Project Browser, Package Manager |

Cookie consent (Klaro) is not included yet.

## SEO

Every content type with its own page gets four SEO fields and a Meta tags field:

| Field | Purpose |
|---|---|
| `field_seo_title` | Overrides the title in search results and when shared |
| `field_seo_description` | Overrides the description |
| `field_seo_image` | Overrides the share image (Media Library) |
| `field_seo_analysis` | Yoast SEO analysis |
| `field_meta_tags` | Advanced tags only (robots, canonical URL), in the sidebar |

The meta tag defaults for content use the first value that is filled in:

| Tag | Value |
|---|---|
| Title | SEO title, otherwise the title |
| Description | SEO description, otherwise the summary of `field_body`, otherwise the body trimmed to 160 characters |
| Share image | SEO image, otherwise the image in `field_media`, cropped to 1200×630 (`seeds_social` image style) |

This works for every feature recipe because they all use the Seeds field names (`field_body`,
`field_media`), and Seeds image media keeps its file in `field_image`.

The feature recipes ship the SEO fields themselves, so they get them whether they are applied
from the UI or with Drush. For content types created later in the UI, the ECA model **Seeds: add
SEO fields to new content types** adds them automatically. It skips types without a page of their
own (FAQ, Partner, Slider, Newsletter issue); edit the list in the model's "Has its own page?"
condition at **Configuration > Workflow > ECA**.

## Seeds conventions in the feature recipes

- **Field names follow the field type**, not the purpose: `field_body` (text with summary),
  `field_formatted_long`, `field_plain_text`, `field_plain_long`, `field_media`, `field_media_1`,
  `field_media_unlimited`, `field_term`, `field_date`, `field_date_range`, `field_link`,
  `field_page_url`.
- **Files use the Seeds `file` media type** (`field_media_1`), images the Seeds `image` type.
- **Edit forms**: the title on top, then horizontal tabs: **Basic Information**, **Media** and,
  for types with their own page, **SEO**. Taxonomy terms use a select list, media items can be
  edited in place, and Promote/Sticky are hidden.

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

Recipes that ask for input (Newsletter) take it as options:

```bash
drush recipe ../recipes/newsletter_recipe --input=newsletter_recipe.from_address=news@example.com --input=newsletter_recipe.from_name="My site"
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
