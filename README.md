# Security Triage Field Guide: URLs, CVSS, NIS2, and KEV

A practical checklist for four recurring security tasks: inspecting rewritten email links, scoring vulnerability severity, screening an organisation against NIS2 scope, and checking CISA's Known Exploited Vulnerabilities catalog.

This is an independent field note, not legal advice or an official CVSS publication. Use the relevant standards, regulator, and primary sources as the authority for decisions.

## 1. Inspect a rewritten email URL safely

A mail security gateway may wrap or rewrite a destination URL so it can scan the link at delivery time or when clicked. Decoding a wrapper reveals the embedded destination; it does not establish that the destination is benign.

1. Copy the complete wrapped URL as text. Do not click it to see where it goes.
2. Decode it in a browser-based tool. The [Email URL Decoder](https://thehackerroom.com/tools/url-decoder/) supports Microsoft Safe Links, Proofpoint URL Defense, Mimecast, Barracuda, and Cisco Secure Email links. It can also inspect pasted email text. The page says decoding runs in your browser without opening or uploading the content.
3. Read the resulting hostname carefully. Watch for misspellings, lookalike characters, unexpected subdomains, and URL shorteners. A familiar brand name elsewhere in the URL does not prove that the hostname belongs to that brand.
4. Treat the decoded destination as untrusted. If investigation requires visiting it, use your organisation's approved isolated analysis environment and procedures.
5. Preserve the original wrapped URL, decoded destination, message context, and timestamp in the case record. Avoid posting private or tokenised links in public issue trackers or chat rooms.

A decoded URL is an inspection aid, not a verdict. Confirm the sender and business context through a known channel, and do not enter credentials into a page reached from an unexpected message.

## 2. Record a CVSS assessment

CVSS communicates vulnerability severity. It does not, by itself, calculate the risk to a particular organisation. Keep the CVSS version and vector with the score so another analyst can understand how the result was produced.

1. Identify the vulnerability and affected product/version. Record the advisory or evidence used.
2. Choose the CVSS version used by the source or required by your workflow. Do not silently mix versions when comparing scores.
3. Select metrics from the evidence. If an important metric is unknown, document the uncertainty rather than guessing.
4. Save the full vector string, score, version, source, and assessment date. The vector is essential context for reproducing the score.
5. Add local prioritisation separately: exposure, reachable attack surface, active exploitation evidence, asset importance, mitigations, and remediation options. These can change operational priority without changing the published CVSS score.

The [CVSS Calculator](https://thehackerroom.com/tools/cvss-calculator/) supports CVSS 4.0 and 3.1. It can set metrics, accept a vector, or look up a CVE for its NVD vector, KEV status, and EPSS score. Check the resulting version and vector before copying them into a ticket or report.

### Metric groups differ by version

- CVSS 3.1 has Base, Temporal, and Environmental metric groups.
- CVSS 4.0 has Base, Threat, Environmental, and Supplemental metric groups. Supplemental metrics provide extra context and do not change the final score.
- A CVSS Base score represents severity. Prioritisation should also use relevant threat intelligence and the affected environment.

### Minimal assessment record

- Vulnerability or advisory:
- Affected asset and version:
- CVSS version:
- Score and full vector:
- Scoring source and date:
- Evidence or assumptions:
- Local exposure and exploitation context:
- Mitigations and remediation owner:
- Review date:

## 3. Screen an organisation for NIS2 scope

The [NIS2 Scope Checker](https://thehackerroom.com/tools/nis2-scope-checker/) walks through jurisdiction, activity/sector, organisation size, and specified exceptions, and shows which rule determined its screening result. The page says the answers stay in the browser and are not uploaded.

Use it as an initial screen. It cannot account for every national implementation, group structure, or sector-specific edge case. Confirm a borderline or consequential result against the applicable national law and regulator guidance, and seek qualified legal advice where needed. The checker itself says it is not legal advice.

## 4. Check the CISA Known Exploited Vulnerabilities catalog

The [CISA KEV Tracker](https://thehackerroom.com/tools/kev-tracker/) searches catalog entries by CVE, vendor, or product and can filter for recent additions or entries associated with ransomware use. Use KEV presence as an actionable signal in vulnerability triage, then check the original CISA entry, affected-version details, and remediation guidance.

A CVE not appearing in KEV does not prove it has never been exploited or that it is safe to defer. Combine the catalog with asset exposure, vendor advisories, threat intelligence, and local impact. The site links each CVE to its NVD record and the CVSS calculator.

## Primary references

- [FIRST CVSS 4.0 User Guide](https://www.first.org/cvss/v4.0/user-guide)
- [FIRST CVSS 4.0 Specification](https://www.first.org/cvss/v4.0/specification-document)
- [FIRST CVSS 3.1 Specification](https://www.first.org/cvss/v3-1/specification-document)
- [Microsoft Safe Links overview](https://learn.microsoft.com/en-us/microsoft-365/security/office-365-security/safe-links)
- [CISA Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
- [NIS2 Directive (EU) 2022/2555](https://eur-lex.europa.eu/eli/dir/2022/2555/oj)

Corrections and practical improvements are welcome. When suggesting changes, include an official reference or reproducible evidence that supports them.
