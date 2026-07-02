# Task 3 – Integration Design

## Overview

The consultation landing page is designed to collect only two user details: Name and Phone Number. After a successful form submission, the lead should automatically reach the CRM, trigger a WhatsApp confirmation message, and send a conversion event to Google Ads. The goal is to keep the process fast, reliable, and easy to maintain.

---

# Integration Flow

The complete flow is as follows:

User submits consultation form

↓

Frontend validates the form

↓

Backend API receives the request

↓

HubSpot Contact Create / Update

↓

Karix WhatsApp Business API

↓

Google Analytics 4

↓

Google Ads Conversion

---

# Step 1 – Landing Page

The landing page is built using HTML, CSS, and vanilla JavaScript.

When the user submits the consultation form, JavaScript validates the required fields and sends the request to the backend API. At the same time, a `window.dataLayer.push()` event is fired so that Google Tag Manager can record the consultation submission in Google Analytics 4.

---

# Step 2 – Backend Processing

The backend receives the patient details and performs all business logic.

Instead of sending data directly from the browser to HubSpot, the backend acts as the integration layer. This keeps API keys secure and allows validation, logging, retry mechanisms, and future integrations.

---

# Step 3 – HubSpot CRM

The backend searches HubSpot using the submitted phone number before creating a new contact.

If the phone number already exists, the existing contact is updated.

If no matching phone number is found, a new contact is created.

The following information is stored in HubSpot:

- Name
- Phone Number
- Clinic Preference
- Source = Google Ads – Consultation Landing Page
- Lead Status = New Enquiry

Using phone number lookup prevents duplicate patient records because this landing page does not collect email addresses.

---

# Step 4 – WhatsApp Confirmation

Once HubSpot successfully processes the lead, the backend calls the Karix WhatsApp Business API.

A confirmation message is sent automatically to the patient within two minutes confirming that the enquiry has been received.

---

# Step 5 – Google Ads Conversion

The frontend pushes the `consultation_form_submitted` event to the dataLayer.

Google Tag Manager captures this event and forwards it to Google Analytics 4.

The same event is imported into Google Ads as the primary conversion action.

This allows Google Ads to optimise campaigns based on actual consultation requests instead of page visits or button clicks.

---

# Biggest Failure Point

The biggest risk in this architecture is the HubSpot CRM integration.

If the HubSpot API is unavailable, new consultation requests may fail to reach the CRM.

To avoid losing patient enquiries, every form submission should first be stored temporarily in a database or message queue.

If HubSpot is unavailable, the backend retries the request automatically until it succeeds.

This ensures that no lead is lost because of a temporary service failure.

---

# WhatsApp SLA Monitoring

The WhatsApp confirmation message should be delivered within two minutes.

Possible reasons for delay include:

- HubSpot API delays
- Backend server issues
- Karix API downtime
- Network failures

To monitor the SLA, the application should maintain API logs, response times, retry counts, and error alerts.

If delivery exceeds the expected time or repeated failures occur, the development team should receive an alert so the issue can be investigated quickly.

---

# Summary

This architecture keeps the frontend simple while placing all business logic inside the backend.

The backend securely manages CRM integration, WhatsApp messaging, duplicate checking, logging, and retry mechanisms.

Google Tag Manager and Google Analytics 4 collect user behaviour, while Google Ads uses the consultation submission event as the primary conversion signal for campaign optimisation.