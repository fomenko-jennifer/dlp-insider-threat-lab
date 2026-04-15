#DLP & Insider Threat Monthly Report
## January 2025 | XYZ Bank — Information Security

### Executive Summary
In January, the DLP program processed 41 events across email, endpoint, and cloud channels involving 13 unique users. 2 investigations were escalated to the ITM lead, including a high-risk departing employee case (USR-007). Key action item: tune DLP-EMAIL-001 to reduce false positives from Finance department and implement automated HR departure correlation for DLP-CLOUD-003.

### Key Metrics

| Metric | January 2025 | Target | Status |
|--------|-------------|--------|--------|
| Total DLP Events | 41 | — | Baseline month |
| Events Blocked | 9 | — | — |
| Events Quarantined | 1 | — | — |
| Block Rate | 22.0% | — | — |
| Unique Users Flagged | 13 | — | — |
| Investigations Open | 10 | — | — |
| Investigations Escalated | 2 | — | — |
| Rules Tuned | 0 | ≥ 2/month | Below target |

### Events by Channel

| Channel | Count | % of Total |
|---------|-------|------------|
| Email | 19 | 46.3% |
| Cloud | 12 | 29.3% |
| Endpoint | 10 | 24.4% |

### Events by Severity

| Severity | Count | % of Total |
|----------|-------|------------|
| High | 11 | 26.8% |
| Medium | 21 | 51.2% |
| Low | 9 | 22.0% |

### Events by Action

| Action | Count | % of Total |
|--------|-------|------------|
| Alert | 31 | 75.6% |
| Block | 9 | 22.0% |
| Quarantine | 1 | 2.4% |

### Investigation Status

| Status | Count |
|--------|-------|
| Closed | 29 |
| Open | 10 |
| Escalated | 2 |

### Insider Threat Summary
- Users flagged for investigation: USR-007 (Jake Torres), USR-003 (David Kim)
- Investigation outcomes:
  - Closed (legitimate activity): 29 events
  - Open (under review): 10 events
  - Escalated to ITM Lead: 2 (USR-007 and USR-003)
- Top risk indicators observed: after-hours activity, USB data staging, channel-hopping after blocks, departing employee correlation

### Highlight: USR-007 — Jake Torres (Sales)
Departing employee generated 8 events across 3 days spanning all 3 channels (email, endpoint, cloud). Pattern consistent with data staging and attempted exfiltration. HR confirmed resignation effective January 31. Full investigation report attached. Recommended actions: access restriction, evidence preservation, HR coordination.

### Rule Tuning Activity

| Rule | Issue | Recommended Action | Projected Impact |
|------|-------|-------------------|-----------------|
| DLP-EMAIL-001 | Finance team triggers repeatedly on legitimate partner communications | Add approved partner domain exceptions | Est. 30-40% FP reduction for this rule |
| DLP-EP-002 | New employee OneDrive syncs trigger bulk download alerts | Add 7-day new-hire grace period | Est. 10-15 fewer alerts/month |
| DLP-CLOUD-003 | Alert-only action insufficient for departing employees | Change to block when HR departure flag is active | Would have prevented Torres Day 1 staging |

### Control Health Check

| Control | Status | Notes |
|---------|--------|-------|
| Email DLP | Operational | Highest volume channel (46.3%). 3 rules active. |
| Endpoint DLP | Operational | USB blocks working as intended. Print monitoring active. |
| Cloud DLP / CASB | Operational | Unsanctioned app uploads blocked (personal Google Drive). |
| Web Filtering | Operational | No policy changes this month. |

### Exception Tracking

| Exception ID | Rule | Requester | Justification | Expiry |
|-------------|------|-----------|---------------|--------|
| EXC-001 | DLP-EP-001 | Finance Director | Quarterly reporting requires USB transfer to auditors | Feb 28, 2025 |

### Recommendations for February
1. Prioritize tuning DLP-EMAIL-001 — highest volume rule, significant FP from Finance.
2. Implement automated HR departure flag → enhanced monitoring correlation for DLP-CLOUD-003.
3. Request CASB block policy for WeTransfer (currently no coverage).
4. Close open investigations from January and track mean time to investigate as new KPI.
5. Schedule quarterly DLP rule review with Finance and HR business unit leads.
