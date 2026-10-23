# USOS Checker — Today Screen Structure (Cyan prototype)

Source: `usoschecker-design-cyan.html`. This describes **what information and elements the screen must contain**, not how it looks or is implemented. The prototype shows only the **Today** tab; other tabs are placeholders.

## App-level

- Mobile-first companion app for USOS students: timetable + grades + what changed.
- Bottom navigation with 5 tabs: **Today** (default), **Plan**, **Grades**, **Changes**, **More**.
- Short toast/snackbar confirms actions (prototype uses it as a stand-in for navigation).
- Prototype data is sample content, with no USOS connection.

## Today screen — 3 blocks

### 1. Next class (primary block, most prominent)
Tappable; opens class details.
- Label: "Next class"
- Course name (e.g. "Programming")
- Time range (e.g. `14:15–15:45`) and room (e.g. `Room 204`)
- Sub-list **"Later today"**: remaining classes of the day, each with course name, start time and room (e.g. Mathematics · 16:00 · 108; Physics lab · 18:00 · 12)

### 2. Needs attention (latest changes: timetable and grades in one list)
Section label: "Needs attention". Each item is tappable and shows:
- Change type as the title: "Room changed", "New grade"
- Detail line: course (+ what changed or which component), e.g. `Mathematics · 204 → 108`, `Algorithms · Laboratory`
- Right side: relative time ("Today") for timetable changes, or the **grade value** (`4.5`) for grade changes
- Link "All changes →" leads to the Changes tab

### 3. This week (overview only)
- Label with the current week's date range (e.g. "This week · 19–25 Oct"); link "Full plan →" leads to the Plan tab
- 7 day buttons (Mon–Sun), each with weekday, day number and one dot per class that day (no dots = no classes; no course names here)
- The current day is marked as today

## Data the screen needs

- Today's classes: course, start/end time, room (ordered; first upcoming = "next class")
- Recent changes: type (room/time change, new grade, etc.), course, details (old → new value, or grade + component), timestamp
- Class count per day for the current week

## Out of scope in this prototype

Plan, Grades, Changes, More tabs; detail views for classes/changes; real data; settings.
