# 🎶 For You, <Name of your partner>

A small romantic surprise web app — built with love, music, and a No button that will never cooperate.

---

## What's inside

A single `index.html` file. No frameworks, no build steps, no dependencies. Just open it in a browser or host it anywhere.

**The journey:**
- A welcome screen just for him
- A love question with a Yes button that works and a No button that absolutely does not
- 9 questions — some MCQ, some typed — covering music, feelings, spicy things, and everything in between
- A piano with 8 coloured keys, each one hiding a reason
- A final page with a love note and a little PS 

---

## Google Sheets integration

His answers get saved automatically to a private Google Sheet after each question.

**Sheet:** <Link to your sheet>

### Setup (one time, 5 minutes)

**Step 1** — Open the sheet, go to `Extensions → Apps Script`

**Step 2** — Delete any existing code and paste this:

```js
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data  = JSON.parse(e.postData.contents);
  sheet.appendRow([data.timestamp, data.question, data.answer]);
  return ContentService.createTextOutput("OK");
}
```

**Step 3** — Click `Deploy → New deployment`
- Type: **Web app**
- Execute as: **Me**
- Who has access: **Anyone**
- Click **Deploy** and copy the web app URL

**Step 4** — In `index.html`, find this line and paste your URL:
```js
const SHEET_URL = "paste-your-url-here";
```

**Step 5** — Push to GitHub. Done.

> When Google shows a warning saying "app not verified" — click **Advanced** → **Go to project (unsafe)**. It's your own script accessing your own sheet, completely safe.

---

## Hosting on GitHub Pages

```bash
git init
git add index.html
git commit -m "your_commit_message"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/REPONAME.git
git push -u origin main
```

Then go to your repo → **Settings → Pages → Source: main / (root) → Save**

Your link will be live at:
```
https://YOURUSERNAME.github.io/REPONAME
```

> Keep the repo **public** for GitHub Pages to work on the free plan. Name it something innocent so he doesn't get suspicious before opening it 😂

---

## Customisation

Everything you'd want to change is clearly labelled in the script section:

| Thing | Where |
|---|---|
| Questions & answers | `const questions = [...]` |
| Piano reasons | `const pianoReasons = [...]` |
| Piano key emojis | `const pianoEmojis = [...]` |
| Welcome / final text | Page 0 and Page 5 HTML |
| Sheets URL | `const SHEET_URL = "..."` |

To make a question a **typed answer** instead of MCQ, add `type: "text"` to that question object and remove `opts` and `reactions`.

---

## Tech

- Vanilla HTML, CSS, JavaScript
- Google Fonts — Quicksand + Playfair Display
- Web Audio API for piano notes
- Google Apps Script for Sheets integration
- Zero npm, zero build, zero config

---

*made with an embarrassing amount of love* 
