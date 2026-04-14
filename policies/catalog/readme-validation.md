# Catalog README Validation

## Scope

This file defines validation rules for README files in repositories and projects. These READMEs are distinct from the CatalogInformation README and serve different purposes.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

README files serve as the primary documentation entry point for repositories and individual projects. It's important to distinguish between different types of READMEs:

- **Repository README**: Located at repository root, describes the repository itself
- **Project READMEs**: Located in project folders, describe individual components
- **CatalogInformation README**: Located in `CatalogInformation/` folder, describes the Catalog item (see [documentation-validation.md](documentation-validation.md))

**Reference**: [Adding a README file | DataMiner Docs](https://docs.dataminer.services/develop/CICD/Skyline%20Communications/Quality_Assurance/GitHub_Repository_Validation/README.html)

---

## Repository README

### Purpose

The repository README is for developers and contributors who want to understand:
- What the repository contains
- How to work with the repository
- How to contribute
- How to build and develop

**[ERROR]** Every repository MUST have a README.md file in the root directory.

---

### Required Content - Repository README

**[ERROR]** The repository README MUST include:

1. **Title and Description**
   - Clear title matching the repository name
   - Brief description of what the repository contains
   - Badge(s) showing build status

2. **Repository Contents**
   - Overview of what's in the repository
   - Explanation of folder structure
   - Description of key components or projects

3. **Getting Started**
   - Prerequisites for development
   - How to clone and set up the repository
   - How to build the solution

**[WARNING]** The repository README SHOULD include:

1. **Development Guidelines**
   - Code style guidelines or link to style guide
   - Testing requirements
   - Commit message conventions

2. **Contributing**
   - How to contribute to the repository
   - Pull request process
   - Link to CONTRIBUTING.md if it exists

3. **Links**
   - Link to Catalog item (if applicable)
   - Link to detailed documentation
   - Link to issue tracker

**[INFO]** Consider including:
- Project status or roadmap
- Contact information
- Acknowledgments or credits

---

### Repository README Structure

**Example - Repository README**:
```markdown
# SLC-S-Ticketing

![Build Status](https://github.com/SkylineCommunications/SLC-S-Ticketing/workflows/Master%20Workflow/badge.svg)

## Overview

This repository contains the Ticketing Standard Solution for DataMiner, providing integration with various ITSM platforms.

## Contents

- **TicketingGateway**: Core automation script for ticket routing
- **ServiceNowConnector**: Connector for ServiceNow integration
- **JiraConnector**: Connector for Jira integration
- **CatalogInformation**: Documentation for the Catalog item

## Getting Started

### Prerequisites

- Visual Studio 2022 or later
- .NET Framework 4.8
- DataMiner Integration Studio (DIS)

### Building

1. Clone the repository:
   ```bash
   git clone https://github.com/SkylineCommunications/SLC-S-Ticketing.git
   ```

2. Open the solution in Visual Studio

3. Build the solution (Ctrl+Shift+B)

## Development

### Code Style

This project follows the [Skyline C# Coding Guidelines](link).

### Testing

Run unit tests before submitting pull requests:
```bash
dotnet test
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

## Links

- [Catalog Item](https://catalog.dataminer.services/details/...)
- [Documentation](https://docs.dataminer.services/...)
- [Issues](https://github.com/SkylineCommunications/SLC-S-Ticketing/issues)

## License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file.
```

---

### Repository README Quality

**[ERROR]** Repository README MUST:
- Be accurate and up-to-date
- Use proper markdown syntax
- Not contain broken links

**[WARNING]** Repository README SHOULD:
- Be concise and scannable
- Use consistent formatting
- Include a table of contents if lengthy (> 10 sections)

**[INFO]** Best practices:
- Keep it focused on repository/development concerns
- Delegate detailed user documentation to CatalogInformation README
- Update when major changes occur

---

## Project READMEs

### Purpose

Project READMEs are located within individual project folders and describe:
- What the specific project/component is
- Technical details specific to that component
- Build or configuration specifics for that project

**[WARNING]** Complex repositories SHOULD include project-level READMEs for:
- Individual connectors
- Individual automation scripts
- Separate applications or services
- Complex submodules

---

### Required Content - Project README

**[WARNING]** Project READMEs SHOULD include:

1. **Component Description**
   - What this specific component does
   - How it fits into the larger solution
   - Key responsibilities

2. **Technical Details**
   - Architecture or design notes
   - Important classes or modules
   - Dependencies specific to this project

3. **Building and Testing**
   - Project-specific build instructions
   - Testing procedures
   - Configuration requirements

**[INFO]** Consider including:
- API documentation or reference
- Known issues specific to this component
- Development notes or TODOs

---

### Project README Structure

**Example - Project README** (TicketingGateway/README.md):
```markdown
# TicketingGateway

## Description

The TicketingGateway is an automation script that handles ticket routing between DataMiner alarms and external ITSM platforms.

## Architecture

The gateway uses a plugin architecture to support multiple ITSM connectors:
- `ITicketingConnector` interface defines the contract
- `TicketRouter` handles routing logic
- `ConfigurationManager` manages connector selection

## Dependencies

- Skyline.DataMiner.Net
- Newtonsoft.Json
- Custom connectors (ServiceNow, Jira, etc.)

## Building

This project requires:
- .NET Framework 4.8
- DataMiner Integration Studio

Build using Visual Studio or:
```bash
msbuild TicketingGateway.csproj
```

## Configuration

Configuration is stored in `TicketingConfig.xml`:
```xml
<Configuration>
  <DefaultConnector>ServiceNow</DefaultConnector>
  ...
</Configuration>
```

## Testing

Run unit tests:
```bash
dotnet test TicketingGateway.Tests.csproj
```
```

---

### When to Use Project READMEs

**[INFO]** Use project READMEs when:
- The repository contains multiple distinct components
- Each component has unique technical details or build requirements
- The repository README would become too long with all details
- You want to provide context for developers working on specific components

**[INFO]** Skip project READMEs when:
- The repository contains a single, simple component
- All relevant information fits well in the repository README
- Projects are trivial or self-explanatory

---

## README vs CatalogInformation Distinction

### Clear Separation of Concerns

**[ERROR]** Do NOT confuse:
- **Repository/Project READMEs**: For developers working with the code
- **CatalogInformation README**: For users of the Catalog item

**[INFO]** Key differences:

| Aspect | Repository/Project README | CatalogInformation README |
|--------|---------------------------|---------------------------|
| **Audience** | Developers, contributors | End users, system admins |
| **Purpose** | How to develop/build | How to use the item |
| **Location** | Repository root, project folders | `CatalogInformation/` folder |
| **Content** | Build steps, architecture, dev guidelines | Installation, usage, configuration |
| **Visibility** | GitHub repository | DataMiner Catalog |

---

## Validation Process

When reviewing README files:

1. **Check Repository README Existence**: Verify README.md in root
2. **Validate Required Sections**: Ensure ERROR-level sections are present
3. **Review Repository Content**: Check for development-focused information
4. **Check Project READMEs**: Verify complex projects have component READMEs
5. **Validate Separation**: Ensure repository README doesn't duplicate Catalog docs
6. **Test Links**: Verify all links work
7. **Check Formatting**: Ensure proper markdown and consistency
8. **Verify Accuracy**: Confirm information is current and correct

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| No repository README | ERROR | Create README.md with required sections |
| README missing build instructions | ERROR | Add getting started and build sections |
| Repository README duplicates Catalog docs | WARNING | Separate concerns - focus repo README on development |
| No project READMEs in complex repo | WARNING | Add READMEs for major components |
| Broken links in README | ERROR | Fix or remove broken links |
| README not updated for recent changes | WARNING | Update to reflect current state |
| No build status badge | WARNING | Add CI/CD status badge |
| README is too lengthy | INFO | Consider splitting into multiple docs or adding TOC |
| No folder structure explanation | WARNING | Add section describing repository layout |

---

## Best Practices

**[INFO]** General README best practices:

1. **Be Concise**: READMEs should be scannable; link to detailed docs
2. **Use Visuals**: Include diagrams, screenshots, or badges where helpful
3. **Keep Updated**: Review and update READMEs with significant changes
4. **Be Consistent**: Use consistent formatting and style across READMEs
5. **Test Instructions**: Verify that build/setup instructions actually work
6. **Link Appropriately**: Link to CatalogInformation README, not duplicate content
7. **Focus on Audience**: Repository README for developers, Catalog README for users

---

## Output Format

When validating README files, provide:
- **Compliant items**: Summary of well-documented READMEs
- **Non-compliant items**: Detailed list of missing or inadequate content with severity
- **Structure issues**: Problems with organization or formatting
- **Improvement suggestions**: Optional enhancements (INFO level)
- **Distinction issues**: Cases where repository/project READMEs duplicate Catalog documentation
