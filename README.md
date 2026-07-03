# OrthoNow Consultation Landing Page

## GTM & Marketing Analytics Assignment

This project was developed as part of a GTM & Marketing Analytics assignment. The objective was to design a consultation landing page, define a complete Google Tag Manager event tracking strategy, and propose a backend integration architecture that securely connects the landing page with HubSpot CRM, WhatsApp Business API, Google Analytics 4, and Google Ads.

---

# Project Overview

The landing page allows users to book an orthopaedic consultation by submitting only two details:

* Name
* Phone Number

The solution focuses on three major areas:

* **Task 1:** Google Tag Manager Event Schema
* **Task 2:** Consultation Landing Page Development
* **Task 3:** Integration Architecture Design

---

# Technology Stack

* HTML5
* CSS3
* Vanilla JavaScript
* Google Tag Manager (Concept)
* Google Analytics 4
* Google Ads
* HubSpot CRM (Architecture)
* Karix WhatsApp Business API (Architecture)

---

# Project Structure

```text
.
├── index.html
├── README.md
└── assets/
```

---

# Task 1 – GTM Event Schema

## Objective

The first task was to design a Google Tag Manager event schema that captures meaningful user interactions instead of tracking only page views.

The schema helps marketing teams understand user behaviour, identify drop-off points, measure engagement, and optimise Google Ads campaigns.

## Implemented Events

| Event Name                  | Purpose                                 |
| --------------------------- | --------------------------------------- |
| consultation_form_submitted | Tracks successful consultation requests |
| booking_step_complete       | Tracks booking funnel progress          |
| call_now_clicked            | Tracks click-to-call interactions       |
| whatsapp_chat_opened        | Tracks WhatsApp engagement              |
| patient_guide_download      | Tracks guide downloads                  |
| clinic_page_view            | Tracks clinic page visits               |
| blog_scroll_25              | Tracks 25% scroll depth                 |
| blog_scroll_50              | Tracks 50% scroll depth                 |
| blog_scroll_75              | Tracks 75% scroll depth                 |
| blog_scroll_100             | Tracks complete article reading         |

---

## Booking Funnel

The booking process is divided into three measurable stages.

```text
Clinic & Specialty Selected
            │
            ▼
Patient Details Entered
            │
            ▼
Booking Confirmed
```

Each completed step triggers a custom `window.dataLayer.push()` event.

These events are captured by Google Tag Manager and forwarded to Google Analytics 4 for Funnel Exploration.

This enables the business team to identify where users abandon the booking process and optimise the user experience.

---

## Primary Conversion Event

The primary business conversion selected for Google Ads is:

```javascript
window.dataLayer.push({
    event: "consultation_form_submitted",
    form_name: "Consultation Form",
    page_name: "Consultation Landing Page",
    submission_source: "Hero Form"
});
```

This event represents a completed consultation request rather than a simple button click, making it a meaningful conversion signal for campaign optimisation.

---

# Task 2 – Consultation Landing Page

## Objective

The second task was to build a responsive consultation landing page that encourages users to book an appointment while providing a clean user experience and supporting marketing analytics.

---

## Features Implemented

### Responsive Design

* Desktop layout
* Tablet layout
* Mobile responsive layout

---

### User Interface

The landing page includes:

* Sticky navigation header
* Hero section
* Consultation booking form
* SVG medical illustration
* Statistics section
* Trust indicators
* Patient testimonial section
* Footer with contact details

---

### Form Validation

The consultation form validates:

* Required Name field
* Required Phone Number field
* Indian mobile number validation
* Error messages
* Success confirmation message

---

### JavaScript Functionality

The frontend performs:

* Client-side validation
* Invalid field highlighting
* Success message display
* Google Tag Manager event triggering using `window.dataLayer.push()`

---

### Accessibility

The page also includes:

* Semantic HTML
* Keyboard focus indicators
* ARIA attributes
* Responsive typography
* Reduced motion support

---

# Task 3 – Integration Design

## Objective

The third task was to design a scalable backend architecture that securely integrates the landing page with CRM, WhatsApp automation, Google Analytics 4, and Google Ads.

---

## Complete Integration Flow

```text
User submits consultation form
            │
            ▼
Frontend Validation
            │
            ▼
Backend API
            │
            ▼
HubSpot CRM
            │
            ▼
Karix WhatsApp Business API
            │
            ▼
window.dataLayer.push()
            │
            ▼
Google Tag Manager
            │
            ▼
Google Analytics 4
            │
            ▼
Google Ads Conversion
```

---

## Backend Responsibilities

The backend is responsible for:

* Receiving patient details
* Validating requests
* Searching HubSpot using phone number
* Creating or updating contacts
* Logging API requests
* Managing retries
* Calling the Karix WhatsApp API
* Returning success responses

Keeping these responsibilities on the backend prevents API keys from being exposed to the browser.

---

## HubSpot CRM Integration

The backend performs duplicate checking using the patient's phone number.

If a contact already exists:

* Update existing record

Otherwise:

* Create a new contact

Stored information includes:

* Name
* Phone Number
* Clinic Preference
* Lead Source
* Lead Status

---

## WhatsApp Confirmation

After HubSpot successfully processes the lead, the backend calls the Karix WhatsApp Business API.

An automated confirmation message is sent to the patient confirming that the consultation request has been received.

---

## Google Analytics & Google Ads

The frontend pushes a custom event using:

```javascript
window.dataLayer.push({
    event: "consultation_form_submitted"
});
```

Google Tag Manager captures this event and forwards it to Google Analytics 4.

The same event is imported into Google Ads as the primary conversion action for campaign optimisation.

---

## Failure Handling

Possible failure points include:

* HubSpot API downtime
* Karix API downtime
* Backend server failures
* Network issues

To prevent lead loss, the architecture recommends:

* Temporary database or queue storage
* Automatic retry mechanism
* API logging
* Error monitoring
* SLA alerts

---

# Key Learning Outcomes

This project demonstrates knowledge of:

* Google Tag Manager Event Design
* Google Analytics 4 Tracking
* Google Ads Conversion Tracking
* Conversion Funnel Analysis
* Frontend Form Validation
* JavaScript Event Tracking
* CRM Integration Design
* WhatsApp Business API Workflow
* Backend Architecture Design
* Marketing Analytics Concepts

---

# Future Improvements

* Backend implementation using Node.js/Express or Spring Boot
* Live HubSpot CRM integration
* Live Karix WhatsApp integration
* GTM Container configuration
* GA4 Dashboard
* Google Ads Conversion Import
* AWS Deployment

---

# How to Run

Clone the repository:

```bash
git clone <repository-url>
```

Open the project folder:

```bash
cd <repository-folder>
```

Launch the application by opening **index.html** in your browser.

No additional dependencies or build tools are required.

---

# Author

**Alok Raj**

MERN Stack Developer | MongoDB | Express.js | React.js | Node.js | JavaScript | REST APIs | HTML | CSS | Git & GitHub

---

# License

This project was developed for educational purposes as part of a GTM & Marketing Analytics assignment.
