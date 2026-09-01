# Security Policy: NVIDIA Product Security Repository

NVIDIA is dedicated to the security and trust of our software products and services, including the security bulletin, CSAF, CVE, Markdown, checksum, and index content published in this repository.

If you believe you have found a security issue in this repository's published advisory content, repository automation, generated metadata, links, checksums, or vulnerability disclosure process, please report it privately using the channels below. Do not open a public issue, pull request, or discussion for a potential vulnerability.

## Reporting a Vulnerability

If you discover a potential security vulnerability, please **do not open a public issue.**

* **Web (preferred):** [NVIDIA Vulnerability Disclosure Program](https://www.nvidia.com/en-us/security/)
* **E-Mail:** [psirt@nvidia.com](mailto:psirt@nvidia.com)
  - We encourage you to use the following PGP key for secure email communication:
    [NVIDIA public PGP Key](https://www.nvidia.com/en-us/security/pgp-key)

Please include the following information:

- Product/project name and affected repository path, branch, commit, bulletin, CSAF file, CVE file, or checksum file
- Type of vulnerability or security concern
- Step-by-step reproduction instructions
- Proof-of-concept code or example malformed input, if available
- Security impact, including whether the issue could affect advisory integrity, public vulnerability data, update guidance, researcher acknowledgements, or downstream automation that consumes CSAF/CVE content

Detailed reports help NVIDIA evaluate and address issues faster.

NVIDIA's Product Security Incident Response Team (PSIRT) will acknowledge receipt, validate severity, develop and publish fixes or content corrections as appropriate, and publish security bulletins or repository updates when needed.

## Security Architecture & Context

The NVIDIA Product Security Repository is a public security advisory content repository. It publishes human-readable Markdown security bulletins, machine-readable CSAF 2.0 advisory JSON files, supplementary CVE JSON records, yearly CVE indexes, researcher acknowledgements, and SHA256 checksum files. The top-level `README.md` describes the repository purpose, the year-based bulletin directory structure, and subscriber guidance. Year directories such as `2026/` contain `README.md`, `CVE_index.md`, `Acknowledgments.md`, per-bulletin directories such as `2026/5868/`, and per-bulletin files including `5868.md`, `5868.json`, `CVE-*.json`, and `*.sha256`.

This repository operates primarily as a **data and documentation publication channel** for externally consumed vulnerability information. It is not an application runtime, web service implementation, driver, firmware image, SDK, or library. Repository reconnaissance found Markdown, JSON, CSV, HTML, and SHA256 checksum artifacts, but no application source code, package manifests, network listeners, authentication handlers, database connectors, or dependency manifests.

Its primary security responsibility is to preserve the confidentiality of vulnerability reports until disclosure, the integrity and accuracy of published security bulletin data, and the availability and usability of advisory artifacts for customers, researchers, downstream vulnerability-management tools, and automated CSAF/CVE consumers.

**Repository Exposure Classification:** Not determined.
Basis: visibility could not be confirmed from the provided non-interactive run; document written to public-safe detail.

**Service Exposure Classification:** External / Regulated (high confidence).
Basis: requesting user confirmed this classification; repository publicly distributes NVIDIA security bulletins, CSAF advisories, CVE records, checksums, affected-version data, fixed-version data, CVSS/CWE metadata, researcher acknowledgements, and PSIRT contact guidance for external consumers.

Key security boundaries and interfaces include:

- Public readers consume `README.md`, yearly `README.md` files, `CVE_index.md`, bulletin Markdown files, CSAF JSON files, CVE JSON files, checksum files, CSV files, and HTML artifacts directly from the repository.
- Downstream tools may parse CSAF JSON files such as `2026/5868/5868.json`, CVE JSON files such as `2026/5868/CVE-2026-61750.json`, and yearly indexes such as `2026/CVE_index.md`.
- Human users may follow update guidance and external links embedded in bulletin Markdown and JSON content.
- The repository stores published researcher acknowledgements in files such as `2026/Acknowledgments.md`.
- The repository does not implement runtime access control, authentication, TLS termination, rate limiting, server-side input validation, or API authorization; those controls are assumed to be handled by the hosting platform and NVIDIA's publication workflow before content reaches this repository.

### Threat Model

The following scenarios represent the primary security concerns for this repository and its advisory-publication workflow:

1. **Advisory Integrity Loss in Machine-Readable JSON:** CSAF files such as `2026/5868/5868.json` and CVE files such as `2026/5868/CVE-2026-61750.json` are intended for automated parsing. Incorrect affected-version ranges, fixed-version values, CVSS vectors, CWE identifiers, product identifiers, or vulnerability descriptions could cause customers or scanners to misclassify exposure or miss required updates.

2. **Checksum Mismatch or Stale Artifact References:** Per-bulletin `README.md` files such as `2026/5868/README.md` enumerate Markdown, CSAF, CVE, and `*.sha256` artifacts. If content is updated without corresponding checksum and index updates, downstream consumers may detect integrity failures, cache stale advisory data, or incorrectly trust superseded files.

3. **Unsafe Embedded Markup in Published Bulletin Content:** Bulletin Markdown and CSAF JSON can contain embedded HTML fragments, as shown in files such as `2026/5868/5868.md` and `2026/5868/5868.json`. If publication tooling allows unreviewed markup, consumers that render advisory content in browsers, portals, or dashboards could be exposed to content injection or misleading rendered output.

4. **Premature or Excessive Disclosure in Public Advisory Artifacts:** The repository is externally readable and contains detailed vulnerability metadata, affected products, fixed versions, and acknowledgements. A publication workflow failure could expose embargoed vulnerability information, non-public reporter details, draft advisory content, or overly specific exploitation guidance before coordinated disclosure is complete.

5. **Broken Report Routing or User Guidance:** The top-level `README.md` directs users to NVIDIA Product Security reporting channels, and individual bulletins link to update guidance. Incorrect, stale, or misleading contact and update links could delay vulnerability reporting, cause reporters to disclose issues publicly, or direct customers to the wrong remediation path.

6. **Index and Cross-Reference Drift:** Yearly files such as `2026/README.md`, `2026/CVE_index.md`, and `2026/Acknowledgments.md` duplicate or summarize bulletin, CVE, CVSS, CWE, affected-product, fixed-version, and acknowledgement information. Drift between these generated indexes and source bulletin artifacts could reduce trust in the repository and cause automated consumers to use incomplete or inconsistent data.

### Critical Security Assumptions

- Publication workflow review prevents embargoed or non-public information from being committed to the public repository.
- The repository hosting platform enforces authentication, authorization, branch protection, audit logging, TLS, vulnerability-report privacy, and access controls for maintainers and private vulnerability reports.
- Generated Markdown, CSAF JSON, CVE JSON, indexes, acknowledgements, and SHA256 files are produced from authoritative advisory data and reviewed before publication.
- Checksums are regenerated whenever corresponding Markdown, CSAF, CVE, CSV, or HTML artifacts change.
- Consumers validate advisory data according to CSAF, CVE, CVSS, CWE, and Markdown parsing expectations rather than treating repository content as executable code.
- Embedded HTML and links in bulletin content are assumed to be sanitized or reviewed by the publication process before release.
- Product names, affected-version ranges, fixed-version ranges, researcher acknowledgements, and vulnerability descriptions are assumed to be approved for public disclosure before they are published in this repository.
- The repository itself does not protect customers from vulnerable product versions; it assumes customers and automated tools consume the published data and apply recommended updates.

## Supported Versions and Security Update Process

This repository publishes NVIDIA security bulletin content rather than a versioned software package. Supported product versions, affected versions, and fixed versions are documented in the relevant bulletin Markdown, CSAF JSON, CVE JSON, and yearly CVE index entries.

Security updates to this repository may include new bulletins, revised bulletins, corrected CVE metadata, regenerated checksums, updated acknowledgements, or corrected links. Consumers should monitor this repository or subscribe through the NVIDIA Product Security page for new or revised advisories.

## Scope

Security issues in scope for this repository include:

- Incorrect or tampered CSAF, CVE, Markdown, CSV, HTML, index, acknowledgement, or checksum content
- Broken or misleading vulnerability-reporting instructions
- Integrity failures between advisory files and their checksum files
- Public disclosure of non-public vulnerability details through repository content
- Unsafe markup or links in published advisory files
- Inconsistencies that materially affect vulnerability management, remediation guidance, or automated security tooling

Security issues in NVIDIA products referenced by this repository should still be reported through the NVIDIA Vulnerability Disclosure Program or PSIRT email rather than public repository issues.

## Dependency Security

Repository reconnaissance did not identify package manifests such as `package.json`, `go.mod`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, or similar build files. The repository primarily contains static advisory artifacts. Dependency risk is therefore concentrated in the external generation, review, and publication tooling used before artifacts are committed, and in downstream consumers that parse the published files.

## Operational Guidance for Consumers

Consumers that automate against this repository should:

- Prefer machine-readable CSAF and CVE JSON artifacts where possible.
- Verify checksum files when relying on local mirrors or cached advisory artifacts.
- Treat Markdown and embedded HTML as untrusted display content when rendering in downstream systems.
- Monitor revised bulletins and yearly indexes for corrected affected-version or fixed-version information.
- Report suspected advisory integrity issues privately through NVIDIA Product Security channels.
