
# Gemau Ystoria Website

This repository contains the source code for the bilingual website of **Gemau Ystoria**, a Welsh-first tabletop roleplaying game publisher.

The site is built with [Hugo](https://gohugo.io/) using the [Ananke theme](https://github.com/theNewDynamic/gohugo-theme-ananke), and supports both Welsh (`cy`) and English (`en`) languages with a language switcher and translated interface.

---

## 🌐 Live Site

**[www.gemauystoria.cymru](https://www.gemauystoria.cymru)**

---

## 📁 Structure

- `content/cy/`: Welsh-language pages
- `content/en/`: English-language pages
- `layouts/`: Custom layout overrides
- `i18n/cy.toml`: Welsh interface translations
- `.github/workflows/deploy.yml`: GitHub Actions workflow for publishing

---

## 🚀 Deployment

This site is automatically deployed using **GitHub Actions** to **GitHub Pages**.

### Prerequisites

- Hugo installed locally (`hugo version`)
- GitHub repository configured with:
  - `gh-pages` branch as the Pages source
  - Custom domain set to `www.gemauystoria.cymru`

### Build and Push

1. Make changes locally
2. Run Hugo to verify:
   ```bash
   hugo server
   ```
3. Commit and push to `main`:
   ```bash
   git add .
   git commit -m "Update content"
   git push origin main
   ```

### GitHub Actions

- The workflow in `.github/workflows/deploy.yml` builds the site on push to `main` and deploys to `gh-pages`.

---

## 🌍 Multilingual Setup

### `hugo.toml` example:

```toml
defaultContentLanguage = "cy"
defaultContentLanguageInSubdir = true

[languages]

[languages.cy]
languageName = "Cymraeg"
languageCode = "cy"
weight = 1
contentDir = "content/cy"
title = "Gemau Ystoria"

[languages.en]
languageName = "English"
languageCode = "en"
weight = 2
contentDir = "content/en"
title = "Gemau Ystoria"
```

### Linking Translations

Each page pair uses:

- A shared `translationKey` in front matter
- A matching `url` to unify navigation

---

## 📄 License

This repository contains content authored by Gemau Ystoria and contributors. See individual files for licensing where applicable.


---

## ➕ Adding Translated Pages

To add a new page in both Welsh and English:

### 1. Create the Files

Use parallel file names for consistency:

```bash
touch content/cy/eiddo.md
touch content/en/property.md
```

### 2. Add Front Matter with Shared `translationKey`

Example `content/cy/eiddo.md`:

```markdown
---
title: "Eiddo"
translationKey: "property"
url: "/property/"
---
Mae hwn yn dudalen sampl yn Gymraeg.
```

Example `content/en/property.md`:

```markdown
---
title: "Property"
translationKey: "property"
url: "/property/"
---
This is a sample page in English.
```

### 3. Verify

Run:

```bash
hugo server
```

Then visit:

- `http://localhost:1313/cy/property/`
- `http://localhost:1313/en/property/`

The language switcher will appear if `.Translations` is correctly linked by `translationKey`.

---

