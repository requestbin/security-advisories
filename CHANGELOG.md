# Changelog

## 2026-10-05
- Initial publication: `incidents/2026-10-03-ghost-cve-chain-requestbin-blog/`
  (Ghost CMS CVE-2026-26980 + CVE-2026-29053 exploitation chain, including
  a DB-level backdoor integration that survived a full server rebuild).

## 2026-10-14
- Corrected `2026-10-03-ghost-cve-chain-requestbin-blog`: the follow-on intrusions
  (2026-10-05, 2026-10-12) were not a replayed session cookie as first written, but
  reuse of an un-rotated built-in Admin API key ("Zapier" integration), confirmed from
  Ghost's own `actions` audit table. Added the new IOCs, the audit-first detection
  steps, and the structural mitigations (read-only themes dir, theme-upload denied at
  the proxy).
