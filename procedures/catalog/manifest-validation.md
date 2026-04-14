# Catalog Manifest Validation

## Scope

This file defines validation rules for the `manifest.yml` file in Catalog items. These rules ensure correct representation in the DataMiner Catalog.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

The manifest.yml file is critical for how your Catalog item appears in the DataMiner Catalog. It must contain accurate metadata to help users discover and understand your item.

**Reference**: [Best practices when creating Catalog items | DataMiner Docs](https://docs.dataminer.services/develop/best_practices/Catalog_Items/Best_Practices_When_Creating_Catalog_Items.html)

---

## Validation Rules

### Type Definition

**[ERROR]** The manifest MUST include a valid `type` field.
- Valid types include: `Automation Script`, `Connector`, `Dashboard`, `Solution`, `Standard Solution`, `User-Defined API`, `Visio Drawing`, `Function`, `Package`, etc.
- The type must accurately reflect what the Catalog item is.

**[WARNING]** The type should be specific rather than generic when applicable.
- Example: Use `Standard Solution` instead of generic `Solution` when the item follows standard solution patterns.

---

### Naming Conventions

**[ERROR]** The manifest MUST include a `name` field that:
- Clearly describes the Catalog item's purpose
- Follows title case convention
- Does not include redundant prefixes (e.g., avoid "DataMiner" prefix)
- Is concise but descriptive

**[WARNING]** The name should:
- Be intuitive to users unfamiliar with the solution
- Avoid abbreviations unless they are industry-standard
- Match the repository name where appropriate

**Example - Good**:
```yaml
name: "Ticketing Gateway for ServiceNow"
```

**Example - Bad**:
```yaml
name: "DM_SNTIX_GW"  # Too cryptic
```

---

### Tags and Metadata

**[ERROR]** The manifest MUST include appropriate `tags`.
- Tags must help users discover the item through search
- Include at least 3-5 relevant tags
- Use lowercase for consistency

**[WARNING]** Tags should:
- Include technology/vendor names (e.g., `servicenow`, `azure`, `aws`)
- Include functional categories (e.g., `monitoring`, `ticketing`, `automation`)
- Avoid overly generic tags (e.g., `dataminer`, `script`)

**[INFO]** Consider adding tags for:
- Industry verticals (e.g., `broadcast`, `telecom`)
- Use cases (e.g., `orchestration`, `reporting`)
- Integration types (e.g., `rest-api`, `database`)

**Example**:
```yaml
tags:
  - ticketing
  - servicenow
  - integration
  - automation
  - itsm
```

---

### Owner Configuration

**[ERROR]** The manifest MUST include a valid `owner` field.
- The owner must be a valid GitHub user or organization
- Typically: `SkylineCommunications` for official Catalog items

**[WARNING]** If the owner is an individual user:
- Consider transferring ownership to an organization for better maintainability
- Ensure the user account is active and monitored

**Example**:
```yaml
owner: SkylineCommunications
```

---

### Additional Required Fields

**[ERROR]** The manifest MUST include:
- `description`: A clear, concise description of what the item does (1-2 sentences)
- `repository`: Link to the GitHub repository

**[WARNING]** The manifest SHOULD include:
- `icon`: A recognizable icon for visual identification
- `categories`: Appropriate categorization for filtering

**[INFO]** Consider including:
- `documentation`: Link to detailed documentation
- `support`: Contact information for support requests

---

## Version Information (EXCLUDED FROM VALIDATION)

**[INFO]** Version information in the manifest is NOT validated by this procedure.
- Version validation occurs during GitHub Release creation
- The CI/CD pipeline handles version consistency checks
- Manual validation of version fields is not required

---

## Validation Process

When reviewing a Catalog item manifest:

1. **Check Type**: Verify the type is valid and accurate
2. **Review Name**: Ensure the name is clear, intuitive, and follows conventions
3. **Validate Tags**: Confirm tags are specific, relevant, and sufficient
4. **Verify Owner**: Check owner is valid and appropriate
5. **Check Required Fields**: Ensure description and repository are present
6. **Review Optional Fields**: Note missing optional fields that could improve discoverability

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| Missing type field | ERROR | Add appropriate type based on what the item is |
| Generic or cryptic name | ERROR | Rename to be descriptive and user-friendly |
| Insufficient tags (< 3) | ERROR | Add relevant technology and functional tags |
| Invalid owner | ERROR | Use valid GitHub user/organization |
| Missing description | ERROR | Add 1-2 sentence description of functionality |
| No icon specified | WARNING | Add icon URL for better visual recognition |

---

## Output Format

When validating, provide:
- **Compliant items**: Brief summary of what is configured well
- **Non-compliant items**: Detailed list of required changes with severity levels
- **Improvement suggestions**: Optional enhancements with INFO severity
