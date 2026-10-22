# Evidence provenance and accuracy

This project is based on the analyst's original uploaded `EchoLeak_Report.odt`, 16 screenshots from Microsoft Defender advanced hunting, and the completed investigation answers supplied for Operation ECHOLEAK.

- **Observed in the supplied evidence:** message/attachment metadata, Copilot prompt, Graph file tools, search terms, sensitivity labels, and Copilot response URLs.
- **Exercise findings:** hidden document instructions, broader sign-in checks, and named exploit stages (CoSnitch and SearchLeak).
- **Not established:** complete exported plaintext, independently observed external HTTP receipt, production incident response, or a deployed detection.
- **Timestamp handling:** the exercise used September 20, 2026 event timestamps and local screenshot times. The email was received at 09:15:22 UTC and the first file access was 10:42:08 UTC, approximately 87 minutes apart.
- **Draft discrepancy:** the original ODT note spells the sender's domain differently than the accepted answer. This project uses `globalfinancereview.net` from the accepted answer; the uploaded source remains unaltered in the downloadable project archive.
- **KQL provenance:** companion KQL is transcribed/adapted from screenshot-visible filters; no query execution was performed to create this repository content.

The full **16-image evidence gallery**, source ODT, and additional explanatory files are available in the accompanying downloadable zip. The images have not been added to this GitHub folder.