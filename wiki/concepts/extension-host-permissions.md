---
title: Extension Host Permissions
summary: The example combines declarativeNetRequestWithHostAccess with host_permissions covering the SharePoint domain.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:25.780Z"
updatedAt: "2026-11-11T10:54:25.780Z"
tags:
  - chrome-extensions
  - permissions
aliases:
  - extension-host-permissions
  - EHP
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Extension Host Permissions

Host permissions specify the domains to which an extension’s network rules apply. In a [[Chrome Extensions with Manifest V3|Manifest V3 extension]], they are declared through `host_permissions` in `manifest.json`. The example pairs them with `declarativeNetRequestWithHostAccess`, which enables [[Declarative Network Request Rules|declarative network rules]]. ^[how-to/chrome-extension/README.md:24-52]

## Configuration

The example extension declares the following permission and host scope. Its manifest also registers an enabled ruleset stored in `rules.json`. ^[how-to/chrome-extension/README.md:24-40]

```json
{
  "permissions": ["declarativeNetRequestWithHostAccess"],
  "host_permissions": ["https://directpojistovnaas.sharepoint.com/*"]
}
```

The host permission identifies the domain covered by the extension, while the rule’s `condition` specifies when an action applies. In the example, `regexFilter` matches the SharePoint `/sites/Directintranet` URL, and `resourceTypes` restricts the rule to `main_frame`. The action performs a [[Declarative URL Redirection|redirect]] to `https://google.com`. ^[how-to/chrome-extension/README.md:50-84]

## Changing the Target Domain

To redirect a different domain, update both the rule’s `regexFilter` in `rules.json` and the corresponding `host_permissions` entry in `manifest.json`. The source illustrates this with a filter for `https://nova-domena.com/` and the host permission `https://nova-domena.com/*`. ^[how-to/chrome-extension/README.md:123-138]

After saving changes, open `chrome://extensions/` and click **Reload** on the extension to apply them. ^[how-to/chrome-extension/README.md:140-142]

## Sources

- [Chrome Extension s deklarativními pravidly](how-to/chrome-extension/README.md)
