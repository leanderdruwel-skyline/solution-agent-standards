# Catalog Item Documentation Validation

## Scope

This file defines validation rules for documentation of Catalog items published on dataminer.services. These rules apply to the README displayed on the Catalog item's page, located in the `CatalogInformation` folder.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

Catalog item documentation must be attractive and clearly present the value of the item to potential users. The main principle is that it should be concise and focused on showcasing value â€” not exhaustive technical documentation.

**Reference**: [Best practices when documenting Catalog items | DataMiner Docs](https://docs.dataminer.services/develop/best_practices/Catalog_Items/Best_Practices_When_Documenting_Catalog_Items.html)

---

## CatalogInformation README

### Existence

**[ERROR]** The `CatalogInformation` folder MUST contain a `README.md` file.
- This README is displayed on the Catalog item's page on dataminer.services
- For extensive technical details, use the `documentation_url` field in the manifest to link to external documentation rather than embedding everything inline

**[INFO]** This README is distinct from:
- The **repository README** â€” describes the repository itself for developers and contributors
- **Project READMEs** â€” describe individual project components in their subfolders

---

## Documentation Structure

### Required Sections

**[ERROR]** The CatalogInformation README MUST include an **About** section:
- Summarizes what makes the item valuable and why users should deploy it
- Addresses the problems it solves and its primary benefits

**[ERROR]** The CatalogInformation README MUST include a **Key Features** section:
- Outlines the main features that distinguish the item
- Focuses on functionality and unique benefits

### Optional Sections

**[WARNING]** The following sections SHOULD be included when applicable:

| Section | When to include |
|---------|----------------|
| **Use Cases** | When there are meaningful real-world scenarios to demonstrate |
| **Prerequisites** | When there are DataMiner version, license, or dependency requirements |
| **Technical Reference** | When detailed external documentation exists |

**[INFO]** For simple items, sections can be combined. For example, a very simple item could leave out Use Cases and mention that information briefly under Key Features instead.

### Contact and Support

**[ERROR]** The CatalogInformation README MUST NOT include references to support contacts or team email addresses:
- Direct users to the [DataMiner Support team](https://docs.dataminer.services/dataminer/Troubleshooting/Contacting_tech_support.html)
- Owner email addresses belong in the `manifest.yml` file, not in documentation

---

## About Section

### Content Rules

**[ERROR]** The About section MUST:
- Summarize what makes the item valuable and why users should deploy it
- Address the problems it solves and its primary benefits

**[WARNING]** The About section SHOULD:
- Use accessible language for both technical and non-technical readers
- Highlight important points with bold text
- Organize content from broad benefits to specific features and practical applications
- Make use of visual [alerts](https://docs.dataminer.services/contributing/CTB_Markdown_Syntax.html#alerts) where applicable
- Keep the tone professional and focused on motivating user adoption

**[WARNING]** The About section MUST NOT:
- Include excessive technical details â€” link to reference documentation instead
- Use jargon or overly complex language
- Use excessive amounts of bold text and/or alerts, as these then lose their purpose
- Refer to generic DataMiner benefits such as alarming and trending â€” focus on the value this specific item brings
- Duplicate points mentioned in the Key Features and Use Cases sections

---

## Key Features Section

### Content Rules

**[ERROR]** The Key Features section MUST:
- Outline the main features that distinguish the item
- Contain a maximum of **5 features** â€” quality over quantity

**[WARNING]** The Key Features section SHOULD:
- Use direct, benefit-oriented language
- Ensure that each feature relates to specific value for the user
- Use action verbs (e.g., "Monitor", "Track", "Detect", "Automate")
- Prioritize features that differentiate the item

**[WARNING]** The Key Features section MUST NOT:
- Include excessive detail or vague descriptors like "high-performance" without specific context
- Add features that are general to DataMiner rather than specific to this item (e.g., the benefits of alarming, which is already a DataMiner capability)

---

## Use Cases Section

### Content Rules

**[WARNING]** When included, the Use Cases section SHOULD:
- Demonstrate practical, real-world scenarios where the solution provides value
- Connect examples to common challenges that users face (e.g., remote connectivity, high data usage)
- Use specific, relatable examples (e.g., "Monitor remote satellite terminals in real-time")
- Optionally provide a link to a use case on [DataMiner Dojo](https://community.dataminer.services/use-cases/)
- Include accompanying visuals where appropriate

**[WARNING]** The Use Cases section MUST NOT:
- Include hypothetical scenarios â€” examples must be relevant to the typical user base
- Duplicate points covered in the Key Features section

---

## Prerequisites Section

### Content Rules

**[WARNING]** When included, the Prerequisites section SHOULD:
- Use concise bullet points limited to strictly necessary information
- State the minimum DataMiner version using **both** Feature Release and Main Release version numbers
- Mention minimum/maximum DxM version if applicable
- List required licenses (e.g., DOM, SRM)
- List required soft-launch options
- List required other Catalog items or component dependencies

**[INFO]** Only mention a minimum DataMiner version if it is a [currently supported DataMiner version](https://docs.dataminer.services/dataminer/Reference/Software_support_life_cycles.html). If the DataMiner Web or Cube version requirement differs from the server version, mention it separately.

**[WARNING]** The Prerequisites section MUST NOT:
- Include complex installation or configuration steps â€” link to documentation instead
- List every small technical dependency â€” focus only on the essentials

---

## Technical Reference Section

### Content Rules

**[WARNING]** When included, the Technical Reference section SHOULD:
- Link to detailed technical documentation using the `documentation_url` field in the manifest
- Use a `> [!NOTE]` alert with a link in the README description when relevant
- Use consistent naming conventions (e.g., "Installing ...", "Working with ...")
- Use public links for additional resources (e.g., docs.dataminer.services for Skyline solutions)
- Use "aka" redirect links when linking to docs.dataminer.services as a Skyline employee, so links can be updated if documentation structure changes

**[WARNING]** The Technical Reference section MUST NOT:
- Include procedures that should not be followed by the user
- Add redundant information already available elsewhere â€” link to it instead
- Document features that change frequently and are not critical to document (e.g., UI details)
- List every small technical dependency â€” focus only on the essentials

---

## Visuals

### Image and GIF Guidelines

**[WARNING]** When visuals are included, they SHOULD:
- Be stored in the `Images` folder within the `manifest.zip` file
- Be limited to a maximum of **3 visuals** to support key points
- Be clear, focused, and free from irrelevant elements
- Use high-quality resolution
- For tables: hide irrelevant columns and only show items relevant to the Catalog item

**[WARNING]** GIFs SHOULD:
- Be at most **10 seconds** and focused on demonstrating one specific feature or action
- Include sufficient time between each click or visual change to avoid disturbing the viewer

**[WARNING]** Visuals MUST NOT:
- Be blurry or pixelated â€” quality is key
- Show unnecessary open panels (e.g., Alarm Console) that do not add value
- Contain unnecessary blank space â€” resize the window when taking a screen capture
- Display confidential data â€” blur sensitive data while keeping non-sensitive data visible

---

## Validation Process

When reviewing Catalog item documentation:

1. **Check README existence**: Verify `CatalogInformation/README.md` exists
2. **Verify About section**: Confirm the About section is present, concise, and focused on value â€” not technical detail or generic DataMiner capabilities
3. **Verify Key Features section**: Confirm the Key Features section is present, contains at most 5 features, and uses specific benefit-oriented language
4. **Check Use Cases section**: If the item has meaningful real-world scenarios, confirm they are documented with specific, non-hypothetical examples
5. **Check Prerequisites section**: If technical requirements exist, confirm they are listed concisely with DataMiner version covering both FR and MR tracks
6. **Check Technical Reference section**: If detailed documentation exists externally, confirm it is linked rather than duplicated inline
7. **Review visuals**: Verify included visuals are relevant, high quality, free from sensitive/irrelevant content, and within the 3-visual limit
8. **Check for contact/support references**: Verify no support contacts or email addresses appear in the documentation body

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| No `CatalogInformation/README.md` file | ERROR | Create the README with About and Key Features sections at minimum |
| About section missing | ERROR | Add an About section summarizing the item's value and the problems it solves |
| Key Features section missing | ERROR | Add a Key Features section with up to 5 benefit-oriented, item-specific features |
| Support or contact details in documentation | ERROR | Remove contact references; direct users to the DataMiner Support team instead |
| Key Features section contains more than 5 items | WARNING | Trim to the 5 most differentiating features |
| Key Features describe generic DataMiner capabilities | WARNING | Replace with features specific to this item |
| About section contains excessive technical detail | WARNING | Move technical detail to Technical Reference and link out instead |
| Use Cases section missing for non-trivial items | WARNING | Add specific, real-world scenarios showing the item's value |
| Prerequisites section missing when dependencies exist | WARNING | Add concise prerequisites including DataMiner version (both FR and MR tracks) |
| Technical Reference missing when detailed docs exist | WARNING | Link to external documentation using the `documentation_url` manifest field |
| Only one version track mentioned in Prerequisites | WARNING | Add both Feature Release and Main Release version numbers |
| Visuals missing | WARNING | Add up to 3 relevant, high-quality images or GIFs illustrating key features |
| Visuals show sensitive or irrelevant data | WARNING | Blur sensitive data; hide irrelevant columns and close unnecessary panels |
| GIF longer than 10 seconds | WARNING | Trim or re-record the GIF to focus on a single feature or action |
| About section duplicates Key Features content | WARNING | Restructure so About gives the value overview and Key Features lists specifics |

---

## Output Format

Use the standard validation output format defined in [../global-instructions.md](../global-instructions.md#validation-output-format).

The section header for this policy's results block must read:

```
### catalog / documentation-validation
```
