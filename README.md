BibTeX Reference Checker

Overview

`bib-checker` is a skill for verifying the authenticity and correctness of references in `.bib` files. It uses web lookups (DOI resolver, DBLP, Semantic Scholar, Google Scholar, arXiv, etc.) to confirm whether a cited paper exists and whether its metadata (authors, year, venue, DOI) is accurate. It can also suggest replacing arXiv preprints with published versions when available.

Key features

- Verify whether each BibTeX entry corresponds to a real publication
- Cross-check authors, year, venue, and DOI fields
- Detect arXiv preprints that have been published and suggest updates
- Flag entries that cannot be verified and require manual review

Installation

Install the skill using the skills installer (example):

```
npx skills add https://github.com/anthropics/skills --skill bib-checker
```

Verification priority (recommended order)

1. DOI (resolve first if present)
2. DBLP (authoritative for computer science)
3. Semantic Scholar
4. Google Scholar
5. arXiv

Sample output

```
=== BibTeX Verification Report ===

[✓] smith2023: "Deep Learning Methods" - Verified (NeurIPS 2023)

[!] jones2024: "Neural Networks Study"
    Issue: arXiv preprint has been published
    Suggested fix: update to @inproceedings with booktitle = {ICML}

[✗] fake2023: "Amazing Results Paper"
    Issue: title not found in any databases; needs manual verification

Summary: Total entries: 25, Verified: 20, Needs update: 3, Suspicious: 2
```

Notes and limitations

- Network access is required for automatic verification; without network the tool can only perform local consistency checks
- Some workshop or non-English venues may not be fully indexed by the queried databases and may require manual checks

Interactive fixes

In interactive mode this skill shows the current entry, authoritative data found online, and a proposed diff. After user confirmation the skill can write corrections back to the `.bib` file or produce a patch for review.