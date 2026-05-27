# wp-plugin-registry

## **Overview**

**wp-plugin-registry** is the **canonical JSON registry** for all **Psydox-maintained WordPress plugins** used by **Psydox WP Hub**.

It acts as the **single source of truth** for:

- **Plugin discovery**
- **Metadata retrieval**
- **Installation endpoints**
- **Version update checks**
- **Changelog links**

Instead of scanning GitHub repositories dynamically, Psydox WP Hub reads this registry directly for controlled and predictable plugin management.

## **Purpose**

This repository exists to centralize plugin records so Psydox WP Hub can reliably determine:

1. Which Psydox plugins should be visible in the Hub
2. Where each plugin metadata file is located
3. Which release package should be installed or updated
4. Where users can view changelog details

## **How It Works**

1. Psydox WP Hub fetches the registry file.
2. The registry returns a list of plugin entries.
3. Each entry contains a plugin slug and a metadata URL.
4. Hub fetches each plugin metadata document.
5. Hub compares installed versions against remote versions.
6. Hub enables install/update actions using the metadata download URL.

## **Registry Format**

```json
{
  "version": "1.0",
  "plugins": [
    {
      "slug": "psydox-seo",
      "metadata_url": "https://raw.githubusercontent.com/Psydox/psydox-seo/main/plugin.json"
    },
    {
      "slug": "psydox-security",
      "metadata_url": "https://raw.githubusercontent.com/Psydox/psydox-security/main/plugin.json"
    }
  ]
}
```

### **Field Definitions**

- **version**: Registry schema/version identifier
- **plugins**: List of plugin objects
- **slug**: Unique plugin slug used by Psydox WP Hub
- **metadata_url**: URL to the plugin metadata file

## **Plugin Metadata Format**

Each plugin repository should expose a plugin.json file in this format:

```json
{
  "name": "Psydox SEO",
  "slug": "psydox-seo",
  "version": "1.0.0",
  "author": "Psydox",
  "description": "SEO toolkit for WordPress.",
  "requires_wp": "6.5",
  "requires_php": "8.2",
  "repository": "https://github.com/Psydox/psydox-seo",
  "download_url": "https://github.com/Psydox/psydox-seo/releases/latest/download/psydox-seo.zip",
  "changelog_url": "https://github.com/Psydox/psydox-seo/releases"
}
```

### **Required Metadata Fields**

- **name**
- **slug**
- **version**
- **author**
- **description**
- **requires_wp**
- **requires_php**
- **repository**
- **download_url**
- **changelog_url**

## **Validation Rules**

To keep registry quality high:

- **slug** must be lowercase and URL-safe
- **metadata_url** must be reachable and return valid JSON
- metadata **slug** must match registry **slug**
- **version** should follow semantic versioning
- **download_url** should point to a valid release ZIP

## **Contribution Workflow**

When adding or updating a plugin:

1. Update the registry entry in the registry JSON file.
2. Ensure metadata_url points to a valid plugin.json file.
3. Validate the plugin.json structure and required fields.
4. Open a pull request with a clear summary of changes.

## **Design Principles**

- **Centralized control**: all plugin visibility is defined in one place
- **Predictable behavior**: no dynamic repository discovery
- **Operational simplicity**: straightforward JSON contracts
- **Compatibility safety**: explicit WordPress/PHP requirements

## **Security and Reliability Notes**

- Keep metadata URLs and download URLs under trusted Psydox repositories.
- Use release assets generated from tagged versions.
- Avoid unverified external mirrors for download URLs.
- Keep changelog URLs current for transparency.

## **License**

This project is intended to support GPL-compatible WordPress ecosystem tooling. Use a license that aligns with your organizational policy, typically **GPL v2 or later** for WordPress plugin interoperability.

## **Maintainer**

**Psydox**

---

If this registry changes, Psydox WP Hub behavior changes accordingly. Keep records accurate, stable, and versioned.
