## SPL Queries for Detection
----------------------------------------------------------
## Query 1: Morning Operational Check
**Purpose:** First thing an analyst runs each morning to see what occurred the night before.
```
index=dlp | stats count by channel, severity | sort - count
```
**What I learned:**

In all channels, cloud, endpoint and email, severity varies. Medium severity emails have the highest rate of occurance in this scenario. Fine-tuning the ruleset will lead to a more accurate understanding of current threats.
---

## Query 2: User Activity Summary
**Purpose:** Identify who is generating the most DLP events.
```
index=dlp | stats count as event_count, dc(channel) as channels_used, dc(rule_id) as rules_triggered, values(severity) as severities by user_id, user_name, department | sort - event_count
```
**What I learned:**
We know that Maria often will send and recieve PII as relates to her Finance role within the company. It is suspicious, however, that Jake Torres has a high event count and high severity within those events. Due to his recent resignation we should investigate this matter futher.

-----------------------------------------------------------------

## Query 3: After-Hours Data Movement
**Purpose:** Data transfer after work hours of 08:00 to 18:00, not the best sign.
```
index=dlp business_hours=false | stats count, values(channel) as channels, values(destination) as destinations, sum(file_size_mb) as total_mb by user_id, user_name | where count > 1 | sort - count
```
**What I learned:**
Jake Torres is the only user who is consistently moving data after work hours. He is also hoppingbetween multiple channels and sending data to an unauthorized removable media (USB) and local drive. 

----------------------------------------------------------------

## Query 4: Restricted Data to External Destinations
**Purpose:** Highest-priority alert combination, sensitive data going external.
```
index=dlp classification="Restricted" (destination="external_email" OR destination="personal_cloud" OR destination="usb_drive") | table timestamp, user_id, user_name, department, channel, destination, file_type, file_size_mb, action_taken | sort timestamp
```
**What I learned:**
Restricted data may be sent to external partners or third-parties, it is essential to recognize that business needs have to work in tandem with security needs. We alert on most of these events and block a few.

-----------------------------------------------------------------

## Query 5: False Positive Rate by Rule
**Purpose:** Weekly tuning review: how can we reduce noise?
```
index=dlp | stats count as total, count(eval(investigation_status="closed")) as resolved by rule_id | eval closure_rate = round(resolved/total * 100, 1) | sort - total
```
**What I learned:**
Email alerts generate the most noise in this scenario. Out of 14 total alerts for DLP Rule DLP-EMAIL-001, 12 were closed. We should correlate information about closure rate with reason for closure to create a better metric for the purpose of improving our ruleset.

---

## Query 6: Jake Torres Investigation Timeline
**Purpose:** Pull all events for a specific user under investigation.
```
index=dlp user_id="USR-007" | sort timestamp | table timestamp, channel, rule_id, severity, classification, destination, file_type, file_size_mb, action_taken, business_hours
```
**What I learned:**

Over the course of three days, the actions of Jake Torres became more brazen. On Jan. 15 he sent a 8.2 mb confidential .xlsx file from the cloud to his local_drive. The next day he attempts to send the same file to a USB drive but was blocked. From there he began to test other channels, even encrypting files before transit, but was not successful.  

-----------------------------------------------------------------

## Query 7: Privileged User Monitoring
**Purpose:** Separate signal for users with elevated access.
```
index=dlp privileged=true | stats count as events, dc(channel) as channels, values(classification) as data_touched, values(destination) as destinations by user_id, user_name, department | sort - events
```
**What I learned:**
In this scenario we see that privileged users are all in the IT department. These users operate on various channels, with various forms of classified data and a multitude of destinations. Although we expect IT users to engage in higher-risk behavior, we don't want to overlook these events. We should operate under notions of Zero Trust given we may not be aware of user compromise or an insider threat.

-----------------------------------------------------------------

## Query 8: Monthly Metrics Summary
**Purpose:** Numbers that go into the monthly governance report.
```
index=dlp | stats count as total_events, dc(user_id) as unique_users, count(eval(severity="Critical")) as critical, count(eval(severity="High")) as high, count(eval(severity="Medium")) as medium, count(eval(severity="Low")) as low, count(eval(action_taken="block")) as blocked | eval block_rate = round(blocked/total_events * 100, 1)
```
**What I learned:**
There are 41 events, 13 unique users, and a low block rate of 22.0% in this scenario.

-----------------------------------------------------------------

## Top 3 Queries I Would Put on a Daily Dashboard
1. Query 1
2. Query 4
3. Query 7


EOF
