# OrthoNow — Developer Assignment

Candidate: **Alok Raj**

Overview
--------
This repository contains a small landing page built for a developer assignment. The goal is to demonstrate a responsive consultation booking page, a GTM/GA4 event tracking strategy, and an integration design for CRM and messaging platforms.

Repository structure
--------------------
```
orthonow-developer-assignment-main/
├─ index.html                # Landing page (single-file: HTML, CSS, JS)
├─ task1-schema.md          # GTM event schema and tracking plan
├─ task3-integration.md     # Integration architecture (HubSpot, Karix, GA4, Ads)
└─ README.md                # This file
```

Key highlights
--------------
- Responsive landing page using HTML, CSS and vanilla JavaScript
- Client-side form validation and an accessibility-friendly success message
- `dataLayer` push on form submission for GTM/GA4 tracking
- Integration plan describing backend flows, CRM mapping and retry strategies

Tech stack
----------
- HTML5, CSS3
- JavaScript (vanilla)
- Google Tag Manager (GTM) / Google Analytics 4 (GA4)

How to run
----------
1. Clone or download the repository.
2. Open `index.html` in any modern browser (Chrome, Edge, Firefox).
3. Fill the consultation form and submit; the page shows an inline success message (no reload).
4. To inspect the tracking event, open the browser console and check `window.dataLayer` after submission.

Example `dataLayer` payload
----------------------------
```javascript
window.dataLayer.push({
  event: 'consultation_form_submitted',
  form_name: 'Consultation Form',
  page_name: 'Landing Page',
  patient_name: 'Rahul Sharma',
  phone_number: '9876543210'
});
```

Notes
-----
- The landing page is intentionally self-contained to make review simple.
- The integration design in `task3-integration.md` outlines how to forward leads to HubSpot and Karix, how to deduplicate phone numbers, and how to map events to GA4 and Google Ads.

Contact
-------
For questions or feedback: **Alok Raj**

---
Updated README for clarity and quick evaluation.