# Catalog Repository Validation

## Scope

This file defines validation rules for GitHub repositories that contain Catalog items. These rules ensure repositories follow best practices for maintainability, security, and discoverability.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

GitHub repositories for Catalog items must be properly configured to ensure quality, maintainability, and compliance with Skyline standards.

**Reference**: [GitHub Repository Validation | DataMiner Docs](https://docs.dataminer.services/develop/CICD/Skyline%20Communications/Quality_Assurance/GitHub_Repository_Validation/GitHub_Repository_Validation.html)

---

## License

### License File

**[ERROR]** The repository MUST include a LICENSE file.
- File must be named `LICENSE` (or `LICENSE.txt`, `LICENSE.md`)
- File must be located in the repository root
- License must be valid and appropriate for the content

**[ERROR]** For Skyline Communications repositories:
- Use MIT License or another permissive open-source license
- Ensure copyright holder is correctly identified
- License text must be complete and unmodified

**Example - MIT License**:
```
MIT License

Copyright (c) [year] Skyline Communications

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

---

## Repository Naming

### Naming Conventions

**[ERROR]** Repository names MUST:
- Follow Skyline naming conventions
- Use kebab-case (lowercase with hyphens)
- Be descriptive and meaningful
- Not include redundant prefixes (e.g., avoid "SLC-" for all repos)

**[WARNING]** Repository names SHOULD:
- Match or relate to the Catalog item name
- Be concise but clear
- Avoid abbreviations unless industry-standard

**[INFO]** Common naming patterns:
- Solutions: `SLC-S-[SolutionName]` (e.g., `SLC-S-Ticketing`)
- Connectors: `SLC-C-[Vendor]-[Product]`
- Automation Scripts: `SLC-AS-[ScriptName]`

---

## .gitignore Configuration

### Required Entries

**[ERROR]** The repository MUST include a `.gitignore` file.
- File must be in the repository root
- Must exclude build artifacts
- Must exclude user-specific IDE files

**[ERROR]** The `.gitignore` MUST exclude:
- Build output folders (`bin/`, `obj/`)
- NuGet packages folder (`packages/`)
- User-specific files (`.vs/`, `*.user`, `*.suo`)
- Temporary files

**[WARNING]** The `.gitignore` SHOULD exclude:
- OS-specific files (`.DS_Store`, `Thumbs.db`)
- Log files (`*.log`)
- Local configuration files with sensitive data

**Example - Minimal .gitignore for C# projects**:
```
# Build results
[Bb]in/
[Oo]bj/

# User-specific files
*.user
*.suo
.vs/

# NuGet
packages/
*.nupkg

# Logs
*.log
```

**[INFO]** Consider using GitHub's official .gitignore templates:
- VisualStudio.gitignore for .NET projects
- Add project-specific exclusions as needed

---

## GitHub Topics

### Repository Topics

**[ERROR]** The repository MUST have topics configured.
- Minimum of 3 topics
- Topics must be relevant to the content
- Use lowercase only

**[WARNING]** Topics SHOULD include:
- Technology/vendor names (e.g., `servicenow`, `dataminer`)
- Type of content (e.g., `connector`, `automation`, `solution`)
- Functional category (e.g., `ticketing`, `monitoring`)

**[INFO]** Good topic practices:
- Align topics with manifest tags for consistency
- Use GitHub-standard topics when available (check similar repos)
- Keep topics specific and searchable

**Example Topics**:
```
dataminer
ticketing
servicenow
automation
integration
```

---

## GitHub Actions Workflows

### Required Workflows

**[ERROR]** The repository MUST include CI/CD workflows.
- Workflows must be in `.github/workflows/` folder
- At minimum, a build/validation workflow is required

**[WARNING]** Recommended workflows:
- **Master Workflow**: Build and quality checks on main branch
- **Development Workflow**: Build and test on pull requests
- **Release Workflow**: Automated release creation and deployment

**[INFO]** Workflow best practices:
- Use Skyline's standard workflow templates
- Enable automatic quality checks
- Include artifact generation for releases

**Example - Minimal workflow structure**:
```
.github/
  workflows/
    master_workflow.yml
    development_workflow.yml
```

### Workflow Links and Documentation

**[WARNING]** Repository README SHOULD:
- Include build status badges
- Link to workflow documentation
- Explain CI/CD pipeline

**Example - Status Badge**:
```markdown
![Build Status](https://github.com/SkylineCommunications/repo-name/workflows/Master%20Workflow/badge.svg)
```

---

## Dependabot Configuration

### Dependency Management

**[WARNING]** The repository SHOULD include Dependabot configuration.
- File should be `.github/dependabot.yml`
- Should monitor relevant package ecosystems
- Should have reasonable update schedules

**[INFO]** Dependabot benefits:
- Automatic security updates
- Dependency version management
- Reduced maintenance burden

**Example - Dependabot configuration**:
```yaml
version: 2
updates:
  - package-ecosystem: "nuget"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10
```

**[INFO]** For NuGet-based projects:
- Monitor `nuget` package ecosystem
- Weekly or daily updates recommended
- Limit concurrent PRs to avoid noise

---

## Repository Settings

### General Settings

**[WARNING]** Repository settings SHOULD include:
- Description: Clear one-line description
- Website: Link to documentation or Catalog page
- Issues enabled: For community feedback
- Discussions: Consider enabling for community support

**[INFO]** Additional settings:
- Enable "Automatically delete head branches" for cleaner repo
- Protect main/master branch with required reviews
- Enable security alerts

---

## Branch Protection

### Main Branch Protection

**[WARNING]** The main/master branch SHOULD be protected:
- Require pull request reviews before merging
- Require status checks to pass before merging
- Require branches to be up to date before merging

**[INFO]** Additional protection rules:
- Require linear history
- Require signed commits (for highly sensitive repos)
- Restrict who can push to main branch

---

## Security

### Security Policies

**[WARNING]** The repository SHOULD include:
- `SECURITY.md`: Security policy and vulnerability reporting instructions
- Enabled security alerts
- Enabled Dependabot security updates

**[INFO]** Security best practices:
- Don't commit secrets or API keys
- Use GitHub Secrets for CI/CD credentials
- Regularly review security advisories

---

## Validation Process

When reviewing a GitHub repository:

1. **Check License**: Verify LICENSE file exists and is appropriate
2. **Review Name**: Ensure repository name follows conventions
3. **Validate .gitignore**: Check that build artifacts and IDE files are excluded
4. **Check Topics**: Verify at least 3 relevant topics are configured
5. **Review Workflows**: Ensure CI/CD workflows are present in `.github/workflows/`
6. **Check Dependabot**: Verify Dependabot is configured (if applicable)
7. **Review Settings**: Check description, website link, and feature enablement
8. **Validate Branch Protection**: Ensure main branch has protection rules
9. **Security Review**: Check for security policy and alerts

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| No LICENSE file | ERROR | Add MIT license to repository root |
| Repository name doesn't follow conventions | ERROR | Rename repository using proper pattern |
| Missing .gitignore | ERROR | Add .gitignore with standard exclusions |
| No topics configured | ERROR | Add minimum 3 relevant topics |
| No CI/CD workflows | ERROR | Add workflow files to `.github/workflows/` |
| Dependabot not configured | WARNING | Add `.github/dependabot.yml` |
| No repository description | WARNING | Add clear description in settings |
| Main branch not protected | WARNING | Enable branch protection rules |
| No security policy | WARNING | Add `SECURITY.md` file |
| Build artifacts committed | WARNING | Update .gitignore and remove artifacts |

---

## Output Format

When validating a repository, provide:
- **Compliant items**: Summary of properly configured aspects
- **Non-compliant items**: Detailed list of issues with severity levels
- **Configuration recommendations**: Specific settings to change
- **Next steps**: Prioritized action items to achieve compliance
