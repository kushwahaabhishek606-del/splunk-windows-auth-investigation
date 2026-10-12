 SOC L1 Incident Investigation Report
 Splunk SIEM — Windows Authentication Monitoring

Platform: Splunk Enterprise 10.6.0.5  
**Data Source:** Windows Security Event Logs  
**Host:** `DESKTOP-R5B4BOT`  
**Account Observed:** `socuser`  
**Investigation Type:** Authentication Event Analysis

### 1. Objective
Investigate Windows authentication events in Splunk, identify repeated failed logons, and correlate them with successful-logon records.

### 2. Evidence and Findings
- **Event ID 4625:** Failed logon.
- **Event ID 4624:** Successful logon.
- Eight matching failed-logon events were observed in the previously examined search results.
- Six failed-logon records occurred between 10:47:36 AM and 10:48:03 AM, approximately 27 seconds apart.
- Two successful-logon records were observed at 10:49:09 AM. The inspected events showed Logon Type 2 (interactive logon).
- The inspected failed-logon event contained source address `127.0.0.1`.

### 3. Preliminary Assessment
Repeated failed logons followed by successful-logon records warrant further investigation. However, the available evidence does not establish that the successful logons resulted from the failed attempts. A brute-force attack and an external attacker have not been confirmed.

### 4. Detection and Monitoring
A Splunk dashboard named `SOC L1 - Windows Authentication Monitoring` was created to display authentication activity. A scheduled alert named `Multiple Failed Logins - SOC L1` was configured to identify users with five or more matching failed-logon events.

The alert is enabled, but its end-to-end firing behavior has not yet been validated. The trigger condition was adjusted during the lab; the scheduled execution and resulting trigger record still require verification.

### 5. Conclusion
The lab demonstrated Windows Security log ingestion, SPL-based authentication searches, dashboard creation, and scheduled alert configuration in Splunk. Further validation is required before concluding that an attack occurred.

### 6. Recommended Next Steps
1. Validate the alert using newly generated lab events and an appropriate search time window.
2. Review the related event details and timestamps.
3. Document the final alert test result.
4. Preserve screenshots as supporting evidence.

**Environment:** Authorized, isolated lab environment.
