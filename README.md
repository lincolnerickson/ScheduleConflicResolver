# Rooks Con 2026 Schedule Generator

A single-page web app that helps Rooks Con 2026 attendees rate events, resolve scheduling conflicts, and build an optimized personal schedule for the convention (May 20-25).

## Features

### Browse & Rate
- Browse all 239 convention events with search and filters
- Rate each event: **Must Attend**, **Interested**, **If It Fits**, or **Skip**
- Simple mode for casual browsing or Advanced mode with filters for day, game, session type, and rating
- Game names link to their BoardGameGeek pages
- "Mark All Unrated as If It Fits" bulk action for quick setup

### Conflicts
- Automatically detects scheduling conflicts between rated events
- Smart conflict detection — ignores conflicts with tournament heats you won't attend if alternatives exist
- Inline rating buttons to resolve conflicts directly

### Optimize
- **Weighted Interval Scheduling** algorithm (dynamic programming) generates an optimal conflict-free schedule
- Tournament chains (Heat → Semi → Final) are scheduled as complete units when possible
- Configurable options:
  - Max events per day
  - Blocked time ranges (times you can't attend)
  - Exclude specific days
  - Fill empty slots with remaining games
- Warnings for incomplete tournament chains and scheduling issues

### My Ratings
- Grouped overview of all rated events organized by rating level
- Inline rating buttons to quickly change ratings

### My Schedule
- **Timeline view** — visual day-by-day grid with color-coded session types
- **List view** — detailed event list with free time gaps shown between events
- Complete tournament chains highlighted with yellow badges
- Per-event Google Calendar integration (opens directly in Google Calendar)
- Export options: Copy as Text, CSV, PDF (print), or bulk .ics calendar file

## How to Use

1. Open `index.html` in any modern browser — no server or build tools needed
2. **Rate** events in the Browse & Rate tab
3. **Review** conflicts in the Conflicts tab and adjust ratings
4. **Configure** options and click **Generate Optimal Schedule** in the Optimize tab
5. **View** your schedule in the My Schedule tab
6. **Export** to Google Calendar, CSV, PDF, or text

## Technical Details

- Zero dependencies — single HTML file with inline CSS, JS, and embedded CSV data
- All data stored in `localStorage` (ratings and schedule persist between sessions)
- Works offline after initial load
- Responsive design for desktop and mobile

## Optimizer Algorithm

The schedule optimizer uses a DP-based Weighted Interval Scheduling approach:

1. **Pre-select tournament chains** as atomic units (Heat + Semi + Final together)
2. **Run weighted interval scheduling** on remaining candidates (weights: Must = locked, Interested = 10, If It Fits = 3)
3. **Post-process** to fill in any missing tournament chain members
4. **Optionally fill** remaining empty time slots with unscheduled games
5. **Auto-add** demos during free time if they fit
