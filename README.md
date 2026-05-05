# todoapp-subtask-due-date-for-parent

A MilkScript that automatically sets the due date of a parent task to the earliest due date found among its subtasks — recursively, across any depth of nesting.

> This product uses the Remember The Milk API but is not endorsed or certified by Remember The Milk.

---

## Why todoapp-subtask-due-date-for-parent?

In Remember The Milk, subtasks are separate entities — they only carry a link to their parent. This means a parent task has no due date of its own unless you set one manually, and that date goes stale every time you complete a subtask.

[samzu on the RTM Ideas Forum](https://www.rememberthemilk.com/forums/ideas/31540/) described the problem well:

> I have a lot of tasks with subtasks. I give the subtasks due dates, but no due date to the parent task — as this is changing every time I complete a subtask and I don't want to change it manually all the time. In my lists I would like to see the parent task at the due date of the subtask with the earliest due date.

Since subtasks and parent tasks are separate objects, this is not a display problem — it requires actual automation. MilkScript is the only native way to do this inside RTM.

---

## What it does

The script treats every task without children as a real actionable item (a leaf), and every task with children as a container. It then:

1. Walks each container's subtree recursively — finding the earliest due date among all leaf descendants, at any depth
2. Sets that date on the container task
3. Works bottom-up, so intermediate levels (subtasks that themselves have subtasks) are also updated correctly

Two flags at the top of the script control debug and audit behavior:

```js
const DEBUG_TAG = "RTMdev"; // only process trees whose root has this tag; "" = run on all tasks
const AUDIT_TAG = "ai";     // tag every changed task for easy review; "" = disable
```

With `DEBUG_TAG = "RTMdev"`, the script only touches task trees where the root task has the `RTMdev` tag. The subtasks themselves do not need the tag. Remove the tag from the constant (set `""`) when you're ready to run on everything.

With `AUDIT_TAG = "ai"`, every task whose due date was actually changed gets tagged `ai`. Use the Smart List filter `tag:ai` in RTM to review what the script touched, then remove the tag when you're satisfied.

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
