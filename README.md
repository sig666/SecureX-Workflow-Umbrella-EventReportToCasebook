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

