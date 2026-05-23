# Job Map

A personalized, interactive web application for tracking job applications, evaluating career opportunities geographically, and making informed decisions with location and lifestyle data—designed with dual-career couples in mind.

## Overview

Job Map transforms the job search process from a spreadsheet into an interactive experience. Whether you're tracking surgical practices across the country, comparing compensation packages, or weighing geography, family proximity, and lifestyle, this tool centralizes everything in one place.

### Built for:
- OMFS professionals seeking practice opportunities (heavily customized for oral & maxillofacial surgery)
- Dual-career couples evaluating opportunities together with different priorities
- Location-sensitive decisions where geography, proximity to family, and lifestyle matter as much as salary
- Complex compensation structures (base salary + production bonus models)

---

## Key Features

- **Interactive Map** — Every opportunity plotted with status-colored pins, popups, and multiple map layers (people, trauma centers, airports, universities, research labs, pharma).
- **Comprehensive Job Tracking** — Compensation, timeline, status, interview notes, pros & cons.
- **Dual-Career Evaluation** — Dedicated sections for both partners, plus drive/flight times to family.
- **OMFS-Specific Details** — Practice group, DSO affiliation, partnership track, call schedule, case mix, hospital affiliations, malpractice, PSLF.
- **Smart Filtering & Search** — Status, excitement, decision score, free-text search, sorting.
- **Decision Tools** — Side-by-side compare (2–4 jobs), chronological timeline, weighted decision matrix (0–100 score), city snapshots.
- **Google Sheets Sync** — One-time setup for automatic backup, cross-device sync, and collaboration.
- **Home Screen Install** — Add to Home Screen on iOS/Android for app-like access (internet required).
- **Data Management** — JSON export/import, destination distances, family & friends locations.

See the [User Guide](USER_GUIDE.md) for full details on each feature and how to use them.

---

## Getting Started

### Trying the live demo (no setup)

The publicly hosted version of Job Map loads a shared **demo sheet** filled with fictional sample data, so you can explore every feature — pins, filters, the decision matrix, comparisons, the map layers — without any setup. The demo sheet is public and may be reset at any time, so don't store anything real in it. To use Job Map for your own search, host your own copy and connect your own Google Sheet, as described below.

### Installation — host your own copy

Job Map is a single static HTML file plus a Google Apps Script backend. Standing up your own instance takes about ten minutes and keeps all of your data in a Google Sheet that **you** own.

**1. Get the code**

- Fork this repository on GitHub (click **Fork** at the top right), or download `index.html` and add it to a new repository of your own.

**2. Publish it with GitHub Pages**

- This repo includes a GitHub Actions workflow (`.github/workflows/jekyll-gh-pages.yml`) that builds and deploys the site automatically.
- In your fork, go to **Settings → Pages**, and under "Build and deployment" set **Source** to **GitHub Actions**.
- Push to the `main` branch (or open the **Actions** tab and run the workflow manually). GitHub will publish your site at `https://<your-username>.github.io/<repo-name>/`.

**3. Set up your own Google Sheet backend**

- Create a new Google Sheet (visit sheets.new) and name it whatever you like.
- In that sheet, open **Extensions → Apps Script**.
- In your deployed Job Map, open **Manage → Sync to Google Sheet…** and click **Copy script**. Paste it into the Apps Script editor and save.
- Click **Deploy → New deployment → Web app**, set **Execute as: Me** and **Who has access: Anyone**, then **Deploy** and authorize. Copy the Web app URL (it ends in `/exec`).

**4. Connect your sheet**

- Back in your deployed app, open **Manage → Sync to Google Sheet…**, paste your `/exec` URL, click **Test Connection** to verify, then **Save & Sync**.
- From then on, every change syncs automatically to *your* sheet, and your data lives only there and in your own browser.

> **Connect your own sheet — this matters.** The code ships with a default URL that points only to the public demo sheet, never to anyone else's real data. Always set up and connect your own Google Sheet using the steps above so your entries go to a sheet you control. Connecting a sheet only affects your own browser and your own sheet; it cannot reach or overwrite anyone else's data.

> **Updating the code later:** to change the published app without minting a new backend URL, edit your existing Apps Script deployment to a new version (**Manage deployments → Edit**) rather than creating a brand-new deployment. Creating a new deployment generates a different `/exec` URL and you'd have to reconnect.

---

## Documentation

- [User Guide](USER_GUIDE.md) — How to add jobs, filter, compare, use the decision matrix, troubleshoot, and more.

---

## Data Storage & Privacy

- **Local storage:** All your data is stored in your browser's local storage by default. It never leaves your device unless you explicitly enable Google Sheets sync.
- **Google Sheets:** If you opt into sync, your jobs are stored in a Google Sheet you control. We don't store data on any other server.
- **Export/Import:** Download your data as a JSON file anytime for local backup or to move between devices.
- **No user accounts:** You don't need to sign up for anything. This is purely client-side or synced to your own Google Sheet.

This app runs entirely in your browser (no server tracking you), doesn't collect analytics or usage data, and doesn't share your data with any third party.

---

## File Structure

- `index.html` — The entire app (single-file HTML + embedded CSS + JavaScript)
- `README.md` — This file
- `USER_GUIDE.md` — Detailed usage instructions

No build process, no dependencies to install—just open `index.html` in a browser or deploy it statically.

---

## Browser Support

- Modern browsers: Chrome, Edge, Safari, Firefox (latest versions)
- Mobile: iOS Safari (via Home Screen), Android Chrome
- Connectivity: An internet connection is required for the map and for Google Sheet sync; full offline use is not currently supported

---

## Contributing & Customization

Since this is a single HTML file, you can:
- Customize colors: Edit CSS variables at the top of the style block (e.g., `--accent: #4f46e5`)
- Add fields: Modify the job form and adjust `FIELDS` array in the Apps Script
- Change scoring weights: Edit `DEFAULT_WEIGHTS` in the JavaScript
- Adjust marker styles: Customize `.pin-marker`, `.status-*` classes in CSS

For significant changes, consider maintaining a fork.

---

## Feedback & Issues

Found a bug or want a feature? Create an issue in the repository with:
- What you were trying to do
- What happened instead
- Browser and OS you're using
- Steps to reproduce (if applicable)

---

## License

Add license here if applicable

---

## Credits

Built with:
- Leaflet.js — Interactive maps
- Google Apps Script — Sheets sync
- Vanilla JavaScript — No frameworks, pure browser APIs

---

## Version History

v1.0 — Initial release with core features: job tracking, interactive map, decision matrix, Google Sheets sync, PWA support, dual-career evaluation, OMFS-specific fields, and comprehensive filtering.

---

Happy job hunting!

<img width="1470" height="956" alt="Screenshot 2026-05-21 at 9 10 15 PM" src="https://github.com/user-attachments/assets/93446211-f430-4628-9fc0-42a9bb3705e7" /><img width="1470" height="956" alt="Screenshot 2026-05-21 at 9 10 34 PM" src="https://github.com/user-attachments/assets/a0111246-f484-4918-b089-f45a75fab988" /><img width="1470" height="956" alt="Screenshot 2026-05-21 at 9 10 57 PM" src="https://github.com/user-attachments/assets/f92213c0-5380-4920-ae6a-aafdc86fd8ae" />
