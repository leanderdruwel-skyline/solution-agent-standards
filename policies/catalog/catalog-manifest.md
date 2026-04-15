# Catalog Item Creation Validation

## Scope

This file defines validation rules for creating and publishing Catalog items on dataminer.services. These rules ensure items are discoverable, correctly described, properly versioned, and compliant with organizational standards.

> **Note**: This file uses severity tags `[ERROR]`, `[WARNING]`, and `[INFO]` as defined in [../global-instructions.md](../global-instructions.md#severity-levels).

---

## Overview

When publishing a Catalog item, two goals must be achieved: users must be able to **find** it, and they must clearly **understand** what it is meant for. This policy validates the manifest configuration, versioning practices, ownership, and size compliance that together ensure those goals are met.

**Reference**: [Best practices when creating Catalog items | DataMiner Docs](https://docs.dataminer.services/develop/best_practices/Catalog_Items/Best_Practices_When_Creating_Catalog_Items.html)

---

## Manifest Visibility

### Name

**[ERROR]** The manifest `name` field MUST be clear to the user:
- The name must communicate what the solution is meant to be used for
- Avoid technical terms, internal codes, or abbreviations that are not industry-standard

**[WARNING]** The name SHOULD:
- Be intuitive to a user who is unfamiliar with the solution
- Follow title case convention

---

### Type

**[ERROR]** The manifest MUST include the correct `type` for the Catalog item.
- The type must accurately reflect the nature of the item
- For a full list of valid types, see [About Catalog items](https://docs.dataminer.services/dataminer/dataminer_services/Catalog/About_the_Catalog_app.html#about-catalog-items)

**[WARNING]** For public Catalog items, generally avoid using `Custom Solution` as the type:
- Use a more specific type (e.g., `Standard Solution`, `Automation Script`, `Connector`) where applicable
- `Custom Solution` is appropriate only when no other type fits

---

### Tags

**[ERROR]** The manifest tags MUST follow these rules:
- Do **not** use the name of the Catalog item as a tag
- Do **not** use the type of the Catalog item as a tag
- Do **not** use general DataMiner terms (e.g., `DataMiner`) as tags
- Use at most **5 tags** per Catalog item

**[WARNING]** Tags SHOULD:
- Be user-centric or market-centric (focus on what the user does or the market it targets)
- Avoid uncommon abbreviations
- Avoid using plurals when not necessary (e.g., use `Source` instead of `Sources`)
- Use [title case](https://docs.dataminer.services/develop/codingguidelines/UserInterface/Title_case.html)
- Contain at most **3 words** per tag

**[INFO]** The main goal of tags is to expose the Catalog item to relevant searches. Tags that describe the user's domain, technology, or workflow are more effective than tags describing the item itself.

---

### Icon

**[WARNING]** The Catalog item SHOULD have an icon assigned:
- Define a vendor for the item using the `vendor_id` field in the manifest
- An icon catches the user's attention and improves discoverability in the Catalog

**[INFO]** If assistance is needed to assign a vendor or icon, reach out to your technical contact at Skyline Communications.

---

## Versioning

### Semantic Versioning

**[ERROR]** Versions MUST follow [semantic versioning](https://semver.org/) using the `A.B.C` format (for all item types except connectors):
- **A (MAJOR)**: Incremented for incompatible changes, breaking changes, or major architectural redesigns that may require user action
- **B (MINOR)**: Incremented for new functionality added in a backward-compatible manner
- **C (PATCH)**: Incremented for backward-compatible bug fixes; when a new range is introduced, the PATCH version MUST start at `0`, not `1`

**[INFO]** Connectors use a special `A.B.C.D` format. For connector versioning details, see [Protocol version semantics](https://docs.dataminer.services/develop/devguide/Connector/ProtocolVersionSemantics.html).

**[WARNING]** The `CUx` suffix (e.g., `1.2.3-CU2`) MUST only be used in exceptional cases:
- Only when a critical issue is discovered after a release deployment
- The released version should be unlisted and replaced with a new cumulative update release

---

### Version Descriptions

**[WARNING]** Each version SHOULD include a clear description of what has changed:
- Use the phrases `Change:`, `Fix:`, and `New Feature:` to categorize entries
- Each phrase can be used multiple times within a single version description

**[INFO]** For standard solutions, the version description SHOULD contain a link to the corresponding release notes (e.g., a link to docs.dataminer.services release notes for that solution).

---

### Range Tagging

**[WARNING]** Range tags SHOULD be assigned correctly:
- There SHOULD be only **one Main range** - the latest and most recommended range to install
- Keep the number of **Active ranges** as low as possible
- An Active range indicates the range is still being maintained and bug fixes should continue to be added to it
- Custom tags on a range SHOULD only be used in exceptional cases (e.g., when two ranges are both valid options but each has specific characteristics)

---

## Ownership

**[ERROR]** Each Catalog item MUST have at least one owner defined in the manifest:
- The owner MUST be an individual person, not a team or group account
- The `name` field MUST contain the owner's full name - do not include an email address in this field
- The `email` field is recommended and should contain the owner's email address
- The `url` field SHOULD contain a URL associated with the owner (e.g., a GitHub account URL)

**[WARNING]** Multiple owners can be specified by adding additional entries to the owner list. This is encouraged for items with shared responsibility.

---

## Size Limitations

**[WARNING]** The following size limits MUST be respected when creating Catalog items:

| Asset | Maximum size |
|-------|-------------|
| Catalog item package (`.zip`) | 250 MB |
| Version file (`.dmprotocol` or `.dmapplication`) | 250 MB |
| Vendor logos and custom icons | 250 KB |

**[INFO]** Images included in `README.md` (within the `Images` folder inside `manifest.zip`) are **not** subject to the 250 KB per-image restriction. That limit applies only to vendor logos and custom icons.

---

## Naming Conventions

**[INFO]** For naming conventions that apply to Catalog item components (e.g., script names, connector names, parameter names), refer to the dedicated guidance:
- [Naming conventions for Catalog item components](https://docs.dataminer.services/develop/best_practices/Catalog_Items/Naming_Conventions_For_Catalog_Item_Components.html)

---

## Validation Process

When reviewing a Catalog item before or after publication:

1. **Check manifest name**: Verify the name is clear, avoids technical terms, and communicates the item's purpose to a non-technical user
2. **Check manifest type**: Confirm the type is correct and specific; verify `Custom Solution` is not used for public items unless no other type fits
3. **Validate tags**: Confirm tags do not use the item name or type, contain no general DataMiner terms, use title case, contain at most 3 words each, and the total tag count does not exceed 5
4. **Check icon**: Verify a vendor/icon is assigned via the `vendor_id` field in the manifest
5. **Verify semantic versioning**: Confirm versions follow `A.B.C` format (or `A.B.C.D` for connectors), PATCH starts at 0 for new ranges, and the `CUx` suffix is used only in exceptional cases
6. **Check version descriptions**: Confirm each version uses `Change:`, `Fix:`, or `New Feature:` phrasing; for standard solutions, verify a release notes link is included
7. **Review range tagging**: Confirm there is only one Main range and Active ranges are kept to a minimum
8. **Validate ownership**: Confirm at least one individual owner is defined with a full name, email, and URL
9. **Check size compliance**: Verify package, version file, and icon/logo sizes are within the permitted limits

---

## Common Issues and Solutions

| Issue | Severity | Solution |
|-------|----------|----------|
| Manifest name uses technical terms or internal codes | ERROR | Rename to clearly describe the item's purpose in plain language |
| Manifest type is missing or incorrect | ERROR | Assign the correct type from the Catalog type list |
| Tag uses item name or type | ERROR | Remove the tag; replace with user-centric or market-centric alternatives |
| Tag uses a general DataMiner term | ERROR | Remove the tag; use domain- or technology-specific terms instead |
| More than 5 tags defined | ERROR | Trim to the 5 most relevant and impactful tags |
| No owner defined | ERROR | Add at least one individual owner with name, email, and URL |
| Owner is a team or group account | ERROR | Replace with an individual person's account |
| Email address included in the `name` field | ERROR | Move the email address to the `email` field |
| Version does not follow A.B.C semantic versioning | ERROR | Rename the version to comply with semantic versioning |
| PATCH version starts at 1 instead of 0 for a new range | ERROR | Rename the initial version to end in `.0` |
| `Custom Solution` type used for a public item | WARNING | Replace with a more specific type where possible |
| No icon or vendor assigned | WARNING | Define a `vendor_id` in the manifest to assign an icon |
| Tags use plurals unnecessarily | WARNING | Simplify tags (e.g., `Source` instead of `Sources`) |
| Tags do not use title case | WARNING | Update tags to use title case |
| Tag contains more than 3 words | WARNING | Shorten the tag to at most 3 words |
| `CUx` suffix used for non-critical release | WARNING | Only use `CUx` for critical post-deployment fixes; use a normal version otherwise |
| Version description missing or unclear | WARNING | Add a description using `Change:`, `Fix:`, or `New Feature:` phrases |
| Multiple Active ranges without justification | WARNING | Consolidate into fewer active ranges; keep only one Main range |
| Icon/logo file exceeds 250 KB | WARNING | Reduce the file size to stay within the 250 KB limit |

---

## Output Format

Use the standard validation output format defined in [../global-instructions.md](../global-instructions.md#validation-output-format).

The section header for this policy's results block must read:

```
### catalog / manifest-validation
```
