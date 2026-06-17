# 🍕 10x Alumni Pizza Night

A tiny, self-serve availability picker for the 10x Founders alumni pizza reunion.

- **Live page:** https://fabian-10x.github.io/alumni-pizza-night/
- **What it is:** `index.html` is the pizza-builder. Alumni type their name + email, tap the evenings they can make, and hit send — which emails their picks to Fabi. They can revisit any time to re-choose.
- **`evenings.json`** drives the page: the list of still-live evenings and the live "X in" counts. It is rewritten daily by an automation.
- **`state.json`** is the automation's working memory (per-evening calendar event IDs, per-person history, statuses). Not used by the page.

## How it stays in sync
A daily Cowork task (`alumni-pizza-reconcile`, 07:02 Europe/Berlin) does the loop:
1. Reads the new replies from Fabi's inbox (subject: `Pizza night — my availability`).
2. Adds each person to the calendar hold for every evening they picked (so they get their own blocker), and removes them from evenings they dropped or declined.
3. Updates each hold's title with the live count, e.g. `🍕 Alumni Pizza · 7 in · Tue 21 Jul`.
4. Drops an evening if Nico or Fabi gets a real conflict on it (and removes it from this page); flags low-interest evenings for a human call.
5. Pushes fresh counts here and emails Fabi a ranked summary.

Source of truth for "who's coming" = the Google Calendar holds. This page is the friendly front door.
