---
title: Declarative Network Request Rules
summary: JSON rules define conditions and actions for redirecting requests, blocking requests, or modifying headers.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:20.846Z"
updatedAt: "2026-11-11T10:54:20.846Z"
tags:
  - chrome-extensions
  - network-rules
aliases:
  - declarative-network-request-rules
  - DNRR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Declarative Network Request Rules

Declarative network request rules describe how a Chrome extension should handle matching requests using JSON. In [[Chrome Extensions with Manifest V3|Manifest V3]], these rules can redirect requests, block them, or modify request headers. The source contrasts this declarative approach with imperative JavaScript logic. ^[how-to/chrome-extension/README.md:75-80, how-to/chrome-extension/README.md:94-96]

## Registering rules

The extension’s `manifest.json` enables network rules through `declarativeNetRequestWithHostAccess`, declares the relevant domains through [[Extension Host Permissions|host permissions]], and registers a rules file under `declarative_net_request.rule_resources`. The `enabled` field activates the registered ruleset. ^[how-to/chrome-extension/README.md:24-40, how-to/chrome-extension/README.md:50-52]

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

## Rule structure

Each rule has a unique `id`, a `priority`, an `action` describing what should happen, and a `condition` describing when it applies. Conditions can use `regexFilter` and `resourceTypes` to select matching requests. ^[how-to/chrome-extension/README.md:75-80]

The following `rules.json` example implements [[Declarative URL Redirection]]: it redirects the specified SharePoint intranet URL to Google. Its condition uses a regular expression and restricts the resource type to `main_frame`. ^[how-to/chrome-extension/README.md:54-84]

```json
[
  {
    "id": 1,
    "priority": 1,
    "action": {
      "type": "redirect",
      "redirect": {
        "url": "https://google.com"
      }
    },
    "condition": {
      "regexFilter": "^https://directpojistovnaas\\.sharepoint\\.com/sites/Directintranet/?([?#].*)?$",
      "resourceTypes": ["main_frame"]
    }
  }
]
```

## Other actions

[[Declarative Request Blocking]] uses an action with `"type": "block"`. [[Request Header Modification]] uses `"type": "modifyHeaders"` with a `requestHeaders` array; the source demonstrates setting `User-Agent` to `CustomBot/1.0` and setting an `X-Custom-Header` value. ^[how-to/chrome-extension/README.md:146-202]

## Editing and testing

To change a redirect, update `action.redirect.url`. To target another domain, update both the rule’s `regexFilter` and the manifest’s `host_permissions`. Literal dots in the regular expression are written as `\\.` inside the JSON string. ^[how-to/chrome-extension/README.md:112-138, how-to/chrome-extension/README.md:206-215]

For local testing, open `chrome://extensions/`, enable **Developer mode**, choose **Load unpacked**, and select the extension folder. After saving changes, click **Reload** on the extension and visit the matching URL to check the behavior. ^[how-to/chrome-extension/README.md:100-108, how-to/chrome-extension/README.md:140-142]

## Sources

- [chrome-extension — Chrome Extension s deklarativními pravidly](how-to/chrome-extension/README.md)
