# Security Advisories & IOC Dataset

Incident writeups, indicators of compromise (IOCs), and defanged malware
samples from security incidents we've directly investigated and
remediated. Published for the benefit of other operators who might be
hit by the same campaign or technique.

This is **evidence from real, remediated incidents**, not original
vulnerability research. CVE numbers referenced here were already
publicly disclosed and patched by the affected vendor before we
published — we're sharing *confirmed real-world exploitation evidence*
(logs, timeline, IOCs, samples), not disclosing a new vulnerability.

## What's in here, what isn't

- ✅ IOCs (IPs, hashes, URLs, file paths, persistence mechanisms) in
  both human-readable (`advisory.md`) and machine-readable
  (`iocs.json` / `iocs.csv`) form.
- ✅ Defanged malware samples (password-protected zip, see each
  incident's `samples/README.md`) with SHA256 checksums.
- ✅ Detection queries/checklists you can run against your own
  infrastructure.
- ❌ **No working exploit payloads.** Where an incident involved
  attacker-crafted exploit code (e.g. an RCE payload), we describe the
  technique and redact the actual payload. We link to the upstream
  CVE record / public PoC repos instead of re-publishing something
  copy-paste weaponizable.

## Index

| Date | Incident | Summary |
|------|----------|---------|
| 2026-10-03 | [`incidents/2026-10-03-ghost-cve-chain-requestbin-blog/`](incidents/2026-10-03-ghost-cve-chain-requestbin-blog/advisory.md) | Ghost CMS CVE-2026-26980 (SQLi) + CVE-2026-29053 (theme-upload RCE) chain, observed in production. Includes a DB-level backdoor that survived a full server rebuild. |

More incidents will be added here as folders under `incidents/` as we
encounter and fully remediate them. Each incident is self-contained —
its own `advisory.md`, `iocs.*`, and `samples/`.

## Using the IOCs

`iocs.json` in each incident folder follows a flat schema:
```json
{
  "type": "ip | domain | url | sha256 | file_path | persistence",
  "value": "...",
  "context": "...",
  "first_seen": "YYYY-MM-DDThh:mm:ssZ"
}
```
Feed straight into a SIEM/threat-intel tool, or just `grep` your own
logs for the `value` fields.

## Handling the samples

Malware samples are zipped with password `infected` (the de facto
convention used by sites like MalwareBazaar) and binaries are not
executable in the archive. **Do not run these outside an isolated,
disposable VM with no network access you care about.** We provide them
for detection-engineering and research purposes only.

## Disclaimer

Everything here reflects what we observed on our own infrastructure.
We make no claim about exhaustiveness (these aren't the only IOCs for
a given campaign, just the ones we captured) and no warranty about
fitness for any particular detection use case. If something here looks
wrong or you have corroborating/contradicting evidence, open an issue.
