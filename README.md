# Mediroza General Hospital — Penetration Test Report

Black-box web application penetration test of a simulated hospital web
platform, completed as the Week 4 project for Networkwalks B083.

> ⚠️ **Educational project.** This was carried out against a sandboxed,
> purpose-built training target in a controlled environment, under written
> authorization, strictly for learning purposes. It does not target any
> real hospital, and no real patient, staff, or shareholder data is
> involved or reproduced here.

## Overview

| | |
|---|---|
| **Target** | `medirozahospital.com` (training environment) |
| **Assessment type** | Black-box web application penetration test |
| **Duration** | 5 days |
| **Scope** | Target domain / web infrastructure |
| **Exclusions** | Social engineering, denial-of-service testing |

## Objectives

The engagement followed four milestones:

1. **Initial Access** — find an exposed entry point and reach three
   confidential patient PDF lab reports.
2. **Data Extraction** — recover the contents/passwords of the encrypted
   PDF files.
3. **Critical Data Exposure** — identify exposure of employee salary and
   shareholder data.
4. **Reporting** — document findings, evidence, risk, and remediation.

## Summary of findings

| ID | Finding | Severity |
|----|---------|----------|
| F-01 | SQL injection in patient login → authentication bypass | Critical |
| F-02 | Publicly accessible legacy database backup (`/old/`) | Critical |
| F-03 | Sensitive patient PDF reports exposed after auth bypass | Critical |
| F-04 | Weak password protection on patient PDFs | High |

**Attack chain:** `robots.txt` disclosed a hidden `/old/` path → that path
exposed a legacy SQL database backup → the patient login was found to be
vulnerable to SQL injection, allowing authentication bypass → the bypass
exposed three password-protected patient PDF reports → one PDF's password
was recovered via an online hash-cracking service (not independently
verified locally).

Full methodology, evidence, impact analysis, and remediation guidance for
each finding are in the report.

## Contents
Download the full report:  Mediroza_General_Hospital_Penetration_Test_Report.docx

```
.
├── Mediroza_General_Hospital_Penetration_Test_Report.docx   # full report
└── README.md
```

## Key remediation priorities

- Remove public access to `/old/` and any other legacy/backup paths.
- Fix the SQL injection via parameterized queries / prepared statements.
- Enforce per-document authorization checks on patient records, not just
  at the login layer.
- Replace weak/common PDF passwords with strong, randomly generated
  secrets if document-level encryption is still used.

## Disclaimer

This work was performed only against an authorized training target as
part of a structured learning exercise. Do not use the techniques
described here against any system you do not have explicit written
authorization to test.
