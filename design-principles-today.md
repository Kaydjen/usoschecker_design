# Today screen: design and UX principles

Applies to `usoschecker-design-cyan.html`. These are my own design reasoning, not checked against external research yet.

## Hierarchy

1. **One screen, one question.** Today answers "what do I need right now?". Everything else is quieter than that answer.
2. **Three levels of loudness.** Hero card (loudest), a regular card, a card-less strip (quietest). Size, contrast and the accent set the level. Equal-looking blocks make the eye wander, which is why the feed was rejected.
3. **One accent, one place.** The accent is a 28×2 px bar on Next class. It is never a fill or a plate. Because it is used once, it still works as a signal.
4. **Contrast without color.** Importance is carried by size (30 px title), weight and white vs. grey text. Color is the last tool, not the first.

## Information grouping

5. **Group by the user's question, not by data type.** A room change and a new grade both mean "something changed", so they share one Needs attention card. Before, they sat in separate cards because of different data sources, which only made the user guess where to look.
6. **No duplicates across blocks.** Class names live only in the hero. The week strip shows dots only. Each fact appears once.
7. **Same scale, different job.** Next class = one class, now. Week = shape of the days ahead. They look similar in topic but answer different questions, so both stay.
8. **Rows of one kind look identical.** A change row is always: dot, title, one grey detail line, value or time on the right. Grades are not special, so no special color or card.

## Attention and emotion

9. **Calm by default.** Matte black, thin 1 px lines, soft shadows, no saturated blocks. A student opening the app between classes should feel oriented, not alarmed.
10. **Quiet unread marker.** A small white dot marks new items instead of red badges. New info is visible, but there is no pressure to clear it.
11. **A pure white tile steals attention.** The white New grade tile was brightest on the screen but is not the main thing here, so it was removed. Bright areas must match importance.
12. **Chunks of 2–3.** Later today shows two classes, Needs attention shows two items. Everything else sits behind "All changes →" and "Full plan →".

## Content and controls

13. **Text or icon, not both.** There are no logos or decorative icons on the tiles. Labels are small uppercase text, values are large.
14. **Remove what does not help.** No app name or logo in the header. The user knows where they are.
15. **Whole card is the tap target.** Hover lifts the card by 2 px and focus shows a visible outline. Navigation labels are words, not icons.
16. **Dates must be real.** The week is 19–25 Oct 2026 and today is Fri 23. Fake data breaks trust in a prototype.

## Layout

17. **Mobile order = priority order.** Next class, Needs attention, Week.
18. **Desktop keeps the same order.** The hero is tall on the left, Needs attention is on the right, and the week spans the full width below. Wide screens must not reshuffle priorities.

## Open

- Accent color: photo cyan `#1fc6ef`, project plan says green. Change `--accent` in one place.
- Not yet verified online for intuitiveness and practicality, as `CLAUDE.md` requires for new variants.
