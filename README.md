# todoapp-subtask-due-date-for-parent

A MilkScript that automatically sets the due date of a parent task to the earliest due date found among its subtasks — recursively, across any depth of nesting.

> This product uses the Remember The Milk API but is not endorsed or certified by Remember The Milk.

---

## Why todoapp-subtask-due-date-for-parent?

In Remember The Milk, subtasks are separate entities — they only carry a link to their parent. This means a parent task has no due date of its own unless you set one manually, and that date goes stale every time you complete a subtask.

[samzu on the RTM Ideas Forum](https://www.rememberthemilk.com/forums/ideas/31540/) described the problem well:

> I have a lot of tasks with subtasks. I give the subtasks due dates, but no due date to the parent task — as this is changing every time I complete a subtask and I don't want to change it manually all the time. In my lists I would like to see the parent task at the due date of the subtask with the earliest due date.

Since subtasks and parent tasks are separate objects, this is not a display problem — it requires actual automation. MilkScript is the only native way to do this inside RTM.

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/O4O41Z5AZU)

*One less thing to update manually. The tools that keep it that way run on coffee.*

---

## What it does

The script treats every task without children as a real actionable item (a leaf), and every task with children as a container. It then:

1. Walks each container's subtree recursively — finding the earliest due date among all leaf descendants, at any depth
2. Sets that date on the container task
3. Works bottom-up, so intermediate levels (subtasks that themselves have subtasks) are also updated correctly

---

## Scoped run — test before you commit

By default, the script runs on all your incomplete tasks. If you want to test it first, or intentionally limit it to a specific subset, add the tag `sync-preview` to the parent tasks you want to process.

When the script detects that any task has the `sync-preview` tag, it switches to scoped mode and only processes parents with that tag. When no task has the tag, it runs on everything.

**Typical flow for a first run:**

1. Add `sync-preview` to 2–3 parent tasks you want to test on
2. Run the script — only those trees will be updated
3. Check the results in RTM
4. If everything looks right, remove the tag from all tasks and run again — this time on everything
5. For future runs, just run the script without any `sync-preview` tags

The script log shows the active mode at the top (`SCOPED` or `FULL`) so you always know which one ran.

---

## Installation

1. Open Remember The Milk → Tools → Scripts → New Script
2. Paste the contents of `sync-parent-due-date.milkscript`
3. Save and run manually, or trigger via an external automation (IFTTT, Zapier, Make, Claude Code, etc.)

The script file will be added here once testing is complete.

---

## Contributing

Issues and PRs welcome.

---

## License

MIT — see [LICENSE](LICENSE).
