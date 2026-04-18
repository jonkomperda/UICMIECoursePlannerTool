# MIE Course Planner Tool

This project is a static webpage for planning UIC MIE degree flowcharts. It supports multiple curricula, eligibility-aware recommendations, import/export of progress, and image export of the current plan.

## What The Page Does

- Lets you choose from five curricula:
  - Mechanical Engineering
  - Industrial Engineering
  - Engineering Management
  - Mechanical Engineering (Fall 2017 to Spring 2024)
  - Industrial Engineering (Fall 2017 to Spring 2024)
- Tracks completed courses by clicking them on and off
- Recommends a next-term schedule up to 18 credits
- Shows all eligible candidates for the selected target term
- Exports the current planner view as a PNG image
- Imports a saved plan JSON file for the currently selected curriculum

## How To Open The Webpage

No build step is required.

### Option 1: Open Directly

Open [index.html](/Users/jon/Documents/GitHub/MIECoursePlannerTool/index.html) in a browser.

The page includes embedded curriculum fallbacks, so it still works when opened directly from disk.

### Option 2: Serve Locally

From the project folder, run:

```bash
python3 -m http.server
```

Then open:

```text
http://localhost:8000
```

## How To Use The Planner

### 1. Choose A Curriculum

Use the curriculum selector at the top of the page to switch between the available degree plans.

### 2. Mark Completed Courses

Click a course card to mark it completed.

- Gray cards are marked taken
- Clicking a taken course again removes it
- Corequisites and concurrent prerequisites are bundled automatically when needed

### 3. Pick A Target Term

Use the `Target term` selector to switch between `Fall` and `Spring`.

This affects:

- which courses count as offered
- the eligible candidate list
- the recommended next-term pack
- the exported PNG filename

### 4. Read The Planner Sections

The page has three main sections:

- `Recommended Next Term`: a packable schedule up to 18 credits
- `All Eligible Candidates`: eligible courses ordered by recommendation priority
- `Terms Grid`: all courses grouped by flowchart term

Card styling:

- White: locked or not offered for the selected term
- Green: eligible now
- Gray with strikethrough: completed
- Red ring: terminal course

### 5. Filter To Only Eligible Courses

Enable `Show only eligible` to hide ineligible courses from the term grid.

### 6. Reset Progress

Use `Reset` to clear the current curriculum's saved progress.

Progress is stored separately for each curriculum in browser local storage.

## Exporting And Importing

### Export Image

Click `Export Image` to download a PNG of the planner grid.

The exported image includes:

- the curriculum name
- the selected target term
- all eight flowchart terms
- crossed-out completed courses
- circled recommended courses

### Import Plan

Use `Import Plan` to load a previously saved JSON plan.

Notes:

- Import expects a JSON plan file, not the PNG export
- The imported file must match the currently selected curriculum
- Unknown course codes are skipped automatically

## Recommendation Rules

Recommendations are based on:

- course eligibility for the selected target term
- proximity to the student's next unfinished flowchart term
- positional weight (`pw`) as a tie-breaker
- curriculum-specific recommendation gates for `499` seminar/audit courses

## Development Notes

- The app is a single static HTML file with JSON curriculum files under `curricula/`
- Browser unit tests live in `tests/test_functions.js`
- Python regression tests live in `tests/test_curriculum_loader.py`

## License

This repository is licensed under [CC BY-NC-SA 4.0](/Users/jon/Documents/GitHub/MIECoursePlannerTool/LICENSE).

That means reuse requires attribution, commercial use is not allowed, and shared adaptations must use the same license.
