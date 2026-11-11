---
title: Request Header Modification
summary: The modifyHeaders action can set request headers, including User-Agent and custom headers.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:36.407Z"
updatedAt: "2026-11-11T10:54:36.407Z"
tags:
  - network-rules
  - http-headers
aliases:
  - request-header-modification
  - RHM
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Request Header Modification

Request header modification uses the `modifyHeaders` action in [[Declarative Network Request Rules]] to set HTTP request headers for URLs matching a rule’s condition. The source demonstrates replacing `User-Agent` and adding a custom header in a Chrome extension. ^[how-to/chrome-extension/README.md:162-202]

## Rule structure

A rule includes an `id`, a `priority`, an `action`, and a `condition`. For header modification, `action.type` is `modifyHeaders`, and `requestHeaders` specifies the header name, operation, and value. The examples use `"operation": "set"` and a `regexFilter` to select matching URLs. ^[how-to/chrome-extension/README.md:75-80, how-to/chrome-extension/README.md:162-202]

The following rule sets `User-Agent` to `CustomBot/1.0` for requests matching `https://api.example.com/`. ^[how-to/chrome-extension/README.md:162-181]

```json
{
  "id": 3,
  "priority": 1,
  "action": {
    "type": "modifyHeaders",
    "requestHeaders": [
      {
        "header": "User-Agent",
        "operation": "set",
        "value": "CustomBot/1.0"
      }
    ]
  },
  "condition": {
    "regexFilter": "^https://api\\.example\\.com/.*"
  }
}
```

The same structure can add a custom header: the source sets `X-Custom-Header` to `my-value` for URLs matching `^https://example\\.com/.*`. In a JSON regex string, a literal dot is escaped as `\\.`. ^[how-to/chrome-extension/README.md:183-215]

## Extension configuration

In the source’s [[Chrome Extensions with Manifest V3|Manifest V3]] setup, `manifest.json` declares the `declarativeNetRequestWithHostAccess` permission, defines [[Extension Host Permissions|host permissions]], and registers an enabled rules file through `declarative_net_request.rule_resources`. The rules themselves reside in `rules.json`. ^[how-to/chrome-extension/README.md:24-52, how-to/chrome-extension/README.md:54-73]

When changing the target domain, update the rule’s `regexFilter` and the manifest’s `host_permissions`. After saving changes, open `chrome://extensions/` and click **Reload** on the extension. ^[how-to/chrome-extension/README.md:123-142]

## Sources

- [how-to/chrome-extension/README.md](how-to/chrome-extension/README.md)
