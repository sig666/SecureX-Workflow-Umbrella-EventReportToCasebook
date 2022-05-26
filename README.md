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
