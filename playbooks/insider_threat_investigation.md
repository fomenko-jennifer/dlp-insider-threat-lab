# Insider Threat Investigation Playbook
## DLP-Triggered Risk Investigation Procedure

### When to Initiate
- User risk score exceeds xth percentile threshold
- Single Critical-severity event on Restricted data with external destination
- HR referral: employee on PIP, submitted resignation, or under investigation
- Manager reports suspicious behavior

### Step 1: Context Gathering 
- Pull user profile from HR system: role, department, access level
- Check HR status: resignation date? PIP? Recent role change?
- Pull last 30 days of DLP events for this user from Splunk
- Check Cloud Access Security Broker (CASB) logs for shadow IT usage 
- Do NOT alert the user at this stage

### Step 2: Build Behavioral Timeline 
- Export user's events chronologically
- Map events on a timeline: look for spurts and escalation
- Flag deviations from their own baseline:
  - New channels they haven't used before?
  - New destinations (personal cloud, USB) they've never accessed before?
  - Activity at unusual hours?
- Compare to other employees with same department, same role

### Step 3: Technical Analysis 
- What data was involved? Check classification and content patterns
- Where was it going? Map destinations to risk (internal share = low, personal Gmail = high)
- Was there obfuscation? (encrypted zips, renamed file extensions, split files)

### Step 4: Risk Determination

| Level | Criteria | Action |
| False Positive | Legitimate business activity confirmed | Close ticket, update rule exception if pattern repeats |
| Low | Minor policy violation, no malicious intent | Document, user awareness coaching, close |
| Medium | Repeated violations or circumvention attempt | Manager notification, enhanced monitoring (x days), policy review |
| High | Deliberate exfiltration or data staging pattern | Escalate to ITM leadership, preserve evidence, coordinate with HR |
| Critical | Active exfiltration confirmed, legal/regulatory data involved | Immediate escalation: CISO, Legal, HR. Evidence preservation. Potential account suspension |

### Step 5: Documentation & Closure
- Complete investigation ticket with: timeline, evidence, determination, actions taken
- If FP: document what triggered it and consider rule tuning
- If true positive: log in case management, track remediation
- Update monthly metrics: investigation count, outcome distribution, mean time to close tickets

EOF
