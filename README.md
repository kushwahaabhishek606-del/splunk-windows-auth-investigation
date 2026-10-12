# Splunk SIEM: Windows Authentication Investigation

## Project Overview
This SOC L1 lab project uses Splunk Enterprise to investigate Windows authentication events, identify repeated failed logons, and correlate authentication activity for incident triage.

## Objectives
- Ingest Windows Security logs using Splunk Universal Forwarder.
- Investigate failed logons (Event ID 4625) and successful logons (Event ID 4624).
- Use SPL searches to examine authentication activity.
- Create a dashboard for authentication monitoring.
- Configure a scheduled alert for repeated failed logons.
- Document findings in an incident investigation report.

## Lab Environment
- Splunk Enterprise 10.6.0.5
- Splunk Universal Forwarder on Windows 10
- Ubuntu Splunk server
- Windows Security Event Logs
- Splunk Search Processing Language (SPL)

## Detection Query
```spl
index=main "4625"
| rex field=_raw "<Data Name='TargetUserName'>(?<target_user>[^<]+)</Data>"
| stats count by target_user
| where count >= 5
```

This query extracts target usernames from matching failed-logon events and returns accounts with five or more matching events in the selected search time range.

## Investigation Findings
- Nine matching failed-logon events were displayed in the dashboard's selected time range during the latest check.
- The username table showed `socuser` with nine matching failed-logon events.
- The dashboard's successful-logon panel displayed 745 matching events in its selected time range.
- Six failed-logon records were previously observed between 10:47:36 AM and 10:48:03 AM, approximately 27 seconds apart.
- Two successful-logon records were previously observed at 10:49:09 AM.
- These counts depend on the selected time range and search results; they should not be treated as proof of a confirmed brute-force attack.

## Dashboard and Alert
Dashboard: `SOC L1 - Windows Authentication Monitoring`

Alert: `Multiple Failed Logins - SOC L1`

The alert is enabled, but end-to-end firing behavior has not yet been validated.

## Incident Report
See [`incident-report.md`](incident-report.md) for the investigation details and preliminary assessment.

## Disclaimer
This is an educational lab conducted in a controlled environment. Findings are limited to the available logs and do not establish a confirmed real-world attack.
