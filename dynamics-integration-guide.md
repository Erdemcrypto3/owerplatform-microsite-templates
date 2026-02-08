# Dynamics 365 CRM Integration Guide

## Integration Architecture

Microsite Form → Power Automate Webhook → Dynamics 365 CRM ↓ Lead Created ↓ Confirmation Email


## Setup Steps

### Step 1: Create Power Automate Flow

1. Go to Power Automate (flow.microsoft.com)
2. Create new **Instant cloud flow**
3. Trigger: **"When a HTTP request is received"**
4. Add action: **"Create a new record"** (Dataverse)
5. Select table: **"Leads"**
6. Map fields from HTTP request to Lead fields

### Step 2: Configure HTTP Trigger

The trigger should accept JSON like this:

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phone": "+1234567890",
  "company": "Example Corp",
  "message": "Interested in your services",
  "campaignSource": "TEMPLATE_001",
  "websiteUrl": "https://microsite.example.com"
}
