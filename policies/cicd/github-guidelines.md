# GitHub Guidelines Validation

## Scope

This file defines validation rules for GitHub repositories following Skyline Communications' GitHub usage guidelines. These rules apply to all Skyline repositories hosted on GitHub.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

GitHub repositories in the Skyline Communications organization must follow specific guidelines to ensure discoverability, maintainability, and compliance with organizational standards.

**Reference**: [Using GitHub - Guidelines | DataMiner Docs](https://docs.dataminer.services/develop/CICD/Skyline%20Communications/Github/Use_Github_Guidelines.html)

---

## Account and Repository Creation

### Repository Visibility

**[WARNING]** Choose the correct visibility when creating a repository:
- **Public**: For generic code/scripts that can be shared with the broader DataMiner community
- **Private**: For code specific to a customer project that cannot be shared publicly

**[ERROR]** Public repositories MUST NOT include a customer acronym in the name. Use `SLC` instead. Refer to the Repository Naming Convention section for details.

---

## License

### License Selection

**[ERROR]** Every repository MUST include a license file.
- Select the correct license at repository creation time
- Changing the license later is very challenging

**[ERROR]** For automation scripts and most public repositories, the license MUST be **MIT**. Refer to the Item Type table in the Repository Naming Convention section for guidance on item types.

**[WARNING]** If unsure about the correct license for a public repository:
- Contact the IT team before creating the repository, OR
- Create a private repository first and convert to public only once the correct license is applied

---

## Repository Naming Convention

### Name Format

**[ERROR]** Repository names MUST follow the naming pattern using `-` as separator:
- **Private repositories**: `{customerAcronym}-{itemType}-{itemName}`
- **Public repositories**: `SLC-{itemType}-{itemName}` (use `SLC` acronym, never a customer acronym)

**[WARNING]** When a repository contains projects with different types, treat it as a Solution and use the `S` item type.

### Item Type

**[ERROR]** The repository name MUST use a valid item type code. Supported item types:

| Syntax | Description |
|--------|-------------|
| `AS` | Automation Scripts (specific types such as GQI data sources, User-Defined APIs, regression tests have their own syntax) |
| `C` | Connectors |
| `CF` | Companion Files |
| `CHATOPS` | ChatOps extension |
| `D` | Dashboards |
| `DISMACRO` | DIS Macro |
| `DOC` | Documentation |
| `F` | Functions |
| `GQIDS` | GQI data source |
| `GQIO` | GQI operator |
| `LCA` | Low-Code App |
| `LSO` | Lifecycle Service Orchestration |
| `PA` | Process Automation |
| `PLS` | Profile-Load Scripts |
| `S` | Solutions |
| `SC` | Scripted Connector |
| `T` | Tests: regression tests, integration tests, performance tests, etc. |
| `UDAPI` | User-Defined APIs |
| `V` | Visio files |
| `EXT` | External tools - software |

**[WARNING]** If the required item type is not in the table above, contact the team to have it added before creating the repository.

### Item Name

**[WARNING]** The item name MUST clearly indicate the purpose of the repository.

---

## README Files

### Root README

**[ERROR]** The repository MUST include a `README.md` file in the root folder.

**[ERROR]** The root `README.md` MUST include:

1. **Repository goal**: A short description (maximum three sentences) explaining the purpose of the repository
2. **Projects overview**: A list of all projects in the solution, including:
   - The project name as a link to its subfolder README (e.g., `[ProjectName](ProjectFolder/README.md)`)
   - A brief description of the project's goal

**[WARNING]** If the repository is published in the Catalog, the root README SHOULD include a TIP alert with a Catalog link:

```markdown
> [!TIP]
> This repository is available in the Catalog: [Catalog item name | Catalog | dataminer.services](https://catalog.dataminer.services/details/{catalog-item-guid})
>
> The Catalog item GUID (ID) and Name (Title) can be found in the *manifest.yml* file.
```

### Project README

**[ERROR]** Each project subfolder MUST contain its own `README.md` file.

**[ERROR]** Each project README MUST include:

1. **Summary**: A functional overview of the project describing what it does — avoid method-level details
2. **Input arguments** (if applicable): Documentation of any input parameters defined in the XML, including:
   - Parameter name
   - Expected type (number, text, multiple choice, etc.)
   - Description of the parameter's purpose

**[INFO]** The project type is automatically determined based on the following code patterns:

| Code Pattern | Project Type |
|---|---|
| C# file implementing `IGQIDataSource` | Ad-Hoc Data Source |
| C# file implementing `IGQIRowOperator` and/or `IGQIColumnOperator` | Data Transformer |
| C# file containing `[AutomationEntryPoint(AutomationEntryPointType.Types.OnApiTrigger)]` | User-Defined API |
| DMSScript XML file with `<Folder>` tag equal to `bot` or starting with `bot/` | ChatOps Operator |
| DMSScript XML file | Automation Script |
| Protocol XML file | Connector |

---

## .gitignore

**[ERROR]** The repository MUST include a `.gitignore` file in the root folder.
- Prevents committing build artifacts (e.g., assemblies from `bin` folders) and user-specific configuration files
- Using the default suggested `.gitignore` for Visual Studio is sufficient

---

## Topics

### Required Topics

**[ERROR]** The repository MUST have at least one relevant topic applied to aid categorization and discoverability.

**[WARNING]** Use the appropriate topic(s) from the following list:

- `dataminer`
- `dataminer-connector`
- `dataminer-visio`
- `dataminer-solution`
- `dataminer-function`
- `dataminer-automation-script`
- `dataminer-dashboard`
- `dataminer-profile-load-script`
- `dataminer-process-automation-script`
- `dataminer-life-service-orchestration`
- `dataminer-gqi-data-source`
- `dataminer-gqi-operator`
- `dataminer-regression-test`
- `dataminer-UI-test`
- `dataminer-bot`
- `dataminer-user-defined-api`
- `dataminer-doc`
- `dataminer-dis-macro`
- `dataminer-chatops`
- `dataminer-nuget`

**[WARNING]** If the code is for a specific project or customer, add a topic with the customer's name (e.g., `Skyline-Communications`). Always use a hyphen (`-`) as a separator.

**[INFO]** For regression tests: use `T` as the item type in the repository name and use topics to specify the type of test (e.g., `dataminer-regression-test`).

---

## NuGet Repositories

**[WARNING]** Repositories that produce NuGet packages SHOULD:
- Use the `dataminer-nuget` topic
- Ensure the NuGet package name matches the repository name
- Follow the guidance in [Producing NuGet packages](https://docs.dataminer.services/develop/TOOLS/NuGet/Producing_NuGet.html) for naming, versioning, metadata, and package creation

**[INFO]** Relevant references for NuGet repositories:
- [NuGet package recommendations](https://docs.dataminer.services/develop/best_practices/NuGet_Recommendations.html)
- [Producing NuGet packages](https://docs.dataminer.services/develop/TOOLS/NuGet/Producing_NuGet.html)
- [DataMiner Dev Packs](https://docs.dataminer.services/develop/TOOLS/NuGet/TOODataMinerDevPackages.html)

---

## Workflows

### CI/CD Workflows

**[WARNING]** Repositories SHOULD include CI/CD workflows that cover:
- Building the solution
- Running unit tests
- Using SonarCloud
- Compiling to a DataMiner package
- Deploying to a cloud-connected DataMiner Agent

**[WARNING]** When using Visual Studio Templates, workflows are automatically included. The `complete` workflow SHOULD be used as it provides the full CI/CD pipeline via the Skyline [reusable workflow template](https://github.com/SkylineCommunications/_ReusableWorkflows/blob/main/.github/workflows/DataMiner%20App%20Packages%20Master%20Workflow.yml).

**[WARNING]** If a workflow other than `complete` is used (e.g., `demo` or `build`), verify that the reduced scope is intentional and justified. Using a partial workflow omits steps such as SonarCloud analysis, DataMiner package compilation, or deployment.

### Deployment Action

**[INFO]** The [Skyline-DataMiner-Deploy-Action](https://github.com/SkylineCommunications/Skyline-DataMiner-Deploy-Action) is publicly available on GitHub for deploying from a GitHub repository.
- See [Marketplace deployment action](https://docs.dataminer.services/develop/CICD/GitHub/Marketplace_deployment_action.html) for more information.

---

## External Collaboration

**[INFO]** For private repositories created for customer projects:
- External users (customer employees) can be invited as **outside collaborators**
- Outside collaborators SHOULD work on a **fork** of the repository
- Changes must be submitted via a **pull request** for the repository owner to review and merge

---

## Dependabot Configuration

**[WARNING]** If a repository uses NuGet packages from Skyline's internal GitHub NuGet registry, Dependabot SHOULD be configured to access that private feed.

**[INFO]** Example Dependabot configuration (`.github/dependabot.yml`):

```yaml
version: 2
registries:
  public:
    type: nuget-feed
    url: https://api.nuget.org/v3/index.json
  slc-github:
    type: nuget-feed
    url: https://nuget.pkg.github.com/SkylineCommunications/index.json
    username: ${{ secrets.PRIVATE_NUGET_USERNAME }}
    password: ${{ secrets.PRIVATE_NUGET_PASSWORD }}
updates:
  - package-ecosystem: "nuget"
    directory: "/"
    registries: "*"
    schedule:
      interval: "daily"
```

The `PRIVATE_NUGET_USERNAME` and `PRIVATE_NUGET_PASSWORD` secrets are only available to Dependabot.

---

## Validation Process

When reviewing a repository against these guidelines:

1. **Check license**: Verify a valid license file exists and uses MIT for scripts/public repositories
2. **Validate repository name**: Confirm the `{acronym}-{itemType}-{itemName}` format, valid item type code, and correct acronym for visibility
3. **Verify root README**: Check existence and required sections (repository goal, projects overview, Catalog link if published)
4. **Verify project READMEs**: Confirm each project subfolder has a README with a summary and documented input arguments
5. **Check .gitignore**: Confirm `.gitignore` is present in the root
6. **Review topics**: Verify at least one appropriate `dataminer-*` topic is applied; check for customer topic if applicable
7. **Check workflows**: Validate CI/CD workflows are present and use the `complete` option where possible
8. **Review NuGet setup**: If applicable, check `dataminer-nuget` topic and naming conventions
9. **Review Dependabot config**: If private NuGet feeds are used, verify `.github/dependabot.yml` is configured

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| No license file | ERROR | Add the appropriate license (MIT for scripts) at repository creation |
| Incorrect license type | ERROR | Contact IT team to resolve before publishing publicly |
| Repository name does not follow convention | ERROR | Rename following `{acronym}-{itemType}-{itemName}` pattern |
| Customer acronym used in public repository name | ERROR | Rename using `SLC` as the acronym |
| Invalid or missing item type in name | ERROR | Use a valid item type from the table; contact team if type is missing |
| No root README | ERROR | Create `README.md` with repository goal and projects overview |
| Root README missing projects overview | ERROR | Add list of all projects with links to subfolder READMEs |
| No project README in subfolder | ERROR | Create `README.md` per project with summary and input arguments |
| No `.gitignore` file | ERROR | Add `.gitignore` to root using the default Visual Studio template |
| No topics applied | ERROR | Add at least one appropriate `dataminer-*` topic |
| No Catalog link in README | WARNING | Add TIP alert with Catalog link if item is published in the Catalog |
| No CI/CD workflow | WARNING | Add workflow via Visual Studio Templates (`complete` option recommended) |
| Workflow other than `complete` in use | WARNING | Verify the reduced scope is intentional; switch to `complete` if possible |
| No Dependabot config for private NuGet | WARNING | Add `.github/dependabot.yml` with private registry configuration |
| NuGet repository missing `dataminer-nuget` topic | WARNING | Add `dataminer-nuget` topic to the repository |
| Item name does not clearly indicate purpose | WARNING | Rename or clarify the item name portion of the repository name |

---

## Output Format

When validating a repository against these guidelines, provide:
- **Compliant items**: Summary of correctly configured aspects
- **Non-compliant items**: Detailed list of violations with severity
- **Naming analysis**: Breakdown of the repository name into its acronym, item type, and item name components
- **Missing files**: List of required files that are absent (license, README, .gitignore)
- **Improvement suggestions**: Optional enhancements (INFO level)
