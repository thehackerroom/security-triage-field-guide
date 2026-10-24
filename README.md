# Security Triage Field Guide: Safe URLs and CVSS

A practical checklist for two routine security tasks: inspecting a rewritten email link without opening it, and recording vulnerability severity in a way another analyst can reproduce.

This is an independent field note, not an official CVSS publication or a substitute for incident response procedures. Use the current FIRST documentation as the source of truth for scoring.

## 1. Inspect a rewritten email URL safely

A mail security gateway may wrap or rewrite a destination URL so it can scan the link at delivery time or when clicked. Decoding a wrapper reveals the embedded destination; it does not establish that the destination is benign.

1. Copy the complete wrapped URL as text. Do not click it to see where it goes.
2. Decode it in a browser-based tool. The [Email URL Decoder](https://thehackerroom.com/tools/url-decoder/) handles Microsoft Safe Links, Proofpoint URL Defense, Mimecast and Barracuda formats. Its page says decoding runs in the browser without opening or uploading the URL.
3. Read the resulting hostname carefully. Watch for misspellings, lookalike characters, unexpected subdomains, and URL shorteners. A familiar brand name elsewhere in the URL does not prove that the hostname belongs to that brand.
4. Treat the decoded destination as untrusted. If investigation requires visiting it, use your organization's approved isolated analysis environment and procedures.
5. Preserve the original wrapped URL, decoded destination, message context, and timestamp in the case record. Avoid posting private or tokenized links in public issue trackers or chat rooms.

A decoded URL is an inspection aid, not a verdict. Confirm the sender and business context through a known channel, and do not enter credentials into a page reached from an unexpected message.

## 2. Record a CVSS assessment

CVSS communicates vulnerability severity. It does not, by itself, calculate the risk to a particular organization. Keep the CVSS version and vector with the score so another analyst can understand how the result was produced.

1. Identify the vulnerability and the affected product/version. Record the advisory or evidence used.
2. Choose the CVSS version used by the source or required by your workflow. Do not silently mix versions when comparing scores.
3. Select metrics from the evidence. If an important metric is unknown, document the uncertainty rather than guessing.
4. Save the full vector string, score, version, source, and assessment date. The vector is essential context for reproducing the score.
5. Add local prioritization separately: exposure, reachable attack surface, active exploitation evidence, asset importance, mitigations, and remediation options. These can change operational priority without changing the published CVSS score.

The [CVSS Calculator](https://thehackerroom.com/tools/cvss-calculator/) supports CVSS 4.0 and 3.1 vectors. Check the resulting version and vector before copying it into a ticket or report.

### Metric groups differ by version

- CVSS 3.1 has Base, Temporal, and Environmental metric groups.
- CVSS 4.0 has Base, Threat, Environmental, and Supplemental metric groups. Supplemental metrics provide extra context and do not change the final CVSS score.
- A CVSS Base score represents severity. Prioritization should also use relevant threat intelligence and the affected environment.

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

## Primary references

- [FIRST CVSS 4.0 User Guide](https://www.first.org/cvss/v4.0/user-guide)
- [FIRST CVSS 4.0 Specification](https://www.first.org/cvss/v4.0/specification-document)
- [FIRST CVSS 3.1 Specification](https://www.first.org/cvss/v3-1/specification-document)
- [Microsoft Safe Links overview](https://learn.microsoft.com/en-us/microsoft-365/security/office-365-security/safe-links)

Corrections and practical improvements are welcome. When suggesting changes, include the official reference or reproducible evidence that supports them.
