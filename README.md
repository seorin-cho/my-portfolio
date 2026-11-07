# Seorin's Portfolio

Personal portfolio built with Hugo Profile and deployed to GitHub Pages.

- Website: https://seorin-cho.github.io/my-portfolio/
- Repository: https://github.com/seorin-cho/my-portfolio

## Build environment

The deployment workflow installs the following tools:

| Tool | Version |
|---|---|
| Runner | ubuntu-latest |
| Python | 3.12 |
| Node.js | 24 |
| Go | 1.27.1 |
| Hugo Extended | 0.143.0 |
| Dart Sass | 1.105.0 |
| Preparation script | 3.1 |

Python, Node.js, and Go are installed by the setup actions.
Hugo Extended and Dart Sass are downloaded and extracted
in the Install Hugo and Sass step.

Workflow: [.github/workflows/hugo-pages.yml](.github/workflows/hugo-pages.yml)

## Reproduce the build with GitHub Actions

This procedure requires permission to run workflows in the repository.

1. Open the repository on GitHub.
2. Select Actions, then Deploy Hugo to GitHub Pages.
3. Select Run workflow and choose main.
4. Start the workflow.
5. Confirm that build and deploy succeed.
6. Open the website and check the result.

This workflow builds and deploys the selected version.
A push to main also triggers it automatically.

For a separate repository, enable Actions and select:
Settings → Pages → Build and deployment → Source → GitHub Actions.

## Build commands and files

After installing the tools above, the workflow runs these commands
from the repository root on the Linux runner:

```bash
python .github/pages_build.py --dependencies
python .github/pages_build.py --build
```

Python alone is not sufficient to run the build.
The workflow supplies SITE_BASE_URL using actions/configure-pages.

- Main configuration: site/hugo.yaml
- Additional deployment configuration: site/pages.json
- Build configuration selection: .github-pages.json
- Page content: site/content/
- Images and static files: site/static/
- Theme: site/themes/template/
- Build output: public/

## Update and redeploy

Edit site/hugo.yaml for the homepage, menus, and project descriptions.
Edit site/content/ for page content.
Add images and static files under site/static/.

From the repository root, review the changes:

```powershell
git status
git diff
```

For a homepage configuration change:

```powershell
git add site/hugo.yaml
git commit -m "Update homepage content"
git push origin main
```

Stage the actual changed paths if editing other files.

After pushing:

1. Open Actions and select the run for the new commit.
2. Confirm that build and deploy succeed.
3. Open https://seorin-cho.github.io/my-portfolio/
4. Refresh and check that the intended changes appear.

## Verified behavior

### Invalid URL recovery

Test URL:
https://seorin-cho.github.io/my-portfolio/not-found-check/

Checks performed:
- An unknown URL displays the Page not found screen.
- The screen includes an explanation and a Return to portfolio link.
- Clicking the link returns to /my-portfolio/.
- The link can be selected with Tab and activated with Enter.

Result: Passed.
## Site content map

| Content | Public location | Source setting |
|---|---|---|
| Name and short introduction | Homepage | params.hero |
| Interests and reasons | /#about | params.about.content |
| Learning goals and next actions | /#about | params.about.content |
| Tools and practical use | /#about | params.about.content and skills |
| Activity period and status | /#projects | params.projects.items |
| Purpose and personal contribution | /#projects | params.projects.items |
| Process and choice of tools | /#projects | params.projects.items |
| Results and source repository | /#projects | params.projects.items |
| Learning outcomes and next improvements | /#projects | params.projects.items |

All settings above are in site/hugo.yaml.
The activity menu is labelled My Activities.

## Theme attribution

### Preserved license notices

- LICENSE: MIT license notice for Hugo Profile.
- site/themes/template/LICENSE: MIT, copyright GURU SABARISH.
- site/LICENSE: Apache License 2.0 notice supplied with the sample site.
- exampleSite/LICENSE: Apache License 2.0 notice supplied with the sample site.

These notices are retained in their original locations.

## Content and asset sources

- Theme: Hugo Profile by gurusabarish.
  Source: https://github.com/gurusabarish/hugo-profile
  The original MIT license and copyright notice are preserved.

### Profile images

The homepage and About Me sections use text-only introductions.
The sample avatars hero.svg and me.png are not displayed.

Their files remain in site/static/images/ as unused theme assets.
They were included in the downloaded Hugo Profile theme and were
not created by me.

Theme source: https://github.com/gurusabarish/hugo-profile
Original license notices are preserved.
Separate image-specific usage terms have not been confirmed.

- Personal introduction: Adapted from AI-assisted drafts
  and reviewed and edited by me.

- Configuration changes: Made by me with AI guidance.

Theme: Hugo Profile by gurusabarish.
Source: https://github.com/gurusabarish/hugo-profile
License: MIT. See LICENSE.

The original theme documentation is retained below.
Its generic setup instructions are separate from this project's
prepared site/ structure and GitHub Pages workflow.

---

## Original theme documentation

# Hugo Profile

[![Twitter](https://img.shields.io/twitter/url?label=Tweet&style=social&url=https%3A%2F%2Fgithub.com%2Fgurusabarish%2Fhugo-profile)](https://twitter.com/intent/tweet?text=Wow:&url=https%3A%2F%2Fgithub.com%2Fgurusabarish%2Fhugo-profile) [![GitHub forks](https://img.shields.io/github/forks/gurusabarish/hugo-profile?style=plastic)](https://github.com/gurusabarish/hugo-profile/network) [![GitHub stars](https://img.shields.io/github/stars/gurusabarish/hugo-profile?style=plastic)](https://github.com/gurusabarish/hugo-profile/stargazers)

[![Netlify Status](https://api.netlify.com/api/v1/badges/5c1dcb34-cada-4c80-82b7-cfdbdbd7c774/deploy-status)](https://app.netlify.com/sites/hugo-profile/deploys)
![Latest Release](https://img.shields.io/github/v/release/gurusabarish/hugo-profile?include_prereleases)
![Last Commit](https://img.shields.io/github/last-commit/gurusabarish/hugo-profile)
![Open Issues](https://img.shields.io/github/issues/gurusabarish/hugo-profile?color=important)
![Open Pull Requests](https://img.shields.io/github/issues-pr/gurusabarish/hugo-profile?color=yellowgreen)
![License](https://img.shields.io/github/license/gurusabarish/hugo-profile)

**Hugo Profile:** a high-performance, mobile-first Hugo theme for personal portfolios and blogs.

- Example Site: [https://hugo-profile.netlify.app](https://hugo-profile.netlify.app)
- Wiki Page: [https://github.com/gurusabarish/hugo-profile/wiki](https://github.com/gurusabarish/hugo-profile/wiki)
- Full documentation (versioned in this repo): [wiki/Home.md](wiki/Home.md)

**Features:**
- Fully Responsive
- Minimalist Design
- SEO Friendly
- Internationalization (i18n) Support
- [Light/Dark/Auto Theme Color Configuration](https://github.com/gurusabarish/hugo-profile/wiki/Color-Customization)
- Categories and Tags Support
- Analytics Support ([Google Analytics](https://gohugo.io/templates/internal/#google-analytics))
- Comment Support ([Disqus](https://gohugo.io/content-management/comments/))
- Contact Form Integration ([FormSpree](https://formspree.io/))
- Built with Bootstrap and Font Awesome


## Requirements

- **Hugo version 0.87.0 or higher**   
To check your installed version, run:   
  ```bash
  hugo version
  ```
  If Hugo is not installed, follow the [official installation guide](https://gohugo.io/installation/) for installation.


## Quick Start 

1. Create a new Hugo site:  

    ```bash
    hugo new site my-site --format="yaml"
    ```  
    This uses a `hugo.yaml` configuration file instead of the default TOML format. 

2. Add a theme.  

    Option A: Clone this repository inside your themes folder.  
    This allows you to make lots of custom changes.
    ```bash
    cd my-site/themes
    git clone https://github.com/gurusabarish/hugo-profile.git
    ```

    Option B: Add as a Git submodule.  
    This allows you to get automatic or structured updates from the original repository.

    ```bash
    cd my-site
    git init
    git submodule add https://github.com/gurusabarish/hugo-profile.git themes/hugo-profile
    ```    

3. Copy the example configuration file to your site root:
    ```bash
    cp -f themes/hugo-profile/exampleSite/hugo.yaml ./hugo.yaml
    ```

4. Start the Hugo development server:
    ```bash
    hugo server
    ```
5. Recommended: Copy example content and assets.

    When you first run `hugo server`, the site may look incomplete — images may be missing and the Blog or Gallery sections might not appear.  

    This is because their content currently resides in `themes/hugo-profile/exampleSite/`, whereas Hugo expects them in the root-level `static/` (for images) and `content/` (for pages) directories.

    To have a complete view of the example site, run:  

    ```bash
    rsync -av themes/hugo-profile/exampleSite/static/ ./static/
    rsync -av themes/hugo-profile/exampleSite/content/ ./content/
    ```

    You can customize or replace this content to match your own site.


## Content Management

You can now start customizing your site.

To change the site title or homepage content, edit the `hugo.yaml` file in the root directory. This file also controls settings for showing or hiding sections of the site (e.g., About, Education).

To create a new page, for example, in the Blog section, run:

```bash
hugo new content content/blogs/my-post.md
```

This creates a new file in the `content/blogs/` folder with front matter that includes metadata like the date.

Here are some useful resources for your reference:

* [Hugo's Quick Start Guide](https://gohugo.io/getting-started/quick-start/) – About how to create a site, add content, and publish the site.

* [Hugo Content Organization – Giraffe Academy](https://www.mikedane.com/static-site-generators/hugo/content-organization/)

* [Wiki Page](https://github.com/gurusabarish/hugo-profile/wiki) – Tips specific to this theme.


## Internationalization (i18n)

This theme supports multiple languages out of the box. Hugo Profile includes built-in translations for English, Spanish, and French, and you can easily add your own languages.

### Setting Up Multiple Languages

To enable multilingual support, add the following to your `hugo.yaml`:

```yaml
defaultContentLanguage: "en"
defaultContentLanguageInSubdir: false

languages:
  en:
    languageName: "English"
    weight: 1
  es:
    languageName: "Español"
    weight: 2
  fr:
    languageName: "Français"
    weight: 3
```

### How It Works

1. **Translation Files**: The theme includes translation files in the `i18n/` directory:
   - `en.toml` - English translations
   - `es.toml` - Spanish translations
   - `fr.toml` - French translations

2. **Language Switcher**: When you enable multiple languages, a language switcher dropdown automatically appears in the navigation bar, allowing visitors to switch between languages.

3. **Backward Compatibility**: All existing sites continue to work without any changes. The theme automatically falls back to English or your configured language if no multilingual setup is provided.

### Adding a New Language

To add support for a new language (e.g., German):

1. Create a new translation file `i18n/de.toml` in your site root or in the theme:
   ```toml
   [nav_about]
   other = "Über uns"
   
   [nav_experience]
   other = "Erfahrung"
   
   # Add all other translations...
   ```

2. Add the language to your `hugo.yaml`:
   ```yaml
   languages:
     de:
       languageName: "Deutsch"
       weight: 4
   ```

3. (Optional) Create language-specific content in `content/de/` directory.

### Customizing Translations

You can override any translation by adding it to your site's `params.terms` section in `hugo.yaml`:

```yaml
params:
  terms:
    read: "Custom Read Text"
    pageNotFound: "Custom 404 Message"
```

For more information about Hugo's multilingual features, see the [Hugo Multilingual Documentation](https://gohugo.io/content-management/multilingual/).


## Deployment

If you do not require extensive customization, the easiest way to deploy is:
1. Click the **Use this template** button to create your own repository.
2. Connect the repository to **Netlify**.

Whenever you make changes to the files inside the `exampleSite` folder, Netlify will automatically detect and deploy your changes. 

---


If you followed the steps in the [Quick Start](#quick-start) section above, you can still deploy your site to Netlify, but you'll need a few additional configurations.   

See the **[Host on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)** guide for further information.

---

For manual deployment, run `hugo` to generate the final, ready-to-deploy static site in the `public/` folder, which you can upload to any hosting platform.

It is recommended to delete the `public/` folder before each build to ensure it only contains the latest output:

```bash
rm -rf public/ && hugo
```


## Trouble-Shooting

```
ERROR error calling resources.GetRemote: Get "https://publish.twitter.com/oembed?dnt=false&url=https%3A%2F%2Ftwitter.com%2FGoHugoIO%2Fstatus%2F1315233626070503424": net/http: TLS handshake timeout
Built in 10266 ms
Error: error building site: logged 1 error(s)
```
The TLS handshake timeout error can happen due to network issues. If this error persists, you can delete the shortcode example `{{< tweet user="GoHugoIO" id="1315233626070503424" >}}` in the "content/blogs/rich-content.md" file.


## Issues

If you have a question, please [open an issue](https://github.com/gurusabarish/hugo-profile/issues) for help and to help those who come after you. The more information you can provide, the better!

## Contributing

Contributions, issues, and feature requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

## License

Licensed under [MIT](LICENSE)

## 🤝 Support

Give a ⭐️ or buy me a ~`coffee`~ tea if you like this project!

<a href="https://www.buymeacoffee.com/gurusabarish" target="_blank" rel="noopener"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="40" width="145" alt="Buy Me A Coffee"></a>
