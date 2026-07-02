# Task 1 – GTM Event Schema

## Overview

OrthoNow currently has only basic page view tracking, which is not enough to understand how users interact with the website or where they leave the booking journey. The objective of this implementation is to track meaningful user interactions, measure the consultation booking funnel, and provide accurate data for Google Analytics 4 and Google Ads optimisation.

---

# GTM Event Schema

| Event Name | Trigger Type | Key Parameters | GA4 Report / Audience |
|------------|--------------|----------------|-----------------------|
| consultation_form_submitted | Form Submission Trigger | form_name, page_name, submission_source | Conversions |
| booking_step_complete | Custom Event Trigger | step_number, step_name, clinic_location | Funnel Exploration |
| call_now_clicked | Click Trigger | phone_number, clinic_location, page_name | Engagement |
| whatsapp_chat_opened | Click Trigger | page_name, clinic_location, button_location | Engagement |
| patient_guide_download | Form Submission + Click Trigger | guide_name, page_name, download_type | Lead Generation |
| clinic_page_view | Page View Trigger | clinic_name, city, page_title | Pages & Screens Report |
| blog_scroll_25 | Scroll Depth Trigger | article_title, scroll_percentage, page_name | Engagement |
| blog_scroll_50 | Scroll Depth Trigger | article_title, scroll_percentage, page_name | Engagement |
| blog_scroll_75 | Scroll Depth Trigger | article_title, scroll_percentage, page_name | Content Performance |
| blog_scroll_100 | Scroll Depth Trigger | article_title, scroll_percentage, page_name | Content Completion |

---

# Booking Funnel Tracking

The appointment booking process contains three important steps. Instead of relying on GTM to detect these automatically, the frontend developer will trigger a custom `window.dataLayer.push()` after every successfully completed step.

This approach allows Google Tag Manager to capture every stage of the booking journey and send the information to Google Analytics 4 for Funnel Exploration.

---

## Step 1 – Clinic & Specialty Selection

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 1,
  step_name: "location_specialty_selected",
  clinic_location: "Bengaluru",
  specialty: "Orthopaedic"
});
```

---

## Step 2 – Patient Details

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 2,
  step_name: "patient_details_entered",
  preferred_date: "2026-07-05",
  form_name: "Consultation Form"
});
```

---

## Step 3 – Booking Confirmation

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 3,
  step_name: "booking_confirmed",
  booking_status: "Success",
  page_name: "Consultation Landing Page"
});
```

---

# Funnel Drop-off Tracking

Each booking step sends its own custom event to Google Tag Manager. GTM forwards these events to Google Analytics 4.

Inside GA4, the Funnel Exploration report is configured with the following sequence:

1. Location & Specialty Selected
2. Patient Details Entered
3. Booking Confirmed

This setup makes it easy to identify the exact stage where users abandon the booking process. For example, if a large number of users complete Step 1 but do not reach Step 2, the marketing or product team can investigate whether the form is too long, confusing, or causing technical issues.

---

# Google Ads Conversion

The conversion event selected for Google Ads is:

**consultation_form_submitted**

### Why this event?

This event represents a completed consultation request, which is the primary business goal of the landing page. Tracking button clicks or WhatsApp opens would only measure user intent, while a successful consultation form submission represents an actual lead.

Using this event as the conversion action allows Google Ads to optimise campaigns towards users who are more likely to submit consultation requests instead of simply interacting with the page.

---

# Implementation Notes

- Google Tag Manager listens for custom `window.dataLayer.push()` events.
- The frontend developer is responsible for triggering these events after each successful booking step.
- GTM captures the events and forwards them to Google Analytics 4.
- Google Ads imports the final consultation submission event as a conversion for campaign optimisation.
- Step-level tracking helps identify drop-off points and improve the booking experience through data-driven optimisation.