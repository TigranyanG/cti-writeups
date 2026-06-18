**TLP:CLEAR**

# Intelligence Assessment — LockBit Ransomware-as-a-Service: Leadership Attribution and Post-Cronos Outlook

**Prepared by:** Grisha Tigranyan
**Date:** June 2026
**Sourcing:** Open-source reporting only — government advisories, law-enforcement releases, and vendor intelligence. This is an analytic synthesis written in finished-intelligence format; it reflects no proprietary or non-public access.

---

## Bottom Line Up Front (BLUF)

LockBit — tracked by CrowdStrike as **BITWISE SPIDER** — was, until early 2024, the most prolific ransomware-as-a-service (RaaS) operation on record. In February 2024, the international **Operation Cronos** task force seized its infrastructure; in May 2024, the US, UK, and Australia publicly attributed the "LockBitSupp" administrator persona to Russian national **Dmitry Yuryevich Khoroshev** and sanctioned him. The operation has since rebuilt under the **LockBit 5.0** brand but at sharply reduced capacity. I assess with **high confidence** that LockBit persists as an active, financially motivated threat, and with **moderate confidence** that sanctions on its leadership will continue to suppress its recovery by deterring ransom payment.

---

## Key Judgments

- **KJ-1 (High confidence).** LockBit is an **eCrime, financially motivated** RaaS operation — *not* a nation-state targeted-intrusion actor. However, its Russia-based leadership and consistent exclusion of victims in Commonwealth of Independent States (CIS) countries indicate tacit operating tolerance within Russia, a recurring marker of Russia-nexus eCrime.
- **KJ-2 (Moderate-to-high confidence).** The "LockBitSupp" administrator persona is Dmitry Khoroshev. Attribution rests on multi-agency law-enforcement analysis of infrastructure seized during Operation Cronos and on blockchain tracing of proceeds. The actor publicly denies the identification; I weight that denial as low-credibility given his clear incentive to deny.
- **KJ-3 (High confidence).** Operation Cronos materially degraded the operation: UK attack volume fell roughly 73%, affiliates defected to rivals (e.g., RansomHub, Qilin), and the interim LockBit 4.0 release (early 2025) failed to gain traction.
- **KJ-4 (Moderate confidence).** LockBit 5.0 ("ChuongDong," announced September 2025) is a genuine rebuild rather than pure brand-jacking, but its return to prior dominance is uncertain. OFAC sanctions on Khoroshev independently suppress affiliate revenue by exposing paying victims to sanctions risk.

---

## Discussion

LockBit emerged in September 2019 (initially "ABCD"), maturing through LockBit 2.0 (2021, which introduced the **StealBit** exfiltration tool and double extortion) and LockBit 3.0 / "Black" (2022). The US Department of Justice assessed 2,000+ victims, more than $500M in ransom proceeds, and billions of dollars in damages; under the RaaS revenue split, Khoroshev allegedly retained roughly a 20% cut, profiting an estimated $100M+.

**Attribution — the analytic centerpiece.** The instructive part of this case is *how anonymity failed*. Khoroshev was confident enough in his operational security to offer a $10M bounty to anyone who could unmask him. Yet the seizure of LockBit's own servers, combined with blockchain tracing of ransom proceeds, supplied the fragments investigators needed — a reminder that an operator's footprint, not the malware itself, is frequently the decisive evidence in attribution. Independently, CrowdStrike Counter Adversary Operations had linked BITWISE SPIDER to the Evil Corp–associated **INDRIK SPIDER** via blockchain and malware analysis as early as October 2022, ahead of the October 2024 law-enforcement confirmation that an Evil Corp member operated a LockBit affiliate account. This sequence demonstrates the value of cross-source correlation — chaining financial, infrastructure, and code indicators — ahead of public confirmation.

**Tradecraft (MITRE ATT&CK).**

| Tactic | Technique | ID |
|---|---|---|
| Initial Access | Exploit Public-Facing Application (incl. Citrix Bleed, CVE-2023-4966) | T1190 |
| Initial Access | Valid Accounts / External Remote Services (RDP, VPN) | T1078 / T1133 |
| Lateral Movement | Remote Services (SMB, RDP) | T1021 |
| Credential Access | OS Credential Dumping | T1003 |
| Defense Evasion | Impair Defenses: Disable or Modify Tools | T1562.001 |
| Exfiltration | Exfiltration via custom tool (StealBit) | T1048 / T1567 |
| Impact | Inhibit System Recovery (shadow-copy deletion) | T1490 |
| Impact | Data Encrypted for Impact | T1486 |

**Diamond Model snapshot.**
- *Adversary:* BITWISE SPIDER — Khoroshev-led core plus a vetted affiliate network.
- *Capability:* LockBit ransomware family (Windows / Linux / ESXi), StealBit exfiltration tool, RaaS control panel and builder.
- *Infrastructure:* dedicated leak site (DLS), Tor-based victim negotiation portals, bulletproof hosting.
- *Victim:* cross-sector big-game-hunting targets; LockBit 5.0 shows a notable tilt toward financial services and South America, diverging from peer groups.

---

## Outlook

LockBit 5.0 adds multi-platform builds, faster encryption, ETW-blinding anti-analysis, randomized 16-character file extensions, and a private-key-gated DLS reflecting tighter OPSEC after the 2024 exposure. I assess with **moderate confidence** that the brand will persist as a mid-tier RaaS through 2026 but is **unlikely to reclaim its former dominance**: sanctions deter payment, trust in LockBit decryptors is damaged (Operation Cronos surfaced faulty keys and unfulfilled deletion promises), and a fragmented market — 85+ active extortion brands observed in Q3 2025, with Qilin and Akira leading — gives affiliates ready alternatives. **Collection priority:** track affiliate migration, infrastructure overlap, and cryptocurrency flows rather than brand names alone, since the brand can outlive — or be reconstituted independently of — its original operators.

---

## Indicators & Further Reading

Representative behavioral indicators (a full IOC set is in the cited CISA advisory): shadow-copy deletion via `vssadmin`; StealBit-associated outbound transfer immediately preceding encryption; randomized 16-character file extensions (5.0). Public financial indicator: OFAC-listed BTC address associated with Khoroshev — `bc1qvhnfknw852ephxyc5hm4q520zmvf9maphetc9z`.

Primary sources: US Treasury / OFAC designation (7 May 2024); UK National Crime Agency, "LockBit leader unmasked and sanctioned"; US DOJ, District of New Jersey, 26-count indictment; CISA et al., "Understanding Ransomware Threat Actors: LockBit" (AA23-165A); CrowdStrike Counter Adversary Operations BITWISE SPIDER profile and reporting.

*Confidence definitions — High: multiple corroborating sources, low ambiguity. Moderate: credible but incompletely corroborated, or plausible alternatives exist. Low: single-source or significant gaps.*
