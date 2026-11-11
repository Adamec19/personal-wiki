---
title: Declarative URL Redirection
summary: A redirect action sends matching navigations to a specified destination, illustrated by redirecting a SharePoint intranet URL to Google.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:33.986Z"
updatedAt: "2026-11-11T10:54:33.986Z"
tags:
  - network-rules
  - redirection
aliases:
  - declarative-url-redirection
  - DUR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Declarative URL Redirection

Declarative URL redirection uses JSON rules to redirect matching browser requests to a specified URL. In a [[Chrome Extensions with Manifest V3|Manifest V3 extension]], the manifest registers a rules file, while each rule defines the redirect action and the conditions under which it applies. ^[how-to/chrome-extension/README.md:24-40, how-to/chrome-extension/README.md:54-80]

## Extension configuration

The extension requests `declarativeNetRequestWithHostAccess`, declares the source domain in `host_permissions`, and registers an enabled ruleset through `declarative_net_request.rule_resources`. This connects [[Extension Host Permissions]] with the file containing the [[Declarative Network Request Rules|network rules]]. ^[how-to/chrome-extension/README.md:24-52]

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

## Redirect rule

In `rules.json`, `action.type` is set to `redirect`, and `action.redirect.url` specifies the destination. The example matches the SharePoint intranet URL and redirects it to `https://google.com`; its condition includes both a `regexFilter` and `resourceTypes: ["main_frame"]`. ^[how-to/chrome-extension/README.md:54-84]

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

The rule has a unique `id`, a `priority`, an `action`, and a `condition`. Literal dots in a domain pattern are escaped as `\\.` in the JSON string. Related actions include [[Declarative Request Blocking]] and [[Request Header Modification]]. ^[how-to/chrome-extension/README.md:75-80, how-to/chrome-extension/README.md:148-202, how-to/chrome-extension/README.md:206-215]

## Customization and testing

To change the destination, edit `action.redirect.url`. To change which source URLs match, edit `condition.regexFilter` and update `host_permissions` in the manifest for the new domain. After saving changes, reload the extension at `chrome://extensions/`. ^[how-to/chrome-extension/README.md:112-142]

For initial installation, enable **Developer mode** at `chrome://extensions/`, choose **Load unpacked**, and select the extension folder. Test the rule by visiting the matching SharePoint URL and checking that the browser redirects to the configured destination. ^[how-to/chrome-extension/README.md:100-108]

## Sources

- [chrome-extension — Chrome Extension s deklarativními pravidly](how-to/chrome-extension/README.md)
