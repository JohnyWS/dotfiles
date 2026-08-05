# intent-log

Use this file only for changes that materially affect scope, portability, or risk.

Log entries are expected when intent impact is Major, or when purpose/support/risk boundaries move.

Format:

- YYYY-MM-DD: short note. Intent: #anchor

Examples:

- 2026-04-12: added root intent anchors and PR references. Intent: #repo-purpose
- 2026-04-12: documented bootstrap/apply breakage as high risk. Intent: #risk-boundaries
- 2026-08-05: native Windows promoted from "not validated" to first-class alongside WSL; both must hold for a change to be done. Intent: #supported-environments
- 2026-08-05: added context-based Git identity switching (default vs private by repo context; selecting value stays render-time-local). Intent: #identity-switching
- 2026-08-05: stated commit signing must work in both environments via each OS's native 1Password mechanism, sharing one signing key. Intent: #supported-environments #commit-signing #risk-boundaries