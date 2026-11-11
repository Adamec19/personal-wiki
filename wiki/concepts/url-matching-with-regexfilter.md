---
title: URL Matching with regexFilter
summary: Network rules use regular expressions to match URLs and resourceTypes to restrict matching to resources such as main_frame navigations.
sources:
  - how-to/chrome-extension/README.md
kind: concept
createdAt: "2026-11-11T10:54:31.528Z"
updatedAt: "2026-11-11T10:54:31.528Z"
tags:
  - network-rules
  - regular-expressions
aliases:
  - url-matching-with-regexfilter
  - UMWR
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# URL Matching with regexFilter

`regexFilter` specifies which URLs a declarative network rule matches in a [[Chrome Extensions with Manifest V3|Manifest V3 extension]]. It belongs to the rule’s `condition` object; the separate `action` object defines what happens to matching requests, such as redirection, blocking, or header modification. ^[how-to/chrome-extension/README.md:54-80]

## Matching a specific URL

The following condition matches the HTTPS SharePoint URL `/sites/Directintranet`, allowing an optional trailing slash and an optional query string or fragment. The `resourceTypes` setting limits the rule to `main_frame` requests. ^[how-to/chrome-extension/README.md:67-70]

```json
"condition": {
  "regexFilter": "^https://directpojistovnaas\\.sharepoint\\.com/sites/Directintranet/?([?#].*)?$",
  "resourceTypes": ["main_frame"]
}
```

The leading `^` and trailing `$` anchor the match to the complete URL. Within the pattern, `/?` allows an optional slash, while `([?#].*)?` allows an optional suffix beginning with `?` or `#`. In the source example, this condition accompanies a [[Declarative URL Redirection|redirect action]] whose destination is `https://google.com`. ^[how-to/chrome-extension/README.md:61-70]

## Common patterns

The source provides patterns for matching a domain, SharePoint subdomains, PDF URLs, and API subdomains. Literal dots are written as `\\.` inside the JSON string. ^[how-to/chrome-extension/README.md:206-215]

| `regexFilter` pattern in JSON | Matches |
|---|---|
| `^https://example\\.com/.*` | HTTPS URLs on `example.com` |
| `^https://.*\\.sharepoint\\.com/.*` | HTTPS URLs on SharePoint subdomains |
| `\\.pdf$` | URLs ending in `.pdf` |
| `^https://api\\..*` | HTTPS URLs beginning with `api.` |

## Updating a matching rule

To target another domain, change `condition.regexFilter` in `rules.json` and update the corresponding [[Extension Host Permissions|host permissions]] in `manifest.json`. After saving the changes, open `chrome://extensions/` and click **Reload** for the extension. ^[how-to/chrome-extension/README.md:123-142]

URL matching is separate from the action performed. The source uses `regexFilter` conditions with [[Declarative Request Blocking|blocking]] and [[Request Header Modification|request header modification]], including setting `User-Agent` or `X-Custom-Header`. ^[how-to/chrome-extension/README.md:146-202]

## Sources

- [how-to/chrome-extension/README.md](how-to/chrome-extension/README.md)
