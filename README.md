# LinkedIn 500 Tracker

**Build meaningful professional connections, one day at a time.**

A free, open-source networking CRM for students and early-career professionals. Plan outreach, track conversations, manage follow-ups, and build relationships that can lead to career opportunities — all from one lightweight dashboard.

- 🎯 **Track your goal:** Monitor progress toward 500+ connections.
- 🤝 **Manage relationships:** Organise contacts, statuses, and follow-ups.
- ✉️ **Personalise outreach:** Use professional message templates tailored to your goals.
- 📊 **Measure progress:** Understand acceptance rates, response patterns, and daily consistency.
- 🔒 **Keep control of your data:** Everything stays in your browser, with no account or backend required.

**[🚀 Try the live demo](https://linkedin-networking-engine.vercel.app/)** · **[⭐ Star on GitHub](https://github.com/santhoshsharrma/linkedin-networking-engine)** · **[🤝 Contribute](https://github.com/santhoshsharrma/linkedin-networking-engine/issues)**

> Not affiliated with or endorsed by LinkedIn. This tool does not scrape profiles, connect to LinkedIn, or automate LinkedIn actions. All outreach and tracking are performed manually.

Built with HTML, CSS, and vanilla JavaScript. Free and open source under the MIT License.

---

## Table of contents

- [Why this exists](#why-this-exists)
- [Features](#features)
- [How it works](#how-it-works)
- [Getting started](#getting-started)
- [Usage guide](#usage-guide)
- [Customisation](#customisation)
- [Data and privacy](#data-and-privacy)
- [Data model](#data-model)
- [Project structure](#project-structure)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## Why this exists

Most referrals come from relationships, and relationships come from consistent, thoughtful outreach. Spreadsheets get abandoned, and it is easy to lose track of who accepted, who replied, and who needs a follow-up.

This tracker gives students and early-career professionals one place to:

- Send a steady number of requests each day without overdoing it.
- See what to do next for every person, so no follow-up is missed.
- Learn which kinds of people accept and reply, then focus on them.
- Reuse professional message templates instead of writing from scratch.

## Features

**Tracking**
- Log each request with name, LinkedIn ID (a full profile URL is accepted and the ID is extracted), category, and date sent.
- Status pipeline: Sent, Accepted, Followed up, Replied, Referral stage, No response.
- Automatic response label (Replied, Accepted with no reply yet, Pending, No response after 10+ days).
- A "what to do next" suggestion for every row, with a one-click copy of the matching message.
- Search plus category and status filters.

**Goal and consistency**
- Progress bar toward a configurable connection goal (default 500).
- Daily request counter and target (default 15) with a streak for days the target is met.
- Estimated requests and days remaining, based on your real accept rate.
- Option to include connections you already had before starting.

**Categories**
- Recruiters, Backend engineers, Alumni, Hiring managers, Peers and students, Mentors and creators.
- Per-category sent, accepted, replied, and accept rate, so you can see which groups respond best.

**Messages**
- Professional, warm connection notes for each category, kept under LinkedIn's 200-character note limit.
- Follow-up, soft nudge, call request, referral ask, and thank-you templates.
- A reply playbook that explains what to do in common situations.
- Type a first name once and every template fills in. Copy with one click.
- First-run profile setup (your name, course, target field, graduation year) personalises every message automatically. It can be edited at any time.
- A universal connection note that works for any category.

**Data**
- Export to CSV.
- Backup and restore as JSON.
- Light and dark theme that follows your system setting, with a manual toggle.
- Responsive layout that works on mobile.
- "Load sample data" button to try the app instantly, with a one-click removal.
- Link preview tags (Open Graph) so shared links look good on LinkedIn and messaging apps.

## How it works

1. **Log** every request you send, with its category.
2. **Update the status** when something changes. The response label and next action update automatically.
3. **Follow the next action.** For example, send a follow-up within 24 hours of an accept, nudge once after 6 to 7 days, and ask for a referral only after real rapport.
4. **Review the numbers** to see where your time is paying off.

Key calculations:

| Metric | Definition |
| --- | --- |
| Connections | Starting connections plus every request that is Accepted, Followed up, Replied, or Referral stage |
| Accept rate | Accepted requests divided by total requests sent |
| Estimated requests left | Remaining connections divided by accept rate (35% is assumed until 10 requests are logged) |
| Estimated days left | Estimated requests left divided by your daily target |
| Streak | Consecutive days with at least the daily target sent, counted back from today or yesterday |

## Getting started

The app is a single static HTML file with no build step and no dependencies to install.

### Run locally

```bash
git clone https://github.com/santhoshsharrma/linkedin-networking-engine.git
cd linkedin-networking-engine
# open linkedin-tracker.html in your browser, or serve it:
npx serve .
```

### Deploy

**Vercel**
1. Push the repository to GitHub.
2. Import it in Vercel. Framework preset: **Other**. No build command is needed.

**GitHub Pages**
1. Open the repository **Settings**, then **Pages**.
2. Choose the main branch and the root folder, then save.

## Usage guide

**Daily routine (about 20 minutes)**
- Send 10 to 15 requests across different categories and log them.
- Send follow-ups to everyone who accepted yesterday.
- Leave 3 thoughtful comments on posts from people you contacted.
- Nudge once, only for people marked "Followed up" for 6 or more days, then stop.
- Update statuses so the numbers stay honest.

**Tips for better results**
- Personalise connection notes with one specific detail, such as their company or a post.
- Free LinkedIn accounts have a limited number of personalised notes per month. Use them on recruiters, hiring managers, and alumni.
- Ask for advice first and a referral later.
- Back up your data weekly.

## Customisation

Everything is in `linkedin-tracker.html`. The main configuration objects are near the top of the script:

| Object | Purpose |
| --- | --- |
| `CATS` | Category keys and display names |
| `ST` | Status keys and display names |
| `T.note` | Connection note per category |
| `T.seq` | Follow-up, nudge, call, referral, and thank-you messages |
| `T.play` | Reply playbook entries |
| `S` defaults | Goal (500), daily target (15), starting connections (0) |

Templates use placeholders: `{n}` (the recipient's first name), `{me}` (your name), `{study}` (your course), `{role}` (your target field), and `{yr}` (your graduation year). The last four come from the profile you fill in on first use, so nobody needs to edit code to personalise their messages.

## Data and privacy

- All data is stored in your browser using `localStorage` under the key `li500.v1`.
- There is no server, account, analytics, or tracking. Nothing you enter leaves your device.
- Data is per browser and per device. Clearing site data, using private browsing, or switching browsers will remove it, so use **Backup JSON** regularly.
- Two deployments of the app (for example a local copy and a hosted copy) do not share data. Use Backup and Restore to move entries between them.

## Data model

Stored as one JSON object:

```json
{
  "goal": 500,
  "daily": 15,
  "start": 0,
  "profile": {
    "name": "Jane Doe",
    "study": "Computer Science",
    "role": "backend engineering",
    "year": 2027,
    "done": true
  },
  "people": [
    {
      "id": "1729254000000ab12",
      "name": "Jane Doe",
      "handle": "jane-doe-123",
      "cat": "rec",
      "date": "2026-10-18",
      "status": "sent"
    }
  ]
}
```

- `cat` is a key from `CATS` and `status` is a key from `ST`.
- `date` is the local date the request was sent, in `YYYY-MM-DD` format.

## Project structure

```
.
├── linkedin-tracker.html     # markup, styles, and logic in one file
├── og-image.png   # link preview image (1200x630)
├── LICENSE
└── README.md
```

Built with HTML, CSS, and vanilla JavaScript. The only external resource is Google Fonts (Schibsted Grotesk), with system fonts as a fallback.

## Roadmap

**Near term**
- [ ] Company column and filter, to track outreach per target company
- [ ] Editable templates inside the app (profile fields are already supported)
- [ ] Notes field per contact
- [ ] Follow-up due list on the home screen, such as "accepted yesterday, no message sent"
- [ ] CSV import
- [ ] Bulk add for faster daily logging

**Referral pipeline**
- [ ] Track target roles: company, role, job ID, link, and application status
- [ ] Link contacts to roles and record referral requests and outcomes
- [ ] Reminders to send thank-you messages

**Insights**
- [ ] Accept and reply rates by template, company, and day of week
- [ ] Weekly summary report
- [ ] Template A/B comparison to see which notes perform best

**Platform and quality**
- [ ] Installable PWA with offline support
- [ ] Optional backend (Node.js or FastAPI with PostgreSQL) with authentication and sync across devices
- [ ] Browser notifications for follow-up reminders
- [ ] Browser extension that lets you log a profile with one click while browsing (manual action only, no automation)
- [ ] Automated tests for the metric calculations
- [ ] Accessibility audit and keyboard-navigation improvements
- [ ] Multi-language templates

## Contributing

Contributions are welcome.

1. Fork the repository and create a branch: `git checkout -b feature/your-feature`
2. Make your change and test it in the browser, including mobile and dark mode.
3. Commit with a clear message and open a pull request describing what changed and why.

Please keep the project dependency-free and privacy-first. Features that add tracking or automate actions on LinkedIn will not be accepted.

## License

Released under the MIT License. See the [LICENSE](LICENSE) file for details.

## Author

Built by **Santhosh Sharma**.

- LinkedIn: [linkedin.com/in/santhoshsharma](https://www.linkedin.com/in/santhoshsharma)
- GitHub: [github.com/santhoshsharrma](https://github.com/santhoshsharrma)
- Portfolio: [santhoshsharrma.me](https://santhoshsharrma.me)
- Live demo: [linkedin-networking-engine.vercel.app](https://linkedin-networking-engine.vercel.app/)
