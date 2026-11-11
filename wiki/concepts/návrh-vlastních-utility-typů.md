---
title: Návrh vlastních utility typů
summary: Vlastní utility typ má smysl pro opakující se pattern, jehož pojmenování zlepší čitelnost; přednost mají standardní utility, indexed access nebo satisfies.
sources:
  - how-to/typescript-cheat-sheet/04-utility-types.md
kind: concept
createdAt: "2026-11-11T11:04:18.778Z"
updatedAt: "2026-11-11T11:04:18.778Z"
tags:
  - typescript
  - návrh-typů
  - čitelnost-kódu
aliases:
  - návrh-vlastních-utility-typů
  - NVUT
confidence: 1
provenanceState: extracted
modelId: codex-cli-default
promptVersion: v7
---

# Návrh vlastních utility typů

Utility typy odvozují nové typy z existujících a snižují duplicitu. Neměly by však skrývat důležitý business kontrakt. Vlastní utility typ má smysl tehdy, když se určitý vzor opakuje a jeho pojmenování zlepší čitelnost. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-3, how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Nejdříve zvaž existující možnosti

Před vytvořením vlastního utility typu vyzkoušej standardní utility, [[TypeScript Indexed Access Types|indexed access]] nebo [[The satisfies operator|satisfies]]. Tyto možnosti mají při návrhu přednost před zavedením nové abstrakce. ^[how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

Standardní utility pokrývají například změny vlastností pomocí [[Partial, Required a Readonly]], výběr podmnožiny kontraktu pomocí [[Pick a Omit]] nebo odvození návratového typu a parametrů funkce pomocí [[ReturnType a Parameters]]. Odvozování z funkce je užitečné, pokud je funkce zdrojem pravdy a cílem je zabránit ručnímu duplikování její signatury. ^[how-to/typescript-cheat-sheet/04-utility-types.md:5-28, how-to/typescript-cheat-sheet/04-utility-types.md:44-57]

Pro kontrolu úplnosti klíčů a překlepů v objektu lze využít [[Record v kombinaci se satisfies]]. Ani takový požadavek proto sám o sobě nevyžaduje vlastní utility typ. ^[how-to/typescript-cheat-sheet/04-utility-types.md:30-42]

## Zachování významu kontraktu

Zkrácení zápisu nesmí nahradit přesný popis dat. `Partial` je vhodný například pro patch request, ale nemá sloužit jako náhrada přesného typu formuláře. Podobně `Pick` a `Omit` používej tehdy, když odvozený typ skutečně představuje podmnožinu původního kontraktu. ^[how-to/typescript-cheat-sheet/04-utility-types.md:19-28]

Při rozhodování o vlastní utilitě tedy posuzuj opakování vzoru i přínos názvu pro čitelnost a současně zachovej srozumitelnost business kontraktu. ^[how-to/typescript-cheat-sheet/04-utility-types.md:3-3, how-to/typescript-cheat-sheet/04-utility-types.md:77-79]

## Sources

- [Utility Types](how-to/typescript-cheat-sheet/04-utility-types.md)
