# USOS Checker — Design Overview

Describes `usoschecker-design.html` (Design Prototype v2).

## Project

USOS Checker is a mobile-first companion app for students of universities that use USOS. It shows the timetable and grades and tells the student what changed (room changes, new grades, schedule updates).

The HTML file is a single-file, clickable prototype with no build step and no dependencies. It runs on hard-coded sample data and has no USOS connection ("Sample content · No USOS connection").

## Structure

Bottom navigation with five tabs:

| Tab | Purpose |
|---|---|
| **Today** | Next class card, "Up next" list, "Needs attention" (latest changes) |
| **Plan** | Week navigation, 7-day strip with a dot on days that have classes, class list for the selected day, swipe to change week |
| **Grades** | Semester select, search by course or teacher, rows with Wykład / Ćwiczenia / Laboratorium grades, "NEW" markers |
| **Changes** | Filters All / Grades / Timetable (with counts), list of detected changes |
| **More** | Grouped tools: Updates, Student (ID, documents, attendance, payments), University (news, campus), App & tools (settings, GPA calculator, API catalog) |

Details (class, course components, change, tool) open in a **drawer**: a right-hand side panel on desktop and a bottom sheet on narrow screens (≤640 px).

## Visual design

- **Theme:** dark only, pure black (`#000`) background with near-black surfaces (`#090b09`, `#101310`) and thin 1 px dividers.
- **Accent:** a single green (`#51cf83`). It is used only for the active tab indicator, the next-class edge, the "new/primary" dots and focus rings. Everything else is neutral grey.
- **Type:** system sans (Inter first). Small, dense sizes (11–14 px). Section headings are uppercase and letter-spaced. The only large text is the next-class title (up to 28 px). Times and grades use tabular numerals.
- **Layout:** one centered column (max 790 px, Grades 440 px). Content is plain lists with hairline separators instead of heavy cards. The only card is the "next class" block.
- **Interaction:** whole rows are tappable and show a chevron. Hover and press feedback is subtle (background tint, 2 px shift). Toasts confirm sample actions.
- **Accessibility:** visible `:focus-visible` outlines, `aria-label` / `aria-current` / `aria-pressed`, a modal dialog with focus return, `prefers-reduced-motion` support, and safe-area insets for the bottom nav.

## Screens: what you see

Every screen is a black page with a single centered column. The bottom bar is always visible, with a thin top border. The active tab has a short green line above its label and brighter text.

### Today
1. **Next class card.** It is the only card in the app: dark panel, rounded corners, green left edge. The small label "NEXT CLASS" sits at the top. Under it is a large class title on the left and the time (`14:15–15:45`) with a round chevron button on the right. The last line shows `Room 204`.
2. **UP NEXT.** Small grey heading with a "Full plan →" link. Below it are up to two rows: title and room on the left, time and chevron on the right.
3. **NEEDS ATTENTION.** Heading with an "All changes →" link. Below it are two rows, each with a small dot (green for the room change, grey otherwise), a bold title ("Room changed") and a grey line of detail ("Mathematics · 204 → 108").

### Plan
- A row with two square arrow buttons (previous and next week). Between them is the date range (`20 Oct–26 Oct`) and, when the week is not the current one, a "This week" link.
- A strip of 7 weekday buttons (Mon 20 … Sun 26). The selected day has a lighter background and border. A tiny dot under a day means it has classes (green if that day is selected).
- Under the strip is the list of that day's classes (title and room on the left, time on the right). A day without classes shows "No classes scheduled."

### Grades
- Top row: a semester dropdown on the left, a search icon and a "⋯" menu (GPA calculator, Refresh grades) on the right. The search icon opens a text field under the row.
- The list is narrower than other screens. Each row is a course name followed by three small columns, `Wyk.` / `Ćw.` / `Lab.`. Each column has a tiny grey label above a bold grade, for example `4.5`. A missing grade is shown as a grey `—`. A new grade has a small green dot to the left of it, and a new course has a "NEW" label next to its name.

### Changes
- Three text tabs across the full width: **All**, **Grades 1**, **Timetable 2**. The active tab is white and bold, the others are grey, and the counts are tiny.
- Below is the same type of row as "Needs attention", with a relative time ("Recently", "Today", "Yesterday") on the right.

### More
- A plain menu with grey uppercase group headings (UPDATES, STUDENT, UNIVERSITY, APP & TOOLS). Each row has a small line icon, a title with a one-line description and a chevron.

### Detail drawer
- It slides in from the right on wide screens and rises from the bottom on phones, over a dimmed background. At the top are a small uppercase label (type of class, COURSE, MORE), a large title and a round close button.
- Next come a grey subtitle and a two-column list of facts (label on the left, value on the right). Course drawers list each component with a bordered grade box instead.
- At the bottom are action buttons, with the primary one marked by a green border on hover (for example "View in Plan", "GPA calculator").

## UX

- **Main idea:** open the app and see the next thing you need at a glance. Today answers "where do I go next?" and "did anything change?". The other tabs hold the full data.
- **Navigation is shallow:** five tabs and one drawer layer. There are no nested pages. Links such as "Full plan →" and "All changes →" jump to the relevant tab.
- **Details on demand:** lists stay short and show only the key data (title, room, time, grade). Everything else is one tap away in the drawer. Tapping a change in the list opens a drawer that links back to the affected class or grade.
- **Changes are highlighted with restraint:** green appears only for what is new or important (a dot, a "NEW" label, the active tab). Everything else is grey, so highlighted items stand out.
- **Quick actions:** swipe the day strip to change week, search by course or teacher on Grades, and close the drawer with Esc, a tap on the dimmed area, or the close button.
- **Feedback:** a short toast appears at the bottom after sample actions (refresh, semester change).
- **Empty states** are plain one-line grey messages.

## Implementation notes

- State lives in one `state` object. Each tab has a `render*()` function that rewrites `<main>` through template strings. Clicks are handled by a single delegated listener using `data-*` attributes.
- Data is two arrays: `courses` (timetable and grade parts) and `updates` (changes). Dates are computed relative to today.
- Interface text is in English. Grade component names stay in Polish, as in USOS.

## Known gaps

- `planMenu` is referenced in the JS (menu toggle, export `.ics`, refresh, find a class), but the Plan screen renders no menu button, so that code is currently unreachable.
- The `More` tools open placeholder text drawers only.
- There is no light theme and no language switch.
