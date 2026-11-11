---
title: Declarative Request Blocking
summary: A block action prevents requests whose URLs match the rule's condition.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:55.167Z"
updatedAt: "2026-11-11T10:54:55.167Z"
tags:
  - network-rules
  - request-blocking
aliases:
  - declarative-request-blocking
  - DRB
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Declarative Request Blocking

Declarative request blocking uses JSON rules in a [[Chrome Extensions with Manifest V3|Manifest V3 extension]] to block requests whose URLs match a specified condition. Blocking is one of the actions supported by [[Declarative Network Request Rules]], alongside redirection and header modification. ^[how-to/chrome-extension/README.md:75-80, how-to/chrome-extension/README.md:94-96, how-to/chrome-extension/README.md:148-160]

## Blocking rule

The following rule blocks requests matching `https://blokovana-stranka.com/` and any path beneath it. The `action.type` selects blocking, while `condition.regexFilter` defines the URL pattern. ^[how-to/chrome-extension/README.md:148-160]

```json
{
  "id": 2,
  "priority": 1,
  "action": {
    "type": "block"
  },
  "condition": {
    "regexFilter": "^https://blokovana-stranka\\.com/.*"
  }
}
```

Each rule has a unique `id`, a `priority`, an `action`, and a `condition`. In a JSON string, the literal dot in the domain is escaped as `\\.`. ^[how-to/chrome-extension/README.md:75-80, how-to/chrome-extension/README.md:206-215]

## Extension configuration

The source extension stores network rules in `rules.json`. Its `manifest.json` enables `declarativeNetRequestWithHostAccess`, declares [[Extension Host Permissions|host permissions]], and registers the rule file through `declarative_net_request.rule_resources`. When adapting the example to another domain, update both the rule’s URL filter and the manifest’s host permissions. ^[how-to/chrome-extension/README.md:24-40, how-to/chrome-extension/README.md:123-138]

To load the extension locally, open `chrome://extensions/`, enable **Developer mode**, choose **Load unpacked**, and select the extension directory. After saving configuration or rule changes, click **Reload** on the extension. ^[how-to/chrome-extension/README.md:100-106, how-to/chrome-extension/README.md:140-142]

## Sources

- [Chrome Extension s deklarativními pravidly](how-to/chrome-extension/README.md)
