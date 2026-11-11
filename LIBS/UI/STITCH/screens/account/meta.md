# Account

- Slug: `account`
- Stitch screen: `projects/81951782971452349/screens/56dd16ecf1cd4a5ba8fa581ae8bdfe5c`
- HTML file: `projects/81951782971452349/files/23369037da1e4d638c2772a141ec0576` (saved as `index.html`, exact export decoded from the download response)
- Screenshot file: `projects/81951782971452349/files/aea857884d0c45abafaaf2c6bb90bdc6` (saved as `screenshot.png`, 2560x3024)
- Device type reported by Stitch: DESKTOP
- Intent: Pass status, licence key, devices, render credit balance and purchases; includes the Free state.
- Linked CHECKLIST tasks: none yet
- Operator clearance: not cleared

## Checked against the prompt (automated, from the saved HTML)

- Element ids in export: 15 (15 distinct)
- Requested ids missing: none
- Requested strings missing: "12 of 20 minutes used today"
- Duplicate ids: none
- Off-vocabulary words found: stripe
- Ids added by Stitch beyond those requested: `account-receipt-2`, `key-display-text`, `tailwind-config`, `toast`, `toast-message`

## Deviations noted by review

- Stitch added a footer line "Payment via Stripe Direct" with an invented "Tax ID: US-92817290". This names a billing provider and invents data; it was not in the prompt and must be removed or replaced before clearance.
- Free-state inset reads "12 of 20 min used today" (prompt: "12 of 20 minutes used today") and "1 voice standard" (prompt: "1 voice").
- Stitch added a top bar breadcrumb "ACCOUNT / Settings & Billing" and a "Licence key copied to clipboard" toast.
