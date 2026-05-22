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

### Interactive Map
- Visual job tracking - Every opportunity plotted on a map with color-coded pins:
  - Status colors: Potential (gray) -> Applied (blue) -> Interviewing (amber) -> Offer (green) -> Rejected (red)
  - Special pins: Current position (solid green), practice locations, and partner's options (purple)
- Popup details - Click any pin to see job summary with key stats, distances to destinations, and action buttons
- Responsive design - Works seamlessly on desktop and mobile
- Multiple map layers: people, trauma centers, airport proximity, universities, research labs, and pharmaceutical companies

### Comprehensive Job Tracking
Store everything about each opportunity:
- Basic info: Company/practice name, location, job title, contact details, posting URL, practice website
- Compensation: Base salary, estimated production revenue, production percentage, signing bonus
- Timeline: Application date, phone interview, in-person interviews (up to 2), offer date, deadline
- Status tracking: Potential -> Applied -> Interviewing -> Offer -> Rejected (or Current position)
- Interview notes: Track conversations and impressions
- Pros & cons: Capture what excites you and what concerns you

### Dual-Career Evaluation
Dedicated sections for both the primary candidate and partner:
- His section: Excitement rating, vibe tags, professional fit, relocation readiness notes
- Her situation: Overall fit rating, location feelings (1-year, 5-year, 10-year outlook), concerns, career opportunities
- Distance to family: Automatically calculated drive/flight times to up to 5 important people's locations

### OMFS-Specific Details
Tailored fields for oral & maxillofacial surgeons:
- Practice group linking (connect sister locations)
- DSO affiliation (Heartland Dental, MB2, Pacific Dental Services, etc.)
- Partnership track details (e.g., "2 years to buy-in")
- Call schedule (e.g., "1 in 5, no trauma")
- Case mix breakdown (wisdom teeth %, implants %, trauma %, orthognathic %, pathology %)
- Hospital affiliations and trauma level
- Malpractice coverage details
- Loan repayment / PSLF assistance

### Smart Filtering & Search
- Status filters: Toggle which job statuses to show
- Excitement levels: Filter by your rating or your partner's rating
- Decision score: Hide opportunities below a minimum score
- Search: Find jobs by company name, location, or any notes
- Sort options: By status, decision score, excitement, salary, date applied, practice name, location, or distance
- Real-time updates: Filters apply instantly

### Decision Tools

#### Compare Jobs
Select 2-4 opportunities and view them side-by-side in a detailed comparison table. Perfect for making the final call between top candidates.

#### Timeline View
See all your applications, interviews, and status changes in chronological order. Understand your job search momentum.

#### Decision Matrix
Weighted scoring system that auto-calculates a 0-100 score for each job based on:
- Base salary importance
- Compensation structure (production bonus potential)
- Benefits/perks
- Quality of life / location
- Career growth
- Team/culture fit
- Proximity to family
- And more

Customize weights (0-10 for each factor) based on what matters most to you. Recalculate on-the-fly.

#### City Snapshots
For each job location, see:
- Major city distances (estimated drive/flight times)
- Airports within reach
- Cost of living notes
- Weather and lifestyle summary

### Google Sheets Sync
One-time 5-minute setup connects your Job Map to a Google Sheet for:
- Automatic backup - Every job you add or edit syncs to the sheet
- Cross-device sync - Access your jobs from any device
- Team collaboration - Share the sheet with your partner for comments/collaboration
- Data portability - Export your data anytime

Includes a ready-to-use Google Apps Script that handles all the sync logic.

### Home Screen Install
- Install to home screen - "Add to Home Screen" on iOS or Android for quick access
- App-like view - Opens full-screen without browser chrome once added to your home screen
- Note: an internet connection is required (for the map tiles and Google Sheet sync); the app does not currently work fully offline

### Data Management
- Export backup - Download all your job data as a JSON file
- Import backup - Restore from a previous export
- Manage destinations - Set 3 important places to calculate distances for every job
- Family & friends - Add up to 5 people whose location matters; drive/flight times show on each job popup

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

## How to Use

### Adding a Job

1. Click + Add Job button
2. Choose the pin type:
   - His OMFS practice - Status-colored pins for his main opportunities
   - His CURRENT position - Green pin for his current role
   - My possible employer - Purple pin for your (partner's) opportunities
   - Sister location - Link to a parent job (e.g., multiple locations of the same practice)
3. Fill in the core details:
   - Practice/Employer: Company name (required)
   - Location: City, State/Country (required) — we auto-lookup coordinates
   - Status: Potential -> Applied -> Interviewing -> Offer -> Rejected
   - Compensation: Base salary and production details if applicable
4. Optional details:
   - Interview dates (phone, in-person #1, in-person #2)
   - Offer date and deadline
   - Contact info, job posting URL
   - Pros, cons, notes
5. OMFS-specific fields (collapse to see more):
   - Practice group, DSO affiliation, partnership track, case mix, etc.
6. His Impressions:
   - Location fit ratings (community, education, career growth, outdoor, culture, urban/rural, safety)
   - Vibe tags and interests
   - Relocation readiness (1-year, 5-year, 10-year outlook and escape velocity)
7. Couple's Context:
   - Her overall fit rating
   - Her career field for job search links
   - Her vibe tags and interests
   - Her location fit ratings and relocation readiness
   - Her notes and concerns
8. City & lifestyle details (cost of living, weather, etc.)
9. Save — the job appears on the map and in your list

### Filtering & Searching

- Search bar: Type company name, location, or keywords from notes to filter
- Status chips: Click to toggle which statuses are shown (e.g., hide "Rejected")
- His Star filter: Filter to jobs rated above a certain excitement level
- Her Star filter: Same for your (partner's) rating
- Score slider: Hide jobs below a minimum decision matrix score
- Sort select: Reorder the job list by status, score, excitement, salary, date, name, location, or distance

### Comparing Jobs

1. Click Compare button
2. Check 2-4 jobs you want to compare
3. Click View Comparison
4. See side-by-side details (compensation, interview timeline, decision scores, etc.)

### Using the Decision Matrix

1. Click Manage -> Decision matrix weights...
2. Adjust the importance of each factor (0 = ignore, 10 = critical):
   - Base salary, compensation structure, benefits, quality of life, career growth, team fit, family proximity, etc.
3. Click Save
4. Each job now has a 0-100 score shown in the sidebar and in details
5. Use "Score >= " filter to hide low-scoring opportunities
6. Click a job and then "Decision Matrix" to see the detailed breakdown

### Managing Family & Friends

1. Click Manage -> Family & friends...
2. Add up to 5 important people (name, location)
3. Save
4. Each job's popup now shows drive/flight time to each person

### Setting Destination Distances

1. Click Manage -> Plane destinations...
2. Customize 3 places (e.g., the cities you fly to most often)
3. Save
4. Every job shows straight-line distance + estimated flight time to each destination

### Timeline View

Click Timeline to see all jobs in chronological order, sorted by:
- Application dates
- Interview dates
- Status changes

Helps you visualize your job search progress and identify bottlenecks.

### Map Layers

Click Layers to toggle:
- People: Show your family/friends pins with drive/flight times
- Trauma centers: For residency or fellowship info
- Distance to nearest city: Heatmap showing isolation vs. urban areas
- Airports: Major US airports for travel considerations
- Universities: Research institutions nearby
- Labs & research centers: Academic and private research facilities
- Pharmaceutical companies: Comp chem and other pharma opportunities

### City Snapshots

Click any job location on the map to see a snapshot of that city:
- Major cities nearby and travel time
- Airports within reach
- Cost of living notes
- Weather/lifestyle summary

---

## Features by Job Status

### Potential (Gray)
Jobs you're considering but haven't applied to yet.
- Track why you're interested
- Note pros and cons
- Rate excitement level

### Applied (Blue)
You've submitted an application.
- Note application date
- Track when you expect to hear back
- Record recruiter/contact info

### Interviewing (Amber)
You're in conversations with the practice.
- Log phone interview date
- Schedule 1-2 in-person interviews
- Take notes on conversations

### Offer (Green)
You've received an offer!
- Log offer date and deadline
- Compare with other offers
- Use decision matrix to decide

### Rejected (Red)
Position isn't moving forward.
- Note when you heard back
- Record reason (helpful for reflection)
- Keep for historical context

### Current Position (Solid Green)
Your existing role (marked with solid green pin).

---

## Data Storage & Privacy

- Local storage: All your data is stored in your browser's local storage by default. It never leaves your device unless you explicitly enable Google Sheets sync.
- Google Sheets: If you opt into sync, your jobs are stored in a Google Sheet you control. We don't store data on any other server.
- Export/Import: Download your data as a JSON file anytime for local backup or to move between devices.
- No user accounts: You don't need to sign up for anything. This is purely client-side or synced to your own Google Sheet.

---

## Tips for Best Results

1. Be specific with locations: "Austin, TX" works better than "Austin" for accurate coordinates
2. Use "Remote" strategically: If a role is remote but based in a city, try "Remote + Austin, TX"
3. Update interview dates promptly: The timeline view and decision matrix improve with accurate dates
4. Rate honestly: Your excitement rating and decision matrix scores are most useful if they reflect your genuine feelings
5. For dual-career: Have your partner fill in the "Couple's Context" section—it surfaces important lifestyle and career concerns
6. Revisit weights: If your priorities change, update your decision matrix weights and recalculate
7. Use notes: The free-form notes field is powerful—capture gut feelings, overheard gossip, culture vibes, anything that matters
8. Export regularly: Backup your data as JSON monthly (or more often if actively job hunting)

---

## Troubleshooting

### Jobs aren't showing on the map
- Ensure the location is in format "City, State" or "City, Country"
- Check that you've saved the job (click Save button)
- If still not showing, the location lookup may have failed; try rephrasing (e.g., "San Diego, CA" instead of "San Diego")

### Google Sheets sync not working
- Verify the Web app URL is correct (should end in `/exec`)
- Check that you set access to "Anyone" during deployment
- Click Test Connection in the sync settings to debug
- If needed, re-deploy the Google Apps Script with a fresh deployment URL

### My data disappeared
- If you've been syncing, your data is safe in your Google Sheet — reconnect via Manage → Sync to reload it
- Check whether you're in a private/incognito window (locally stored data doesn't persist there)
- Note that clearing site data/cookies for the app's address removes locally stored jobs, so avoid that if you haven't synced
- Safari (iOS/macOS) auto-clears this kind of local storage after about 7 days without opening the app; syncing to a sheet protects against this
- Use Import backup if you have a previous JSON export

### Locations not found
- Try using full state abbreviations (e.g., "TX" not "Texas")
- For international cities: "City, Country" (e.g., "Toronto, Canada")
- Avoid extra punctuation or abbreviations in company names

---

## Advanced Features

### Sister Locations
If a practice has multiple office locations, create a "Sister location" pin and link it to the parent job. Sister locations appear on the map (slightly transparent) but don't show in the job list—clicking them opens the parent job's details.

### Practice Groups
Jobs with the same "Practice group" value (e.g., "Smith OMFS Group") are linked behind the scenes, helping you organize multi-location practices.

### Custom Vibe Tags
Add comma-separated tags to capture the gut feeling about a practice:
- His: "surgical-heavy, well-equipped, laid-back, busy"
- Her: "isolating, energizing, home-y, scary, lonely"

Useful for pattern-matching across opportunities.

### Cost of Living & Lifestyle Notes
Not just compensation—record local info:
- "Rent ~$2k, cheaper than SF"
- "Warm, outdoorsy, hiking nearby"
- "Excellent schools, family-friendly"

These show up in city snapshots for quick reference.

---

## File Structure

- index.html - The entire app (single-file HTML + embedded CSS + JavaScript)
- README.md - This file

No build process, no dependencies to install—just open index.html in a browser or deploy it statically.

---

## Browser Support

- Modern browsers: Chrome, Edge, Safari, Firefox (latest versions)
- Mobile: iOS Safari (via Home Screen), Android Chrome
- Connectivity: An internet connection is required for the map and for Google Sheet sync; full offline use is not currently supported

---

## Closing dialogs

Job Map is primarily mouse/touch driven. Close any open panel with the ✕ in its corner. (Dedicated keyboard shortcuts aren't implemented yet.)

---

## Privacy & Data

This app:
- Runs entirely in your browser (no server tracking you)
- Stores data locally by default (or in your own Google Sheet if enabled)
- Doesn't collect analytics or usage data
- Doesn't share your data with any third party

---

## Contributing & Customization

Since this is a single HTML file, you can:
- Customize colors: Edit CSS variables at the top of the style block (e.g., --accent: #4f46e5)
- Add fields: Modify the job form and adjust FIELDS array in the Apps Script
- Change scoring weights: Edit DEFAULT_WEIGHTS in the JavaScript
- Adjust marker styles: Customize .pin-marker, .status-* classes in CSS

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
- Leaflet.js - Interactive maps
- Google Apps Script - Sheets sync
- Vanilla JavaScript - No frameworks, pure browser APIs

---

## Version History

v1.0 - Initial release with core features: job tracking, interactive map, decision matrix, Google Sheets sync, PWA support, dual-career evaluation, OMFS-specific fields, and comprehensive filtering.

---

Happy job hunting!
