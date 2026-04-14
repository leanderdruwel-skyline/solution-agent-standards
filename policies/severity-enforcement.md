# Severity Enforcement Guide

## Purpose

This document defines how agents should interpret and enforce the severity levels used throughout the instruction files in this repository.

---

## Severity Levels

### **[ERROR]** — Pipeline Blocking

- **Behavior**: Agent must report the violation and **block** the pipeline/workflow from continuing
- **Exit Code**: Non-zero (e.g., exit code 1)
- **Use Cases**:
  - Critical naming conventions (e.g., `SOL-` prefix requirement)
  - Mandatory architectural patterns (e.g., explicit contracts at boundaries)
  - Security requirements (e.g., no secrets in code)
  - Breaking changes to public APIs without proper versioning

**Example Error Output**:
```
[ERROR] Naming violation detected in solution-naming.md
- File 'Files/MyFile.xml' does not start with 'SOL-' prefix
- Required: All files in Files folder must start with 'SOL-'
Pipeline execution blocked. Fix this error to proceed.
```

### **[WARNING]** — Should Fix (Non-Blocking)

- **Behavior**: Agent reports the violation but **allows** the pipeline to continue
- **Exit Code**: Zero (success with warnings)
- **Use Cases**:
  - Best practices that improve code quality but aren't critical
  - Design patterns that should be followed but have valid exceptions
  - Code organization and maintainability guidelines

**Example Warning Output**:
```
[WARNING] Architecture guideline violation detected in solution-architecture.md
- Component 'DataProcessor' mixes data ingestion and business logic
- Recommendation: Separate concerns into distinct components
Pipeline continues, but please address this warning.
```

### **[INFO]** — Informational (No Enforcement)

- **Behavior**: Agent may log the information for context but takes no enforcement action
- **Exit Code**: Zero (success)
- **Use Cases**:
  - General recommendations
  - Optional optimizations
  - Informational best practices

---

## Implementation Guidelines for Agents

### Parsing Instructions

1. Read the relevant `.md` files from the `procedures/` folder
2. Extract rules that contain severity tags: `[ERROR]`, `[WARNING]`, or `[INFO]`
3. If no tag is present, default to `[WARNING]`

### Validation Flow

```
For each instruction with severity tag:
  1. Check if the rule is violated in the target repository
  2. If violated:
     - [ERROR]: Log error + exit with non-zero code
     - [WARNING]: Log warning + continue
     - [INFO]: Log info (optional) + continue
  3. Continue to next rule

After all rules checked:
  - If any [ERROR] was found: Exit 1
  - If only [WARNING] or [INFO] found: Exit 0
```

### Example Agent Implementation

```python
import re
import sys

def parse_severity_rules(md_file):
    """Extract rules with severity tags from markdown file"""
    rules = []
    with open(md_file, 'r') as f:
        for line in f:
            match = re.search(r'\*\*\[(ERROR|WARNING|INFO)\]\*\*\s+(.*)', line)
            if match:
                rules.append({
                    'severity': match.group(1),
                    'rule': match.group(2)
                })
    return rules

def validate_and_enforce(rules, target_repo):
    """Validate rules and enforce based on severity"""
    has_errors = False
    
    for rule in rules:
        violation = check_rule_violation(rule, target_repo)
        
        if violation:
            if rule['severity'] == 'ERROR':
                print(f"[ERROR] {violation}")
                has_errors = True
            elif rule['severity'] == 'WARNING':
                print(f"[WARNING] {violation}")
            elif rule['severity'] == 'INFO':
                print(f"[INFO] {violation}")
    
    return 1 if has_errors else 0

# Usage in CI/CD pipeline
exit_code = validate_and_enforce(rules, target_repo)
sys.exit(exit_code)
```

---

## CI/CD Integration

### GitHub Actions Example

```yaml
name: Validate Solution Standards

on: [push, pull_request]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Checkout Standards Repository
        uses: actions/checkout@v3
        with:
          repository: leanderdruwel-skyline/solution-agent-standards
          path: .standards
      
      - name: Run Validation Agent
        run: |
          python .standards/validators/validate_standards.py
        continue-on-error: false  # Pipeline fails on [ERROR]
      
      - name: Upload Validation Report
        if: always()
        uses: actions/upload-artifact@v3
        with:
          name: validation-report
          path: validation-report.txt
```

### Azure DevOps Example

```yaml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

steps:
- checkout: self
- checkout: git://solution-agent-standards

- script: |
    python solution-agent-standards/validators/validate_standards.py
  displayName: 'Validate Solution Standards'
  failOnStderr: false
  
- task: PublishBuildArtifacts@1
  condition: always()
  inputs:
    PathtoPublish: 'validation-report.txt'
    ArtifactName: 'validation-report'
```

---

## Updating Severity Levels

When adding or modifying rules in any procedure file:

1. Choose the appropriate severity level based on impact:
   - **[ERROR]**: Violation causes breaking changes, security issues, or critical failures
   - **[WARNING]**: Violation degrades quality, maintainability, or team standards
   - **[INFO]**: Guideline for best practices without enforcement

2. Add the tag at the start of the rule description:
   ```markdown
   - **[ERROR]** This is a critical rule that blocks the pipeline
   - **[WARNING]** This is an important guideline that should be followed
   - **[INFO]** This is a helpful suggestion
   ```

3. Be conservative: Use `[ERROR]` sparingly, only for rules that genuinely should stop deployment

---

## Migration Path

For repositories currently referencing these standards without severity awareness:

1. **Phase 1** (Current): All existing rules default to `[WARNING]`
2. **Phase 2**: Add severity tags to critical rules (`[ERROR]` for must-fix items)
3. **Phase 3**: Enable enforcement in CI/CD pipelines
4. **Phase 4**: Gradually promote important warnings to errors as teams adopt standards

