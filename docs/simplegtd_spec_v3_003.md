# SimpleGTD — Specification

## Pending

Open items to resolve before this spec is final.

1. Write the non-negotiables checklist.
2. Define capture.
3. Define what should not persist.
4. Verify `functional-indexing` on npm.

## Non-negotiables

*Placeholder.*

## Sections

Tasks live in sections, stacked vertically in a single column. A section has a name and holds an ordered set of tasks. Sections support full CRUD. Deleting a section takes its tasks with it.

A section can be collapsed so only its header remains.

## Tasks

A task is a line of text, belonging to one section. Tasks support full CRUD. A task can be toggled done and undone, moved to another section, and reordered within its section.

Tasks carry no due date, tags, notes, or subtasks. The app is a capture surface, not a project manager.

Deletion is permanent. It must be protected against accidental deletion.

## Capture

*Placeholder.*

## Search

Tasks can be searched across all sections from anywhere in the app. Selecting a result brings the user to that task.

## Persistence

State is persisted to localStorage. Everything persists by default — user data and interface state alike — so an interrupted session loses as little as possible.

What should not persist: *placeholder.*

## Data model

Two flat arrays, one of sections and one of tasks, each task holding the identifier of its section. No nesting.

Order is computed with the `functional-indexing` library, so moving a section or task updates only that record's order key rather than every sibling's.

Performance is not a concern unless an approach is orders of magnitude off, or worse than quadratic.

The model is expected to change. Where it conflicts with the interface described above, the interface wins.

## Out of scope

Features not described in this spec are out of scope — due dates, reminders, tags, projects, notes, attachments, subtasks, recurring tasks, and the like. This is not license to skip ordinary correctness or usability.

Archiving is planned for a later build and is not part of this one.
