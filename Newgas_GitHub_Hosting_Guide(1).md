# How to Host Newgas Fleet Portal on GitHub Pages
## Step-by-step guide — no coding experience required

---

## What is GitHub Pages?

GitHub Pages is a free hosting service by GitHub. It turns any file in your
GitHub repository into a live website accessible from a URL like:

  https://YOUR-USERNAME.github.io/newgas-fleet-portal/

It is completely free, requires no server setup, and is reliable enough for
an internal company tool accessed by dozens of employees.

---

## What You Need

1. A GitHub account (free) — sign up at https://github.com
2. The file: Newgas_Fleet_Portal.html (downloaded from this project)
3. A browser (Chrome recommended)

That is all. No terminal, no code editor, no server.

---

## STEP 1 — Create a GitHub Account

1. Go to https://github.com
2. Click "Sign up"
3. Choose a username (e.g. newgas-ops or your name)
4. Use your company email address
5. Verify your email and complete setup

---

## STEP 2 — Create a New Repository

A repository is like a folder on GitHub that stores your files.

1. After signing in, click the green "New" button (top left)
   OR go to: https://github.com/new

2. Fill in the form:
   - Repository name: newgas-fleet-portal
     (use exactly this — it becomes part of your URL)
   - Description: Newgas Fleet Management Portal
   - Visibility: Choose PRIVATE (recommended for a company tool)
     Note: GitHub Pages works on PRIVATE repos only with GitHub Pro/Teams.
     If using a free account, you must choose PUBLIC for Pages to work.
   - Check "Add a README file" ✓
   - Leave everything else as default

3. Click "Create repository" (green button)

---

## STEP 3 — Upload the Portal File

1. You are now inside your new repository
2. Click "Add file" → "Upload files"

3. Drag and drop your file onto the upload area:
   - Rename it to: index.html
     (IMPORTANT — it must be called index.html, not Newgas_Fleet_Portal.html)

4. Scroll down to "Commit changes"
   - Add a message: "Initial upload — Newgas Fleet Portal v3.0"
   - Leave "Commit directly to the main branch" selected
   - Click "Commit changes"

5. Wait a few seconds for the upload to complete

---

## STEP 4 — Enable GitHub Pages

1. In your repository, click "Settings" (top tab, gear icon)

2. In the left sidebar, scroll down and click "Pages"

3. Under "Source":
   - Click the dropdown that says "None"
   - Select "Deploy from a branch"

4. Under "Branch":
   - Select "main"
   - Keep the folder as "/ (root)"
   - Click "Save"

5. GitHub will show a message:
   "Your site is being published..."
   Wait 1–3 minutes.

6. Refresh the page. You will see:
   "Your site is live at https://YOUR-USERNAME.github.io/newgas-fleet-portal/"

---

## STEP 5 — Access Your Live Portal

Copy the URL shown (e.g. https://newgas-ops.github.io/newgas-fleet-portal/)
and share it with your team.

Employees open this URL in any browser on any device.
Bookmark it or add it to the company intranet homepage.

---

## STEP 6 — Update the Portal in Future

When a new version of the portal is ready:

1. Go to your repository on GitHub
2. Click on "index.html" in the file list
3. Click the pencil icon ✏ (Edit this file) — top right of the file view
   OR click "..." → "Upload new file" to replace it

4. If uploading:
   - Upload the new index.html
   - Commit the change with a message like "Update to v3.1"

5. GitHub Pages re-deploys automatically within 1–2 minutes

---

## Custom Domain (Optional — Advanced)

If you want employees to access it at a custom URL like
fleet.newgas.com.gh instead of the github.io URL:

1. Purchase/configure a domain through your DNS provider
2. In repository Settings → Pages → "Custom domain"
3. Enter: fleet.newgas.com.gh
4. At your DNS provider, add a CNAME record:
   Name: fleet
   Value: YOUR-USERNAME.github.io
5. Enable "Enforce HTTPS" ✓

Contact your ICT team (ict@newgas.com.gh) to help with the DNS step.

---

## Security Note

Because this is a static HTML file:
- All data is stored in each user's browser (localStorage)
- Data does NOT sync between employees' devices automatically
- For multi-device data sharing, a backend server is needed (Phase 2)

For a shared single-terminal deployment (e.g. one Admin/HR computer
in the office), GitHub Pages works perfectly.

For full multi-user, multi-device deployment across the company,
see the Phase 2 section in README.md.

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| "404 Not Found" after enabling Pages | Wait 3–5 minutes and refresh. Pages takes time to build. |
| Page shows file listing, not the app | Make sure the file is named exactly index.html (not Index.html or portal.html) |
| "Pages not available" error | Free accounts need a PUBLIC repository. Change visibility in Settings → General. |
| Login doesn't work | Clear browser cache / open in Incognito window (fresh localStorage) |
| Changes not appearing after update | Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac) |
| Employees can't access URL | Check if company firewall blocks github.io. Ask ICT to whitelist it. |

---

## Quick Reference

| Item | Value |
|------|-------|
| Repository name | newgas-fleet-portal |
| File name | index.html |
| Branch | main |
| Pages source | / (root) |
| Live URL format | https://USERNAME.github.io/newgas-fleet-portal/ |
| Admin access code | newgas2024 |
| IT Support | ict@newgas.com.gh · Ext. 100 |

---

## Full Setup Checklist

- [ ] GitHub account created
- [ ] Repository created (name: newgas-fleet-portal)
- [ ] index.html uploaded to repository
- [ ] GitHub Pages enabled (Settings → Pages → main branch)
- [ ] Live URL confirmed and working
- [ ] URL shared with Admin/HR team
- [ ] Admin/HR tested login (adelaide.nyarko@newgas.com.gh / adel6666)
- [ ] Credentials communicated individually to all staff
- [ ] URL bookmarked / added to intranet
- [ ] ICT team notified to whitelist github.io domain

---

Prepared for: Newgas Operations
Contact: ict@newgas.com.gh
