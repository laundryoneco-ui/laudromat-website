# Laundry One Co Website

The website for **Laundry One Co**, a self-service laundromat at 57 Dudley St, West Melbourne.

- **Live site:** https://laundryoneco.com.au
- **Built with:** plain HTML, [Tailwind CSS](https://v3.tailwindcss.com/) (v3) and images. There is no framework and no build step on the server.
- **Hosting:** Netlify. It deploys automatically when changes are pushed to the `main` branch.

---

## Project structure

```
index.html          Home page (mobile and desktop layouts, see below)
pricing.html        Pricing page
images/             Photos and graphics used on the site
css/tailwind.css    Generated Tailwind styles (do not edit by hand)
tailwind.config.js  Tailwind settings, used only to regenerate css/tailwind.css
```

Page-specific styles (fonts, the promo animation, the slideshow) are in the `<style>` block at the top of each HTML file.

The original design files (logos, brochures, banner, full-size photos) are **not** in this repository. Laundry One Co holds the originals.

---

## Making changes

1. Edit the HTML file. The simplest way is on GitHub: open the file, click the pencil icon, make the change, then "Commit changes" to `main`.
   Alternatively, clone the repo, edit locally, and `git push` to `main`.
2. Netlify publishes the change automatically, usually within a minute.
3. Check the live site on **both a phone and a computer** (see the next section for why).

To preview locally, open `index.html` in a browser. No server is needed.

### ⚠️ The home page has two copies of its content

`index.html` contains a **mobile layout** and a **desktop layout**. Each one is shown or hidden depending on screen size:

- `<!-- Mobile Layout -->`: the block with class `md:hidden`, shown on phones
- `<!-- Desktop Layout -->`: the block with class `hidden md:block`, shown on tablets and computers

**Any text change on the home page must be made in both layouts.** Otherwise phone and computer visitors will see different information.

### Where common content lives

| Content | Where to change it |
|---|---|
| Machine prices | `index.html`, "Our Machines" section, **in both layouts**, **and** `pricing.html` (3 places in total) |
| Opening hours | `index.html`, "Opening Hours", in both layouts |
| Address, phone, email | `index.html`, the "Visit Us" section and the footer, in both layouts. The address is also in the `pricing.html` footer |
| Promotion | `index.html`, the banner near the top and the "Oct – Nov Special" section, in both layouts (see below) |
| Online payment / sign-up link | `index.html`, the `start.bubblepayportal.com` links in the promo sections |
| Map | `index.html`, the Google Maps `<iframe>` and the `google.com/maps/place/...` links |
| Photos | Replace the file in `images/`, keeping the same file name, or update the `src="images/..."` references |

Search the file for the old text (for example `$11.00` or `6:00 AM`) to find every place it appears.

### Promotions

Every promo element has the class `js-promo`. A small script at the bottom of `index.html` removes them automatically after a set date:

```js
if (new Date() >= new Date('2026-12-01T00:00:00+11:00')) {
```

To run a new promotion, update the promo text in both layouts and change this date to the day **after** the promo ends. To remove a promo permanently, delete the `js-promo` elements.

---

## Styling (Tailwind CSS)

The site uses Tailwind utility classes (for example `text-2xl`, `px-6`, `md:hidden`). The CSS for these classes is pre-generated into `css/tailwind.css`, and the generated file **only includes classes that already appear in the HTML**.

- **Changing text, prices, links or images:** nothing extra is needed.
- **Adding or changing Tailwind classes:** regenerate the CSS before pushing, or the new classes will have no effect. This needs [Node.js](https://nodejs.org/):

  ```sh
  npx tailwindcss@3.4.17 -o css/tailwind.css --minify
  ```

  Then commit the updated `css/tailwind.css` together with the HTML change.

Keep the version at `3.4.17`. Tailwind v4 works differently and would change how the site looks.

---

## Hosting and domain

| | |
|---|---|
| **Code** | GitHub repository, owned by Laundry One Co |
| **Hosting** | Netlify: branch `main`, **no build command**, publish directory is the repository root |
| **Domain** | `laundryoneco.com.au`, registered with **Crazy Domains** in Laundry One Co's name |
| **DNS** | Managed by **Netlify DNS**. The domain's nameservers at Crazy Domains point to Netlify. Edit DNS records in Netlify, not Crazy Domains |
| **HTTPS** | Certificate issued and renewed automatically by Netlify |

The website, code repository, hosting and DNS were handed over to Laundry One Co on 19 October 2026.

**Keep the domain renewed.** Crazy Domains sends renewal notices to the registrant's email. If the domain expires, the website and any links to it stop working. Turning on auto-renew is recommended.
