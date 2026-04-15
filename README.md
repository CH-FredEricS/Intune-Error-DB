# Intune Error Database

A standalone, offline-capable browser tool for quickly looking up Microsoft Intune error codes, their causes, and step-by-step resolution guidance.

---

## Overview

The Intune Error Database is a single HTML file that runs entirely in the browser — no server, no installation, no internet connection required. It contains 106 documented Intune errors across 13 categories, each with a full error code, description, common causes, resolution steps, and a direct link to the relevant Microsoft Learn or community documentation page.

---

## Getting Started

1. Download `intune-error-db.html`
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari)
3. No setup required — the tool is immediately usable

---

## Features

- **Category navigation** — left sidebar lists all error categories with entry counts; click any category to filter the list
- **Full-text search** — the search bar at the top searches across error codes, hex codes, titles, descriptions, causes, and resolution steps simultaneously
- **Detail view** — click any error card to open the full detail panel showing all fields
- **Microsoft Learn links** — each error links directly to the relevant official documentation page
- **Responsive layout** — adapts to any window size; the sidebar collapses on narrow screens with a back button for navigation
- **Fully offline** — all data is embedded in the HTML file; no external requests are made

---

## Error Categories

| Category | Errors | Description |
|---|---|---|
| Autopilot | 14 | Deployment, ESP, profile assignment, TPM attestation, hardware-specific issues |
| Applications | 19 | Win32 apps, MSI, Store apps, IME, detection rules, supersedence, exit codes, Android/iOS |
| Compliance | 8 | BitLocker, Defender AV, OS version, Secure Boot, firewall, passwords |
| Enrollment | 12 | Windows, iOS, Android enrollment, licensing, platform restrictions, registry blocks |
| Configuration | 15 | OMA-URI, certificates (SCEP/PKCS), Wi-Fi, VPN, email, update rings, Settings Catalog |
| Security | 8 | Security baselines, Conditional Access, LAPS, WHfB, MDE, ASR rules, DFCI |
| Co-management | 3 | ConfigMgr/Intune co-management, workload switching, MDM authority |
| Device Management | 8 | Check-in failures, remote actions, wipe/retire, scope tags, UPN issues |
| Mobile | 5 | iOS APN/ABM/VPP, Android work profiles, Managed Google Play |
| Connectors | 4 | ODJ Connector, Certificate Connector, Exchange Connector, NPS Extension |
| Device Sync | 4 | MDM certificate failures, private key issues, sync errors (0x80072f99, 0x80072f9a) |
| Autopilot Device Prep | 3 | AP-DP group ownership, Managed Installer OOBE issue, time zone deployment failure |
| App Protection (MAM) | 3 | MAM policy not applying, Conditional Access app requirements, data transfer restrictions |

---

## Each Error Entry Contains

| Field | Description |
|---|---|
| **Error code** | Decimal or hex error code (e.g. `0x87D1041C`) |
| **Category** | Which Intune area the error relates to |
| **Title** | Short human-readable summary of the error |
| **Description** | Full explanation of what the error means and when it occurs |
| **Common causes** | Bulleted list of the most frequent root causes |
| **Resolution steps** | Numbered step-by-step remediation guide |
| **Documentation link** | Direct URL to the relevant Microsoft Learn page |

---

## How to Use

### Browsing by category
Click a category name in the left sidebar to filter the error list to that topic. Click **All errors** at the top of the sidebar to return to the full list.

### Searching
Type any of the following into the search bar to find matching errors:
- Error code (e.g. `0x80180014`)
- Hex code
- Keyword from the title or description (e.g. `BitLocker`, `TPM`, `certificate`)
- Text from a cause or resolution step (e.g. `NDES`, `manage-bde`, `dsregcmd`)

Up to 10 results are shown as a dropdown. Click any result to jump directly to that error's detail view.

### Viewing error details
Click any error card in the list to open the full detail panel on the right. The detail panel shows all fields for the selected error. On narrow screens, the detail view replaces the list — use the **← Back** button to return.

---

## Adding New Errors

The error data is stored as a JavaScript array inside the HTML file. To add new entries, open the file in a text editor, locate the `const DB=[` array, and append a new object following this structure:

```js
{
  id: 'unique_id',
  cat: 'Category Name',
  code: '0xXXXXXXXX',
  title: 'Short title of the error',
  desc: 'Full description of what the error means.',
  causes: [
    'First common cause',
    'Second common cause',
    'Third common cause',
  ],
  steps: [
    'First resolution step',
    'Second resolution step',
    'Third resolution step',
  ],
  url: 'https://learn.microsoft.com/en-us/mem/...'
}
```

**Guidelines for new entries:**
- `id` must be unique across all entries (suggested format: `cat###`, e.g. `ap015`, `comp009`, `mam004`)
- `cat` must exactly match an existing category name, or a new category will be created automatically in the sidebar
- `code` should be the full hex error code as it appears in Intune or Windows logs; for non-code issues use a short descriptive identifier
- `causes` and `steps` should each have 3–5 entries for consistency
- `url` should point to the most relevant Microsoft Learn or trusted community documentation page for the error

Alternatively, share the error details in a conversation with Claude and request an updated HTML file — the new entries will be added and a fresh file generated for download.

---

## Technical Details

| Property | Value |
|---|---|
| File type | Single HTML file |
| Dependencies | None (no external libraries or CDN calls) |
| Browser support | All modern browsers (Chrome 90+, Edge 90+, Firefox 88+, Safari 14+) |
| Internet required | No — fully offline capable |
| Data storage | Embedded in HTML (JavaScript array) |
| Total entries | 106 errors |

---

## Known Limitations

- Error data is sourced from Microsoft Learn documentation and community blogs including call4cloud.nl, patchmypc.com, patchtuesday.com, msendpointmgr.com, and systemcenterdudes.com, reflecting knowledge available up to April 2026
- The tool does not sync with any live Microsoft database or API; new errors or changes after the last update will not be present until manually added
- There is no built-in export or print function; use the browser's built-in print/save-as-PDF feature if a printed reference is needed
- The search does not support wildcard operators or boolean logic; it performs a simple substring match across all fields
- Some entries reference known issues that may have been resolved by Microsoft since documentation; always verify current status on Microsoft Learn

---

## Sources

Error entries are compiled from the following sources:

| Source | Focus area |
|---|---|
| [Microsoft Learn — Intune](https://learn.microsoft.com/en-us/mem/intune/) | Official Microsoft documentation, error codes, known issues |
| [call4cloud.nl](https://call4cloud.nl) | Sync errors, MDM certificates, Settings Catalog, enrollment deep dives |
| [patchmypc.com/blog](https://patchmypc.com/blog) | Autopilot, IME, ESP, TPM attestation, Win32 app deployment |
| [patchtuesday.com](https://patchtuesday.com) | Win32 app lifecycle, exit codes, TPM attestation, Autopilot |
| [msendpointmgr.com](https://msendpointmgr.com) | Endpoint management, Win32 app state messages, Delivery Optimization |
| [systemcenterdudes.com](https://www.systemcenterdudes.com) | Autopilot errors, enrollment errors, Intune logs |

---

## File Reference

```
intune-error-db.html    — the complete tool (open this in a browser)
intune-error-db-docs.md — this documentation file
```
