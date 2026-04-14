# Catalog Documentation Validation

## Scope

This file defines validation rules for documentation in Catalog items, with specific focus on the README in the `CatalogInformation` folder.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

Proper documentation is essential for users to understand and effectively use Catalog items. The `CatalogInformation` folder contains documentation specifically for the Catalog, distinct from repository or project READMEs.

**Reference**: [Best practices when documenting Catalog items | DataMiner Docs](https://docs.dataminer.services/develop/best_practices/Catalog_Items/Best_Practices_When_Documenting_Catalog_Items.html)

---

## CatalogInformation README

### Purpose and Scope

**[ERROR]** The `CatalogInformation` folder MUST contain a README file.
- This README is specifically for Catalog item documentation
- It is displayed on the Catalog item's page in docs.dataminer.services
- It is distinct from repository README (which is about the repo itself) and project READMEs (which are about individual components)

**[INFO]** Understanding the distinction:
- **CatalogInformation/README**: What the Catalog item does and how to use it
- **Repository README**: How to work with the repository (development, contribution)
- **Project READMEs**: Technical details about specific projects/components

---

### Required Content

**[ERROR]** The CatalogInformation README MUST include:

1. **Overview Section**
   - Clear description of what the Catalog item is
   - Primary purpose and use cases
   - Target audience

2. **Features Section**
   - Key capabilities
   - Main functionalities
   - What problems it solves

3. **Installation/Deployment Section**
   - How to install or deploy the item
   - Prerequisites
   - Step-by-step instructions

4. **Usage Section**
   - How to use the item after installation
   - Common scenarios
   - Configuration options

**[WARNING]** The CatalogInformation README SHOULD include:

1. **Prerequisites Section**
   - Required DataMiner version
   - Required connectors or dependencies
   - Licensing requirements

2. **Configuration Section**
   - Configuration parameters
   - Settings and options
   - Customization possibilities

3. **Examples Section**
   - Practical use case examples
   - Screenshots or diagrams
   - Sample configurations

**[INFO]** Consider including:
- Troubleshooting section
- FAQ section
- Links to additional resources
- Known limitations

---

### Content Quality Standards

**[ERROR]** Documentation MUST be:
- **Accurate**: Information must be correct and up-to-date
- **Complete**: All essential information must be present
- **Clear**: Written in clear, understandable language

**[WARNING]** Documentation SHOULD:
- Use proper markdown formatting
- Include visual aids (screenshots, diagrams) where helpful
- Be organized with clear headings
- Use code blocks for examples

**[INFO]** Best practices:
- Write for your target audience (avoid overly technical jargon when not needed)
- Use numbered lists for sequential steps
- Use bullet points for non-sequential items
- Include links to related documentation

---

### Structure and Organization

**[ERROR]** The README MUST:
- Start with a clear title
- Use proper heading hierarchy (H1 for title, H2 for sections, etc.)
- Be logically organized

**[WARNING]** The README SHOULD:
- Include a table of contents for longer documents (> 5 sections)
- Group related information together
- Use horizontal rules to separate major sections

**Example Structure**:
```markdown
# [Catalog Item Name]

## Overview
[What it is and why it exists]

## Features
- Feature 1
- Feature 2

## Prerequisites
- DataMiner version X.X.X or higher
- Required connectors

## Installation
1. Step 1
2. Step 2

## Configuration
[Configuration details]

## Usage
[How to use the item]

## Examples
### Example 1: [Scenario]
[Details]

## Troubleshooting
[Common issues and solutions]
```

---

### Visual Content

**[WARNING]** Documentation SHOULD include:
- Screenshots for UI-based components
- Architecture diagrams for complex solutions
- Workflow diagrams for processes

**[INFO]** When including images:
- Store images in an appropriate subfolder (e.g., `CatalogInformation/images/`)
- Use descriptive file names
- Include alt text for accessibility
- Optimize image sizes for web viewing

---

### Code Examples

**[WARNING]** When including code examples:
- Use proper syntax highlighting (specify language in code blocks)
- Ensure code is functional and tested
- Include comments for complex code
- Provide context for code snippets

**Example**:
````markdown
```csharp
// Initialize the connector
var connector = new ServiceNowConnector(apiUrl, apiKey);
await connector.ConnectAsync();
```
````

---

## Documentation Maintenance

**[WARNING]** Documentation SHOULD be:
- Updated when functionality changes
- Reviewed for accuracy with each release
- Versioned along with the Catalog item

**[INFO]** Consider:
- Adding a "Last Updated" date
- Including version compatibility information
- Noting deprecated features

---

## Multi-Language Support

**[INFO]** For international audiences:
- Primary documentation should be in English
- Consider providing translations for major languages
- Use clear, simple English that translates well

---

## Validation Process

When reviewing Catalog documentation:

1. **Check Existence**: Verify `CatalogInformation/README.md` exists
2. **Review Required Sections**: Confirm all ERROR-level sections are present
3. **Assess Content Quality**: Check for accuracy, clarity, and completeness
4. **Validate Structure**: Ensure logical organization and proper markdown
5. **Check Visual Content**: Verify images and diagrams are present and useful
6. **Test Code Examples**: Ensure code snippets are accurate and functional
7. **Verify Links**: Check that all links are valid and working

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| CatalogInformation README missing | ERROR | Create README with required sections |
| No overview/description | ERROR | Add clear overview explaining the item |
| Missing installation instructions | ERROR | Add step-by-step installation guide |
| No usage examples | WARNING | Add practical usage scenarios |
| Broken images or links | WARNING | Fix or remove broken references |
| Poor markdown formatting | WARNING | Apply proper markdown syntax |
| Outdated information | WARNING | Update to reflect current functionality |
| No visual aids | INFO | Consider adding screenshots/diagrams |

---

## Output Format

When validating documentation, provide:
- **Compliant items**: Summary of well-documented sections
- **Non-compliant items**: Detailed list of missing or inadequate sections with severity
- **Improvement suggestions**: Optional enhancements (INFO level)
- **Examples**: Specific suggestions for improvement where applicable
