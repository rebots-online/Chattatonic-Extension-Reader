# Landing

- Slug: `landing`
- Stitch screen: `projects/81951782971452349/screens/f7672438786f478f877bbd759badb53d`
- HTML file: `projects/81951782971452349/files/f132263e278e4053acf4528d2730f53a` (saved as `index.html`, exact export decoded from the download response)
- Screenshot file: `projects/81951782971452349/files/78bf55a83859488dae0daeab404894bc` (saved as `screenshot.png`, 2560x7628)
- Device type reported by Stitch: DESKTOP
- Intent: Marketing home page that explains the product and leads to install, web app and pricing.
- Linked CHECKLIST tasks: none yet
- Operator clearance: not cleared

## Checked against the prompt (automated, from the saved HTML)

- Element ids in export: 18 (15 distinct)
- Requested ids missing: none
- Requested strings missing: "Free: one voice, 20 minutes a day. No card."
- Duplicate ids: `nav-how-it-works`, `nav-pricing`, `nav-voices`
- Off-vocabulary words found: subscri
- Ids added by Stitch beyond those requested: `footer-pricing`, `nav-add-to-chrome`, `nav-how-it-works`, `nav-sign-in`, `nav-voices`, `pass-day-select`, `pass-lifetime-select`, `pass-month-select`, `pass-year-select`, `tailwind-config`

## Deviations noted by review

- Stitch added marketing copy that uses the word "subscriptions" in the negative: "Flexible passes. Zero subscriptions. Pay once when you need it. No surprise monthly rebills". DESIGN.md says never to use "subscription" wording.
- "No card." became "No card required."
- Stat tiles were reworded (for example "100% On-Device", "Web & PDF Highlighting").
- Nav ids `nav-how-it-works`, `nav-pricing`, `nav-voices` each appear twice (header and footer); ids must be made unique before wiring.
- A second Landing screen exists in Stitch (`projects/81951782971452349/screens/826ee8bd6e854436b540b7f6c2c604f8`), created by a retry after a client timeout. It is not frozen here.
