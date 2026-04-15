# Investigation Report: USR-007 — Jake Torres

## Trigger

Jake Torres had 7 High severity events within the timeframe of Jan 15 to Jan 17. Torres had sent data over multiple channels and even attempted to encrypt data
before transmission to an unauthorized destination. His recent resignation should be considered in the context of this investigation. 

## User Context

Sales, Sales Representative, Resigned, standard access.

## Timeline of Events

Day 1 (Jan 15)
- 9:45 PM — Downloaded client list from SharePoint. Alerted, not blocked.

Day 2 (Jan 16)
- 10:12 PM — USB copy of client list. Blocked.
- 10:30 PM — USB copy of sales pipeline report. Blocked.

Day 3 (Jan 17)
- 8:05 AM — Encrypted zip emailed to personal email. Quarantined.
- 11:22 AM — Client contacts uploaded to personal Google Drive. Blocked.
- 11:45 AM — Financial report uploaded to personal Google Drive. Blocked.
- 5:40 PM — Client file emailed externally. Blocked.
- 5:58 PM — Screenshot of client management app. Blocked.


## Analysis

Torres generated more alerts in 3 days than an average sales representative would generate within 1-2 months. Torres engaged in channel hopping and did not stop 
his behavior despite being blocked by our system. Further, he had multiple after-hours events which highly contrast his previous baseline: 100% between 
the hours of 0800 and 1800.

## Risk Determination
High Risk

## Recommended Actions
- Escalate to ITM Lead and HR immediately.
- Preserve endpoint image, email logs, and CASB session logs as evidence.
- Restrict Torres' access to Confidential and Restricted data.
- Assess whether exfiltrated data from Day 1 download requires client notification.


## DLP Tuning Recommendation
DLP-EMAIL-003 quarantined the encrypted zip but did not block. Consider auto-block.

EOF
