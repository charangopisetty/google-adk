**High-level structure of our system**

- Goal: Automatically discover **local events**, identify **decision makers**, generate **qualified catering leads**, and produce **personalized outreach emails** for restaurants.
- Stack: **Google Agent Development Kit + Python + search APIs + email enrichment APIs + database + deployment API service.**

Below is a **`PROJECT.md` style specification** you can place in your repository.

---

# PROJECT.md

## AI Multi-Agent Lead Generation System for Restaurant Catering

## 1. Overview

This system uses a **multi-agent architecture** to discover events occurring near a user-provided ZIP code and generate **qualified catering leads** for restaurants.

The system performs the following pipeline:

1. Discover **upcoming events**
2. Identify **organizing companies**
3. Extract **decision-maker contacts**
4. Find **email addresses**
5. Generate **personalized outreach email**
6. Export leads to **CSV / dashboard**

The system is built using **Google Agent Development Kit** and deployed as a backend service that restaurant owners can access through a dashboard.

---

# 2. Definition of a Lead

A **lead** is defined as an event with a **high probability of requiring catering services**.

### Lead Qualification Criteria

| Criteria               | Description                                                    |
| ---------------------- | -------------------------------------------------------------- |
| Event Type             | Corporate event, conference, meetup, wedding, networking event |
| Event Size             | 30+ attendees                                                  |
| Event Date             | Within next 90 days                                            |
| Location               | Within restaurant delivery radius                              |
| Organizer Identifiable | Event organizer or company available                           |
| Contactable            | Email or contact form available                                |

### Lead Score

| Score  | Qualification |
| ------ | ------------- |
| 80–100 | Hot Lead      |
| 50–79  | Warm Lead     |
| <50    | Low Priority  |

---

# 3. Multi-Agent Architecture

## Agent 1 — Event Discovery Agent

Purpose: Identify upcoming events.

### Data Sources

- Event platforms
- Community calendars
- Meetup websites
- Conference websites
- Corporate events pages

### Output

```
Event Name
Event Type
Date
Location
Organizer
Event URL
Estimated Attendance
```

---

## Agent 2 — Organization Intelligence Agent

Purpose: Identify the organization responsible for the event.

### Extract

```
Organization Name
Website
Industry
Headquarters
Event Contact Page
```

### Tools

- Web search
- Website scraping
- Company database APIs

---

## Agent 3 — Contact Discovery Agent

Purpose: Identify decision makers who can approve catering.

### Target Roles

- Event Manager
- Office Manager
- HR Manager
- Community Manager
- Operations Manager
- Executive Assistant

### Output

```
Contact Name
Title
LinkedIn
Company
```

---

## Agent 4 — Email Enrichment Agent

Purpose: Find valid email addresses.

### Methods

- Email pattern inference
- Email enrichment APIs
- Company directory scraping

### Output

```
Email
Confidence Score
Verification Status
```

---

## Agent 5 — Personalization Agent

Purpose: Generate personalized catering outreach.

### Inputs

```
Restaurant Name
Cuisine Type
Location
Event Details
Organizer Name
```

### Output Example

```
Subject: Catering for <Event Name>

Hi <Name>,

I noticed that <Company> is hosting <Event Name> in <City>.
Our restaurant specializes in catering for corporate gatherings and would love to support your event with customized menus.

If catering is still being arranged, I’d be happy to share options.

Best,
<Restaurant Name>
```

---

# 4. Lead Data Schema

Each lead stored in database:

```
Lead_ID
Event_Name
Event_Date
Event_Location
Zip_Code
Event_Type
Estimated_Attendees

Organizer_Name
Organizer_Website

Contact_Name
Contact_Title
Contact_Email
Email_Verified

Lead_Score
Lead_Status
Generated_Email
Source_URL
Created_At
```

---

# 5. Owner Dashboard Requirements

Restaurant owners need a **simple decision interface**.

### Lead Overview Page

Display:

| Field        | Purpose              |
| ------------ | -------------------- |
| Event Name   | Identify opportunity |
| Event Date   | Time planning        |
| Distance     | Delivery feasibility |
| Event Size   | Catering potential   |
| Contact Name | Person to email      |
| Email        | Outreach             |
| Lead Score   | Priority             |

---

### Lead Detail Page

```
Event Information
Event website
Organizer details
Contact profile
Generated email
Lead score
```

Actions:

```
Send Email
Edit Email
Save Lead
Archive Lead
Export CSV
```

---

# 6. CSV Export Format

```
Event Name
Event Date
City
Organizer
Contact Name
Email
Lead Score
Generated Email
Source URL
```

---

# 7. Processing Pipeline

### Step 1

User enters:

```
ZIP code
Radius (miles)
Restaurant cuisine
Restaurant name
```

---

### Step 2

Event Discovery Agent collects **100–300 events**

---

### Step 3

Filter events:

```
Remove past events
Remove small events
Remove irrelevant categories
```

---

### Step 4

Organization Agent identifies **company responsible**

---

### Step 5

Contact Agent finds **decision maker**

---

### Step 6

Email Agent enriches **email address**

---

### Step 7

Personalization Agent generates **email template**

---

### Step 8

Lead stored in database

---

# 8. Deployment Architecture

```
Frontend Dashboard
        |
Backend API
        |
Agent Orchestrator (Google ADK)
        |
Agent Workers
    |    |    |
Events  Contacts  Email
        |
Database
        |
Lead Storage
```

---

# 9. Recommended Tech Stack

Backend

- Python
- **Google Agent Development Kit**

APIs

- Event discovery API
- Email enrichment API
- Search API

Storage

- PostgreSQL
- Supabase

Deployment

- Docker
- Cloud Run / Kubernetes

---

# 10. Metrics to Track

System quality metrics:

```
Events discovered per ZIP
Leads generated per event
Email discovery rate
Email verification rate
Lead conversion rate
```

Business metrics:

```
Emails sent
Replies received
Deals closed
Revenue per event
```

---

# 11. Future Improvements

- AI lead scoring model
- Catering demand prediction
- Automatic email sending
- CRM integration
- Event size estimation using LLM

---

## Optional Advanced Feature

Autonomous agent loop:

```
Discover Events → Qualify → Enrich Contacts → Generate Email → Store Leads
```

Runs daily for each restaurant.

---
