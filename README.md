# cow-scripts

Small client-side tweaks, user scripts, and CSS modifications for Remember The Milk.

> This product uses the Remember The Milk API but is not endorsed or certified by Remember The Milk.

---

## What this is

A collection of small improvements to the Remember The Milk interface, running entirely client-side — user scripts, CSS, bookmarklets, and MilkScripts. No backend, no data collection, no new app. Just useful additions on top of what RTM already does.

Free and open-source under the MIT License.

---

## Contents

| Path | Description |
|---|---|
| `scripts/` | MilkScript automations (run inside RTM) |
| `styles/` | CSS / Stylus modifications |
| `bookmarklets/` | Browser bookmarklets |
| `docs/` | Usage documentation |

---

## Scripts

### `scripts/sync-parent-due-date.js` *(work in progress)*

**Idea:** [RTM Community Forum — Show parent task at earliest subtask due date](https://www.rememberthemilk.com/forums/ideas/31540/)

Automatically sets the due date of every parent (container) task to the earliest due date found among its leaf subtasks — recursively across any depth of nesting.

**How it works:**
- Leaf tasks (no children) are treated as the real actionable items — their due dates are the source of truth
- Container tasks (with children) get their due date derived from the earliest leaf in their subtree
- Runs bottom-up, so intermediate levels are also updated correctly

**Debug flags** (top of script):
```js
const DEBUG_TAG = "RTMdev"; // only process trees whose root has this tag; set "" for all
const AUDIT_TAG = "ai";     // tag every changed task for review; set "" to disable
```

**Usage:** Paste into RTM → Tools → Scripts, or run via the RTM API.

---

## Installation

### MilkScripts
Copy the script content into Remember The Milk → Tools → Scripts → New Script.

### User scripts (Tampermonkey / Violentmonkey)
Install [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/), then click the `.user.js` file link and confirm install.

### CSS
Use a browser extension like Stylus to apply custom stylesheets.

---

## Contributing

Issues and PRs welcome. Please keep changes client-side only and RTM ToS compliant.

---

## Links

- [Remember The Milk](https://www.rememberthemilk.com/)
- [RTM API docs](https://www.rememberthemilk.com/services/api/overview.rtm)
- [MilkScript docs](https://www.rememberthemilk.com/services/milkscript/)
- [RTM API Terms of Use](https://www.rememberthemilk.com/services/api/terms.rtm)
