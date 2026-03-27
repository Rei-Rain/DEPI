# Implementation Guide
## Cybersecurity Incident Response Framework
**Document Type:** Implementation | **Section:** 5

---

## 1. Source Code Standards

### 1.1 Coding Standards (Python)
```python
# ✅ CORRECT — descriptive names, comments, error handling
def generate_incident_report(incident_id: str, severity: str) -> dict:
    """
    Generates a structured incident report dictionary.
    
    Args:
        incident_id: Unique identifier for the incident
        severity: Severity level (Critical/High/Medium/Low)
    
    Returns:
        dict: Structured incident report
    """
    try:
        report = {
            "id": incident_id,
            "severity": severity.upper(),
            "timestamp": datetime.utcnow().isoformat(),
            "status": "OPEN"
        }
        return report
    except Exception as e:
        logger.error(f"Failed to generate report for {incident_id}: {e}")
        raise

# ❌ WRONG — no comments, bad names, no error handling
def gen(i, s):
    r = {"id": i, "sev": s}
    return r
```

### 1.2 File Naming Conventions
```
Documents:    kebab-case          → incident-response-plan.md
Scripts:      snake_case          → generate_report.py
Classes:      PascalCase          → IncidentReport
Functions:    snake_case          → classify_severity()
Constants:    UPPER_SNAKE_CASE    → MAX_RESPONSE_TIME = 3600
```

### 1.3 Security Coding Practices
- Never hardcode credentials — use environment variables
- Validate all input before processing
- Use parameterized queries for all database operations
- Log errors without exposing sensitive information
- Hash all passwords using bcrypt or Argon2

---

## 2. Version Control & Branching Strategy

### 2.1 GitFlow Branching Model
```
main ──────────────────────────────────────────────────────► (production-ready)
  │
  ├── develop ──────────────────────────────────────────────► (integration branch)
  │       │
  │       ├── feature/week1-research ──► PR ──► develop
  │       ├── feature/week2-ir-plan  ──► PR ──► develop
  │       ├── feature/week3-simulation──► PR ──► develop
  │       └── feature/week4-final    ──► PR ──► develop
  │
  └── hotfix/critical-fix ──────────────────────────────────► PR ──► main
```

### 2.2 Branch Naming
| Branch Type | Format | Example |
|-------------|--------|---------|
| Feature | feature/[description] | feature/week2-ir-plan |
| Bug fix | fix/[description] | fix/readme-formatting |
| Documentation | docs/[description] | docs/literature-review |
| Release | release/[version] | release/v1.0 |

### 2.3 Commit Message Format
```
[TYPE]: Brief description (max 50 chars)

[Optional body — what and why, not how]

Types: feat | fix | docs | test | refactor | style
```

**Examples:**
```
docs: add Week 2 incident response plan

feat: add severity classification matrix to IR plan

fix: correct VLAN numbering in architecture diagram

test: add test cases for containment procedures

docs: complete Week 3 simulation log with timestamps
```

### 2.4 Pull Request Rules
- All PRs require 1 reviewer approval before merge
- PR description must include: what changed, why, how to test
- No direct commits to `main` — always via PR
- Squash merge for feature branches to keep history clean

---

## 3. README — Installation & Setup Guide

### 3.1 Prerequisites
- Git installed
- GitHub account
- Python 3.8+ (for PDF generation scripts)
- Node.js 16+ (for DOCX generation scripts)
- Internet browser (for viewing rendered Markdown on GitHub)

### 3.2 Installation Steps

```bash
# Step 1 — Clone the repository
git clone https://github.com/[username]/DEPI.git
cd DEPI

# Step 2 — Install Python dependencies
pip install reportlab

# Step 3 — Install Node.js dependencies
npm install docx

# Step 4 — Generate all documents (optional)
python3 build-week1-pdf.py
python3 build-week2-pdf.py
python3 build-week3-pdf.py
python3 build-week4-pdf.py
node build-week1-docx.js
```

### 3.3 Repository Structure
```
DEPI/
├── README.md                    ← Start here
├── 1-project-planning/          ← Proposal, Plan, Risk, KPIs, Roles
├── 2-literature-review/         ← Academic review and sources
├── 3-requirements-gathering/    ← Stakeholders, stories, requirements
├── 4-system-analysis-design/    ← All diagrams and design docs
├── 5-implementation/            ← This file + branching strategy
├── 6-testing/                   ← Test plan, cases, bug reports
├── 7-final-presentation/        ← User manual, technical docs
├── week-1-foundation/           ← Week 1 research and network discovery
├── week-2-ir-planning/          ← IR Plan and architecture
├── week-3-simulation/           ← Scenario, simulation log, response docs
├── week-4-final/                ← Final report and presentation notes
└── deliverables/                ← .docx and .pdf versions
```

### 3.4 CI/CD Pipeline (GitHub Actions)

```yaml
# .github/workflows/validate.yml
name: Document Validation

on: [push, pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Check all required files exist
        run: |
          for file in \
            "1-project-planning/project-proposal.md" \
            "2-literature-review/literature-review.md" \
            "3-requirements-gathering/requirements-gathering.md" \
            "4-system-analysis-design/system-analysis-design.md" \
            "6-testing/testing-qa.md" \
            "7-final-presentation/user-manual.md" \
            "deliverables/FINAL-REPORT.docx"; do
            [ -f "$file" ] || (echo "Missing: $file" && exit 1)
          done
          echo "All required files present ✅"
      
      - name: Validate Markdown syntax
        uses: DavidAnson/markdownlint-cli2-action@v11
```
