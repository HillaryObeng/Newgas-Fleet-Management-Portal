# Newgas Fleet Management Portal — Codebase Documentation

## Project Overview

A fully-featured, role-based vehicle request and fleet management web application built
for Newgas Operations. Single-file HTML deployment — no server, no build step, no
dependencies beyond Google Fonts (loaded from CDN; falls back gracefully offline).

---

## File Structure

```
newgas-fleet-portal/
│
├── index.html                    ← Production file (self-contained, deploy this)
│
├── README.md                     ← This file
│
├── src/                          ← Segmented source for development/review
│   ├── 01_structure.html         ← Page shell, <head>, meta, font imports
│   ├── 02_markup.html            ← Full HTML body: auth wall, nav, all views
│   │
│   ├── css/
│   │   ├── 01_tokens.css         ← CSS custom properties, reset, scrollbars
│   │   ├── 02_nav.css            ← Navigation, notification panel, user pill
│   │   ├── 03_layout.css         ← Views, hero strips, page wrappers, KPI grid
│   │   ├── 04_components.css     ← Cards, chips, table, badges, buttons
│   │   ├── 05_form.css           ← Form system, type tiles, priority tiles
│   │   ├── 06_views.css          ← Request cards, timeline, detail grid, modal
│   │   ├── 07_admin.css          ← Admin lock, admin panel, audit, fleet
│   │   ├── 08_dashboard.css      ← Dashboard-specific styles, charts, sparkline
│   │   ├── 09_auth.css           ← Login wall, password strength, lockout bar
│   │   ├── 10_darkmode.css       ← Complete dark mode overrides
│   │   └── 11_utilities.css      ← Toast, print, responsive, dept colours
│   │
│   └── js/
│       ├── 01_data.js            ← Master data: COMPANY, FLEET, STAFF_DIR
│       ├── 02_persistence.js     ← localStorage keys, counters, save/load
│       ├── 03_helpers.js         ← Utility functions, badges, date helpers
│       ├── 04_navigation.js      ← gotoView, nav tab handling, keyboard shortcuts
│       ├── 05_form.js            ← 4-step request form, validation, auto-save
│       ├── 06_requests.js        ← Cancel, detail modal, My Requests view
│       ├── 07_allocations.js     ← Today's Allocations view
│       ├── 08_admin_requests.js  ← Admin request management, bulk actions
│       ├── 09_admin_workflow.js  ← Approve, reject, assign vehicle, complete
│       ├── 10_admin_fleet.js     ← Fleet CRUD management
│       ├── 11_admin_people.js    ← People/staff management
│       ├── 12_admin_depts.js     ← Department, units, categories management
│       ├── 13_admin_locations.js ← Destination locations management
│       ├── 14_notifications.js   ← Notification system, bell, escalations
│       ├── 15_dashboard.js       ← Dashboard engine, charts, KPIs, extras
│       ├── 16_auth.js            ← Full authentication engine
│       ├── 17_session.js         ← Session timeout, activity tracking
│       ├── 18_darkmode.js        ← Dark mode toggle and persistence
│       ├── 19_pdf.js             ← PDF/print export functions
│       └── 20_boot.js            ← Initialisation sequence
│
└── credentials.md                ← Default login credentials (keep confidential)
```

---

## Deployment

### Option A — Single File (Recommended for intranet)
Copy `index.html` to any shared network drive or internal web server.
Open in any modern browser. No installation required.

### Option B — Local File
Double-click `index.html` to open directly in Chrome, Firefox or Edge.
All data persists in the browser's localStorage on that machine.

### Option C — Internal Web Server (Best practice)
Serve `index.html` from any static file server:
```bash
# Python
python3 -m http.server 8080

# Node.js
npx serve .

# nginx — point root to the folder containing index.html
```

---

## Data Storage

All data is stored in the browser's `localStorage` under these keys:

| Key           | Contents                          | Notes                        |
|---------------|-----------------------------------|------------------------------|
| `ngs_req`     | All vehicle requests              | Primary data store           |
| `ngs_aud`     | Audit log (status history)        | Append-only                  |
| `ngs_flt`     | Fleet register                    | Editable by Admin/HR         |
| `ngs_ntf`     | Notifications                     | Per-session bell items       |
| `ngs_staff`   | Staff directory                   | Editable by Admin/HR         |
| `ngs_company` | Company structure (depts/units)   | Editable by Admin/HR         |
| `ngs_locs`    | Destination locations             | Editable by Admin/HR         |
| `ngs_pw`      | Hashed passwords (SHA-256)        | Never stored in plaintext    |
| `ngs_lck`     | Account lockout state             | Auto-clears after 15 min     |
| `ngs_session` | Current session                   | Cleared on tab close         |
| `ngs_persist` | Remember-me session (7 days)      | Expires automatically        |
| `ngs_activity`| Login/logout activity log         | Last 200 entries             |
| `ngs_draft`   | Auto-saved form draft             | Cleared on submit            |
| `ngs_theme`   | Dark/light preference             | Persists across sessions     |
| `ngs_rc/lc/nc`| ID sequence counters              | Request / Log / Notif IDs    |

**Important:** localStorage is device and browser specific. For multi-device access,
a backend API (Node.js/Python + PostgreSQL) is required for Phase 2.

---

## Role Access Matrix

| Feature                        | Staff | Driver | Supervisor | Admin/HR | Executive |
|-------------------------------|-------|--------|------------|----------|-----------|
| Submit new request            | ✓     | ✓      | ✓          | ✓        | ✓         |
| View own requests             | ✓     | ✓      | ✓          | ✓        | ✓         |
| View today's allocations      | ✓     | ✓      | ✓          | ✓        | ✓         |
| Dashboard                     | ✓     | ✓      | ✓ (dept)   | ✓ (all)  | ✓ (all)   |
| Approve / Reject requests     | —     | —      | ✓ (dept)   | ✓        | —         |
| Assign vehicles               | —     | —      | —          | ✓        | —         |
| Admin Panel (full)            | —     | —      | —          | ✓        | —         |
| Manage Staff / Fleet / Depts  | —     | —      | —          | ✓        | —         |
| Reset passwords               | —     | —      | —          | ✓        | —         |
| Export CSV / PDF              | —     | —      | —          | ✓        | —         |
| View audit log                | —     | —      | —          | ✓        | —         |

---

## Authentication

**Default password formula:** first 4 characters of first name (lowercase) + last 4 digits of phone number
- Example: Esi Ampofo (phone: 0247778888) → `esim8888`
- Exception: names under 4 chars pad with a dot → Ama Donkor → `ama.3344`

**Admin access code (lock screen):** `newgas2024`
Admin/HR Officers bypass this automatically on login.

**First login:** Every employee is forced to change their password on first login
before accessing any part of the portal.

**Security:**
- Passwords hashed with SHA-256 via Web Crypto API
- Account locked for 15 minutes after 5 failed attempts
- Session expires after 30 minutes of inactivity (2-minute warning)
- Remember Me option stores session for 7 days

---

## Phase 2 Roadmap

1. **Backend API** — Node.js/Express + PostgreSQL for multi-device data sync
2. **Email notifications** — Sendgrid/Mailgun integration for approval/rejection alerts
3. **PWA / offline mode** — Service worker for field staff without reliable internet
4. **HR system integration** — Auto-sync staff from existing HR platform
5. **Telematics integration** — Auto-populate mileage from vehicle GPS data
6. **Finance integration** — Trip cost allocation against department budgets

---

## Browser Compatibility

| Browser         | Support |
|-----------------|---------|
| Chrome 90+      | ✓ Full  |
| Firefox 88+     | ✓ Full  |
| Edge 90+        | ✓ Full  |
| Safari 14+      | ✓ Full  |
| IE 11           | ✗ Not supported |

Web Crypto API (SHA-256) requires HTTPS or localhost in some browsers.
For local file deployment, Chrome is recommended.

---

## Support

IT Support: **ict@newgas.com.gh** · Extension 100
Portal version: **3.0** — Newgas Fleet Management Portal
