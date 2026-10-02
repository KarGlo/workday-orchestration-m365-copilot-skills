---
name: workday-orchestration-expressions
description: Write, explain, fix and convert Workday Orchestrate expressions in Orchestration Builder — Expression Builder pill and Advanced Mode syntax, data("Step","output") references, string interpolation, if/else, JSONPath and XPath accessors, type casting with asJSON/asXML, iterators, launch parameters (lp), integration system attributes (intsys), app attributes (attrstore), context functions, and Create Text Template syntax ({{#each}}, {{#if}}, aliases, functions). Use for any question about an expression, a function name or signature, extracting a value from a JSON or XML response, building a request body or output file, or an expression that fails, returns empty or has the wrong type.
---

# Workday Orchestrate expressions

## Reference files

These `.txt` files are packaged next to this skill (in its `references` folder) or, when the skill was
uploaded as a single `SKILL.md`, attached to the agent's knowledge under the same file names.
Look them up by file name in whichever place is available.

- `syntax.txt` — Expression Builder modes, how to reference step outputs, interpolation,
  conditionals, types, JSONPath and XPath support, text template syntax, usage statistics.
- `functions-global.txt` — every global function (attrstore, bp, context, date,
  datetime, documents, InstanceRef, intsys, list, localtime, lp, map, mapping, math, no-qualifier,
  random, resource, system, zoneddatetime).
- `functions-strings-text.txt` — String, Text, StringList, StringMap, Boolean.
- `functions-structured-data.txt` — Data, Json, JsonKeyValue, Xml, Csv, CsvRow,
  DocumentAccessor, FileInfo(List), HttpHeaders, HttpQueryParams, InstanceReference(List),
  Iterator, JoinResiduals, MatchedWith, ProcessingError.
- `functions-numbers-dates-collections.txt` — BigDecimal, Number, NumberList/Map,
  BooleanList/Map, Date, DateList/Map, LocalDateTime(List/Map), LocalTime(List/Map),
  ZonedDateTime(List/Map).

## Procedure

1. **Establish the input type.** Ask or infer what the value is: a raw HTTP/API response
   (DataType — cast with `asJSON()` / `asXML()` first), a String, a launch parameter, a loop item.
   A function exists only for the type it is appended to.
2. **Find the function in the catalogue files.** Search by name or by return type. Quote the exact
   signature. **Never invent a function name or argument order.** If nothing in the catalogue fits,
   say so and suggest Function Explorer in Orchestration Builder.
3. **Write the expression twice** when the user builds it in the UI:
   - Advanced Mode text in a code block, e.g.
     `data.GetWorker.response.asJSON().stringAtJsonPathWithDefault("$.data[0].descriptor", "")`
   - Pill-mode clicks: plus button > Orchestration Data from Orchestration Steps > step > output >
     Append Function > function > arguments.
4. **Choose safe accessors by default.** `stringAtJsonPath`, `numberAtJsonPath`,
   `booleanAtJsonPath`, `objectAtJsonPath` and the XPath `...AtXPath` family throw when the value
   is missing. Use the `...WithDefault` / `...OrEmptyString` variant unless a missing value must
   fail the run — then say that the failure is intended.
5. **Check the path syntax** against the supported and unsupported JSONPath and XPath tables in
   `syntax.txt` (for example negative indices and root-referencing filters are not
   supported; at most 10,000 primitives per JSONPath).
6. **Mind memory.** Avoid `toString()` on large file-backed documents; iterate with
   `iterator(...)` and a Loop instead of materialising big strings.
7. **Explain the result type** of the final expression and where it can be used (for example a
   String output can feed a query parameter; an iterator feeds a Loop).

## Conventions to apply

- Reference step outputs as `data.StepName.output`; both that and `data("StepName","output")` are
  valid and equivalent.
- Interpolate with `s"${...}${...}"`; triple quotes `s"""..."""` are also valid.
- Write conditions directly; `if (x) true else false` is redundant.
- Launch parameter and attribute names are case- and space-sensitive: they must match the
  integration system configuration exactly.
- `attrstore.*Value("name")` throws if the attribute is missing; use it only for attributes the
  app defines and every tenant has a value for.
- In text templates use `{{#each ... as name}}` and `{{item.name...}}` for readable nested loops,
  and `{{#alias}}` for expensive sub-expressions used more than once.
- Split Create Values into independent and dependent groups for parallel evaluation.

## When the expression fails

- "Value not found" / exception at runtime → a non-default accessor met a missing value, or the
  JSONPath/XPath doesn't match. Re-check the path on a real response from the Debug tool or Run
  Logs.
- Wrong type / function not offered → the value wasn't cast (`asJSON()`/`asXML()`) or is a
  different type than assumed.
- Empty output from XPath → the path selects a fragment; only iterator, fragmentAtXPath and
  countItemsAtXPath return fragments.
- Namespace errors in XPath → declare the namespace prefix in the orchestration's settings.

For error handling around expressions see the `workday-orchestration-errors-debugging` skill.
