# SecureX-Workflow-Umbrella-EventReportToCasebook
This workflow utilizes the DNS Activity endpoint of the Umbrella Reporting API to extract events that occurred within a specified time period (the default setting for this template is 1 hour), report the time of occurrence, verdict, Internal IP address, External IP address to be used, and domain for the destination for the event, and record the results in the Ribbon Casebook.

# Change Log
- May, 26, 2022 : Initial Release

# Requirements
The following system atomics are used by this workflow:
- Umbrella - Reporting V2 - Get Token
- Threat Response - Generate Access Token
- Threat Response - Create Incident

The following atomic actions must be imported before you can import this workflow:
- None

The targets and account keys listed at the bottom of the page
- Cisco Umbrella

# Workflow Steps
1. Get a token for the Umbrella Reporting API
2. Request DNS Event Details (specified Category ID, From Time, To Time, number of fetch events)
3. Check if the request was successful:
 - If it wasn’t, output an error and end the workflow
 - If it was:
   - Convert the statistics to a table
   - Loop through the table checking if any of the categories are in scope. If it is, add it to the Incident text
   - Convert JSON Text to XML
   - Convert XML to HTML Incident Message
4. Generate an access token for SecureX and create an incident to Ribbon Incident Manager

# Installation
1. Browse to your SecureX orchestration instance. This wille be a different URL depending on the region your account is in:
 - US: https://securex-ao.us.security.cisco.com/orch-ui/workflows/
 - EU: https://securex-ao.eu.security.cisco.com/orch-ui/workflows/
 - APJC: https://securex-ao.apjc.security.cisco.com/orch-ui/workflows/
2. Click on **Import** to import the workflow.
3. Select **Browse** from Import From
4. Open **SecureX-Workflow-Umbrella-EventReportToCasebook.json** and Copy text
5. Paste to **Paste JSON or upload the workflow to import** and click **Import**

# Configuration
- Set the `Umbrella Organization ID` in local variable to your Umbrella organization’s ID (found in your Umbrella dashboard’s URL)
- Set the `Category ID` in local variable to fetch Event Details you want to alert on (ex: 55,188,72,148,151,66)
- Set the `Request Threshold` in local variable to set number of Events to fetch  per hour you want to alert on. This is 10 by default
- By default, the workflow is configured to run once an hour using the `0023 - Umbrella - Excessive Requests to Incidents schedule`. When you import the workflow, the schedule trigger will be disabled. To enable the schedule:
  - Open the workflow in the workflow editor
  - Scroll down to the **Triggers** section of the workflow’s properties and click **Umbrella Report Polling**
  - Uncheck the **Disable Trigger** box and click **Save**
- If you change the schedule to every 2 hours, you would need to change `Relative Url` parameter  **from=-2hours** instead of from=-1hours in `WEB SERVICE - Request Activities`.

# Targets
Target Group: `Default TargetGroup`

# Account Keys
Default

# Reccomendation
To import 023 - Umbrella - Excessive Requests to Incidents schedule and check the details in this Workflow
Many compornents have been adapted.
