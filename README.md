# Robinuo Learning Hub — Website

The marketing site for Robinuo Learning Hub, a robotics, coding, and AI school for kids in Bandar Puteri, Puchong. It's a small static website: two pages, one stylesheet, a sprinkle of vanilla JavaScript, and no build step to get in the way.

If you can open an HTML file in a browser, you can run this.

## What's in it

There are two pages:

- **`index.html`** — the landing page. Hero, a quick "highlights" strip, the program lineup, a photo gallery from the workshop, and a location section with a Google Maps embed.
- **`about.html`** — the story page. Who started it, what they care about, and the five things the classes try to build in students.

The main calls-to-action point straight at WhatsApp so a parent can message about a free trial without filling in a form.

## Tech stack

Nothing fancy, on purpose:

- Plain **HTML5** and **CSS3** (no framework, no preprocessor)
- A little **vanilla JS** for scroll reveals and the copyright year
- **Google Fonts** — Poppins for headings, Inter for body text
- **Font Awesome** (via CDN) for the icons
- A **Google Maps** iframe for the location

No bundler, no npm install, no package.json. The whole thing is files you can read top to bottom.

## Project structure

```
robinuoWebsite/
├── index.html          # Landing page
├── about.html          # Story / about page
├── style.css           # All styling + design tokens
├── script.js           # Smooth-scroll helper (see note below)
├── images/
│   ├── logo.png        # Transparent logo, used in the nav + footer
│   ├── favicon.png     # Logo on a white square, used for the browser tab
│   ├── hero.jpeg       # Hero photo + last gallery tile
│   ├── learning-1..5.jpeg   # Gallery photos
│   ├── scratch.svg     # Program card icon
│   └── arduino.svg     # Program card icon
└── README.md
```

A heads-up on `script.js`: it holds a smooth-scroll snippet, but neither page actually links it right now. Smooth scrolling already happens through `scroll-behavior: smooth` in the CSS, and the rest of the page behavior (scroll reveals, staggered cards, the live copyright year) lives in a small inline `<script>` at the bottom of each HTML file. So `script.js` is effectively a spare part. Wire it up with a `<script src="script.js">` tag if you'd rather keep that logic in its own file, or delete it.

## Running it locally

Pick whichever is least effort for you.

**Just open the file.** Double-click `index.html`. This works for most things, but the Google Maps embed and some browsers can be picky about `file://`, so a local server is a bit nicer.

**Python (already configured):**

```bash
python -m http.server 5500
```

Then visit `http://localhost:5500`. There's a `.claude/launch.json` set up to do exactly this.

**Node, if you prefer:**

```bash
npx serve
```

**VS Code:** the "Live Server" extension also does the job and gives you auto-reload.

## How the design is put together

If you're going to edit the styling, two things are worth knowing first.

**Design tokens live at the top of `style.css`.** Colors, the radius, shadows, and the two brand gradients are all CSS custom properties in the `:root` block. Change `--primary` (the blue) or `--accent` (the orange) there and it ripples through the whole site instead of you hunting for hex codes.

**The page background is a tiled SVG, not a gradient.** It's a faint blueprint-style grid with small circuit nodes at the intersections, encoded as a `data:` URI on the `body`. Because it repeats, it covers the page at any height and never cuts off at a section edge. The hero is transparent so the grid shows straight through.

**Motion is handled with an IntersectionObserver.** Elements tagged `.reveal` (plus cards, gallery items, and section headers) start slightly faded and slide up as they scroll into view. Grid children get a small staggered delay so they cascade in rather than popping all at once. It degrades gracefully: if `IntersectionObserver` isn't available, everything just shows immediately.

## Common edits

**Add or change a program.** Programs are the `.card` blocks inside `<section id="programs">` in `index.html`. Copy an existing card, swap the icon (`<i class="fas ...">` or an `<img>`), the title, the age tag, and the three bullet points.

**Update contact details.** Phone number, email, and address show up in the footer (both pages) and in the location section of `index.html`. The WhatsApp links also encode the phone number in the `href`, so update those too if the number changes.

**Swap the location pin.** Replace the Maps `iframe` `src` and the "Get Directions" link in the location section with your own embed/share URLs from Google Maps.

**Change the photos.** Drop new images into `images/` and update the `src` and `alt` attributes in the gallery and hero.

**Replace the logo or favicon.** `images/logo.png` is the transparent version used in the nav and footer. `images/favicon.png` is the same logo flattened onto a white square so it reads clearly on a dark browser tab. If you regenerate the logo, regenerate the favicon to match.

## A note on caching

The stylesheet is linked as `style.css?v=2`. That `?v=` bit is a cache-buster: browsers hang onto CSS aggressively, and bumping the number forces a fresh download after you ship a change. If you edit `style.css` and people report seeing the old look, bump it to `?v=3` (in both HTML files) and they'll pull the new version.

## Deploying

It's static, so almost anything works: GitHub Pages, Netlify, Cloudflare Pages, Vercel, or any plain web host where you can drop the files.

For GitHub Pages, push to the repo and turn on Pages for the `main` branch in the repo settings. Since everything is relative paths, there's nothing to configure.

## Contact

- **Robinuo Learning Hub** — 19-2, Jalan Puteri 1/4, Puchong 47100, Selangor
- Phone / WhatsApp: +60 11-3312-6359
- Email: admin@robinuo.com
- [Facebook](https://www.facebook.com/p/Robinuo-Learning-Hub-61576348565523/) · [Instagram](https://www.instagram.com/robinuokids/) · [TikTok](https://www.tiktok.com/@robinuokids)
