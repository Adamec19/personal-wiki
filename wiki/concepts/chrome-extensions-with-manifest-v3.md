---
title: Chrome Extensions with Manifest V3
summary: Manifest V3 extensions declare their configuration, permissions, and static network rulesets in manifest.json.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:13.756Z"
updatedAt: "2026-11-11T10:54:13.756Z"
tags:
  - chrome-extensions
  - manifest-v3
aliases:
  - chrome-extensions-with-manifest-v3
  - CEWMV
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Chrome Extensions with Manifest V3

Manifest V3 is a Chrome extension manifest format used in the source’s “Bypass SharePoint” example. The extension changes browser behavior through [[Declarative Network Request Rules|declarative network rules]] defined in JSON, redirecting a specific SharePoint page to Google. ^[how-to/chrome-extension/README.md:1-3, how-to/chrome-extension/README.md:94-96]

## Extension structure

The example’s `bypass-sharepoint/` directory contains `manifest.json` for extension configuration, `rules.json` for network rules, and a Chrome-generated `_metadata/` directory. It can serve as a template for a similar extension. ^[how-to/chrome-extension/README.md:7-16]

The manifest sets `manifest_version` to `3`, declares the extension’s name and version, and requests `declarativeNetRequestWithHostAccess`. [[Extension Host Permissions|Host permissions]] specify the SharePoint host, while `declarative_net_request.rule_resources` registers and enables the rules file. ^[how-to/chrome-extension/README.md:24-52]

```json
{
  "manifest_version": 3,
  "name": "Bypass SharePoint",
  "version": "1.0",
  "permissions": ["declarativeNetRequestWithHostAccess"],
  "host_permissions": ["https://directpojistovnaas.sharepoint.com/*"],
  "declarative_net_request": {
    "rule_resources": [
      {
        "id": "ruleset_1",
        "enabled": true,
        "path": "rules.json"
      }
    ]
  }
}
```

## Declarative network behavior

A network rule contains a unique `id`, a `priority`, an `action` describing what happens, and a `condition` describing when it applies. The source demonstrates [[Declarative URL Redirection|redirection]], [[Declarative Request Blocking|blocking]], and [[Request Header Modification|request header modification]]. ^[how-to/chrome-extension/README.md:75-80, how-to/chrome-extension/README.md:146-202]

The redirect example uses `regexFilter` to match the SharePoint intranet URL and `resourceTypes: ["main_frame"]` to target main-frame requests. Its action redirects matching navigation to `https://google.com`. ^[how-to/chrome-extension/README.md:56-84]

The source contrasts Manifest V3’s JSON rules with imperative JavaScript in Manifest V2, presenting the declarative approach as simple, safe, and performant and describing V3 as restricting what extensions can do. ^[how-to/chrome-extension/README.md:88-96]

## Installation and customization

To load the example locally, open `chrome://extensions/`, enable **Developer mode**, select **Load unpacked**, and choose the `bypass-sharepoint` directory. Visiting the matching SharePoint URL then tests the redirect. ^[how-to/chrome-extension/README.md:100-108]

To customize the redirect, change `redirect.url` in `rules.json`. To target a different domain, update both `condition.regexFilter` and the manifest’s `host_permissions`. After saving changes, click **Reload** for the extension at `chrome://extensions/`. ^[how-to/chrome-extension/README.md:112-142]

## Sources

- [Chrome extension example and guide](how-to/chrome-extension/README.md)
