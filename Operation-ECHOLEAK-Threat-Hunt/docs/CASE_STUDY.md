# Operation ECHOLEAK — Investigation report

**Simulation | Microsoft Defender Advanced Hunting | Completed October 19, 2026**

## 1. Initial access

My investigation identified the sender `quarterly.reports@globalfinancereview.net`, attached document `Q3-2026-Global-Markets-Review.docx`, and a delay of **1 hour 27 minutes** between delivery and first document access. The submitted exercise describes the report as containing hidden white-on-white and zero-point prompt injection text.

## 2. Copilot hijack

Emily's authorized prompt was **"Summarise the key findings of this quarterly report."** The audit trail showed unexpected `Graph.SearchFiles` and `Graph.ReadFile` calls against `site:cormorantcapital.sharepoint.com` and unrelated sensitive materials. My exercise classification was indirect prompt injection (`AML.T0051`).

## 3. Collection and output

The initial phase accessed **five** previously unopened sensitive files in approximately six seconds. In `CopilotAudit_CL`, the `CopilotResponse` field included markdown images whose URLs pointed to `metrics-cdn.analyticshub.io`. The image URL query parameters carried encoded data. This demonstrates the response artifact, but does not independently prove complete server-side receipt.

## 4. Blast radius

The initial five files documented in my report were:

1. `Board Meeting Minutes - October 2026.docx`
2. `Project Falcon - M&A Target Assessment.xlsx`
3. `Salary Review FY2027 - Executive Summary.pdf`
4. `Client Portfolio - Henderson Family Office.xlsx`
5. `Copilot System Configuration - Cormorant.json`

The exercise also described exposure of the Copilot system prompt and enterprise configuration. I identified the limitation that Office activity logs capture **access**, not the full text of the accessed files; response URL records alone cannot guarantee an exact inventory of what was received externally.

## 5. Normal versus anomalous

I compared the suspicious session to the provided normal Copilot activity. The normal summarization sessions had prompt and response events without unrelated Graph file search/read calls. The anomalous session instead showed:
- Unrequested `Graph.SearchFiles` and `Graph.ReadFile` calls.
- Previously unopened, unrelated sensitive files.
- Five accesses in approximately six seconds.
- External image URLs embedded in responses.

**Conclusion:** The pattern, rather than file access alone, made this activity anomalous.

## 6. Expanded search and classification

The later **SearchLeak** phase used keywords `confidential`, `restricted`, `board`, `acquisition`, and `salary`, accessing **eight additional files**. The reported total was **13 sensitive files**.

My final classification was **external input manipulation**, not an account or Copilot configuration compromise. The exercise explanation says sign-in activity was consistent with Emily's normal authentication and the configuration was exposed rather than edited. I have not independently reproduced those sign-in checks in this published package.

## Investigation boundaries

This is a **simulated hunt**. The screenshots and original notes support the observed Graph activity, sensitive file access, and suspicious response URLs. The exact content received at the remote server, independent browser request telemetry, and any actual remediation are **not verified** here.

[← Project overview](../README.md)