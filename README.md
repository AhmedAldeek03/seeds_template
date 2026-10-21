# Seeds template

A complete Seeds site in one step: **Seeds base** plus all our feature recipes.

| Recipe | Adds |
|---|---|
| Seeds base | The Seeds foundation (replaces the Seeds install profile) |
| Media center + Seeds cards | News and Event types, home and compiled blocks, Seeds UI cards |
| Local Reach | Key figures, progress bars, ring charts, country flags, institution summary (Canvas) |
| Slider | Slide type and Slick carousel |
| FAQ | FAQ type with categories, accordion block |
| Gallery | Photo and video albums |
| Partners | Partner and client logos |
| Team | Staff and board members |
| Publications | Annual reports and studies with files |
| Contact form | "Contact us" webform at `/contact-us` |
| Newsletter | Simplenews setup |

Seeds base is applied first, so every feature builds on Seeds' own media types, editor and toolbar.

## Install a new site

```bash
drush site:install ../recipes/seeds_template --account-name=admin --site-name="My site"
```

Each feature recipe can also be applied on its own to an existing site, for example
`drush recipe ../recipes/faq_recipe`.

## Requirements

All recipes must sit in the same `recipes/` folder (Composer puts them there), because recipes
include each other by name. The project also needs the two Seeds module patches listed in the
Seeds base README.
