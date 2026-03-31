# Newgas Fleet Portal v10

GitHub-ready static version of the Newgas Fleet Portal, packaged from the latest v10 standalone build.

## What is included

- `index.html` — main application shell
- `assets/css/styles.css` — extracted portal styles
- `assets/js/app.js` — extracted application logic and data bootstrapping
- `docs/ARCHITECTURE.md` — structure and module overview
- `docs/ROLES_AND_WORKFLOW.md` — roles, workflow, and accountability logic
- `docs/DEPLOYMENT.md` — how to host on GitHub Pages or any static server
- `assets/img/` — workflow images for documentation
- `.nojekyll` — helps GitHub Pages serve static folders as-is

## Core functional areas

- Request submission workflow
- Supervisor notification-only visibility
- Admin/HR approval and assignment
- Vehicle register with compliance tracking
- Driver register with license controls
- Location manager with search and map support
- Dashboard reporting and accountability views
- Local browser persistence using `localStorage`

## Reporting and accountability included

- Number of requests by department
- Completed vs cancelled/rejected vs delayed trips
- Vehicle utilization rate
- Overdue return tracking
- Most requested locations
- Most used vehicles
- Compliance exceptions
- Requests per supervisor, department, and admin officer

## Driver management included

- Driver register
- License number
- License expiry date
- Driver phone number
- Driver status: Available, Off Duty, Assigned, Suspended
- Driver assignment together with vehicle
- Blocking of expired or invalid driver licenses during assignment

## Quick start

Open `index.html` directly in a browser for local testing.

For GitHub Pages:

1. Create a new repository.
2. Upload all files and folders from this package.
3. Commit to the default branch.
4. In repository settings, enable **GitHub Pages** from the root of the default branch.

## Important note

This is still a static browser-based app. Data is stored in the browser with `localStorage`, so it is suitable for prototype, demo, or controlled internal use. For real multi-user production use, move the data layer and authentication to a backend.
