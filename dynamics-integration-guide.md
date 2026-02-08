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
Step 3: Map Lead Fields


HTTP Field	Dynamics Field	Required
firstName	firstname	Yes
lastName	lastname	Yes
email	emailaddress1	Yes
phone	telephone1	No
company	companyname	No
message	description	No
campaignSource	Subject or custom field	Yes
websiteUrl	websiteurl	No

Step 4: Add Error Handling
Add a "Scope" action and configure:

Try: Main logic
Catch: Send error notification
Finally: Log to analytics
Step 5: Get Webhook URL
Save the flow
Copy the HTTP POST URL
Add this URL to your microsite's config.js file
Security Considerations
Protect Your Webhook
Use HTTPS only - Reject HTTP requests
Implement rate limiting - Prevent spam
Validate origin - Check referrer headers
Add reCAPTCHA - Prevent bot submissions
Sanitize inputs - Prevent injection attacks
Authentication Options
Option 1: Public Webhook (Simple)
No authentication required
Relies on obscurity of URL
Add reCAPTCHA for protection
Best for: Low-risk lead capture
Option 2: Shared Secret (Better)
Include secret key in request headers
Validate in Power Automate
Best for: Medium-risk applications
Option 3: OAuth 2.0 (Most Secure)
Full authentication flow
Token-based access
Best for: High-security requirements
