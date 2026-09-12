# Changelog

## v1.2
Extensive testing against real-world scripts — 9 community templates from the [Tydorius JanitorAI_Scripts repo](https://github.com/Tydorius/JanitorAI_Scripts) and 2 scripts from JanitorAI's own official help center — surfaced several real bugs, both in the analyzer's judgment and in the one-click auto-fix engine itself. All are fixed and re-verified.

**Auto-fix correctness (the important ones):**
- Fixed: the `parseInt` auto-fix silently failed to add a radix on any call whose argument itself contained a function call (e.g. `parseInt(str.slice(0, 2))`) — a very common real-world shape. It now correctly handles nested calls.
- Fixed: the `== NaN` / `=== NaN` auto-fix could produce outright broken code on anything more complex than a bare variable — e.g. `parseFloat(str) === NaN` was rewritten into the nonsensical `parseFloat(isNaN(str))`, and array/property access could produce invalid syntax. Rewritten to correctly handle function calls, indexing, and member access on either side of the comparison.
- Hardened the `JSON.parse` guard auto-fix against the same class of nested-argument issue.

**Analyzer accuracy — reducing false positives on genuinely safe patterns:**
- The standard defensive-guard idiom (`x = x || fallback`, and now also the ternary form `x = (typeof x === "string") ? x : fallback`, and the if-statement form `if (!x) x = fallback;`) is no longer wrongly flagged as a destructive read-only write or full-field-replacement. One of these was found directly contradicting the documented behavior of JanitorAI's own official "Emotion Engine" script, which states it is append-only and never overwrites.
- `typeof context.chat.someField === "string"` style feature-detection (checking whether a field exists before using it) is no longer flagged as an unknown-field error — this can never throw and is a deliberate, safe pattern, found in JanitorAI's own official "Advanced Lorebook v12" script.
- The "append pattern — stacking drift" warning was rebuilt to check each individual append's own guard condition instead of one whole-script regex for "does a guard exist anywhere." Previously, a script with one guarded append anywhere would silently downgrade every other unrelated, genuinely unguarded append to an informational note — including real `if (day >= 20)`-style one-shot-event bugs that fire on every turn forever instead of once. Verified this catches the real bug in a 466-line community lorebook template while still correctly clearing a 735-line script that uses safe, per-turn relevance-gated injection.

Also corrected a `NaN`-comparison detection rule that had never actually been able to fire due to a regex boundary bug (separate from the auto-fix issue above).

## v1.1
- Added proper mobile layout: collapsible header menu, swipeable Script/Findings views, larger touch targets.
- Added one-click auto-fix for common mistakes (smart/curly quotes, `.length()`, `parseInt` without a radix, `== NaN` comparisons, misplaced `"use worker"`, unguarded `JSON.parse`), with a before/after diff preview before bulk-applying and one-click undo.
- Added a plain-language health summary at the top of the Findings tab.
- Added small in-editor gutter markers on lines with an available auto-fix.
- Added a dismissible first-time tip pointing at the new fix buttons.
- Fixed: the desktop two-pane layout could render as a broken single column depending on browser/zoom due to a CSS grid issue.
- Fixed: the "`NaN` compared with `==`/`===`" check never actually triggered due to a regex bug.
- Removed a modern-only CSS selector for wider browser compatibility.

## v1.0
- Initial release: static analyzer, sandboxed script runner, chat simulator, multi-turn soak testing, scenario suite, and exportable reports.
