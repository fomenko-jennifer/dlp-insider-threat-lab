# Data Classification Schema — XYZ Bank

## Tier 1: Public
- **Definition:** Information approved for external release
- **Examples:** Marketing materials, public financial filings, job postings
- **Controls:** No DLP restrictions
- **Access:** All employees, general public

## Tier 2: Internal
- **Definition:** General business information not intended for public release
- **Examples:** Org charts, internal memos, meeting notes, training materials
- **Controls:** DLP alert on external sharing (no block)
- **Access:** All employees

## Tier 3: Confidential
- **Definition:** Sensitive business data that could cause competitive harm if disclosed
- **Examples:** Financial reports (pre-release), strategic plans, vendor contracts, employee performance reviews, source code
- **Controls:** DLP alert + manager notification on external sharing; encrypt if approved
- **Access:** Need-to-know by department/role

## Tier 4: Restricted
- **Definition:** Highly sensitive data subject to regulatory requirements (GLBA, PCI-DSS, SOX)
- **Examples:** Customer SSNs, account numbers, credit card numbers, ACH routing data, audit findings, M&A materials
- **Controls:** DLP block on external sharing; block USB/print; require encryption for any transmission; log all access
- **Access:** Strict need-to-know, principle of least privilege

Every DLP rule maps to a classification tier. The tier determines:
1. What triggers the rule (content patterns)
2. What action to take (alert vs. block vs. encrypt)
3. Who gets notified (user only vs. manager vs. SOC vs. Legal)
4. What exceptions are allowed

EOF
