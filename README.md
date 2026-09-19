# dewmath

Maths tools for further education, starting with a readiness diagnostic for QQI Level 5 Mathematics for IT (5N18396) and Computational Methods (5N0554).

Everything is a single HTML file with no build step and no server. The site is published from this repository with GitHub Pages.

## Layout

| Path | What it is |
|---|---|
| `index.html` | The landing page: what dewmath is, how the diagnostic works, downloads, stages. |
| `diagnostic.html` | The current diagnostic. Open it bare for the teacher builder, with `#c=…` for a student sitting, with `#analyse` for the class analysis page. |
| `versions/` | Earlier stages, kept so that old links and old results files keep working. |
| `samples/` | A simulated class of twelve results files and one v1-format file, for trying the analysis page. |
| `fonts/` | OpenDyslexic (SIL Open Font License), used by the "Font: OpenDyslexic" display setting. |

## How the diagnostic works

The teacher chooses skills, wording, order, time limit and a question cap in the builder. The settings are packed into the link itself (a few bytes, base64url), so the same link always produces the same sitting. Students answer in the browser; their answers save locally as they go; at the end they download a results file and send it wherever the link told them to (a OneDrive file request, a Microsoft Form with a file upload, or an email). The analysis page reads any number of those files and produces the class report. Nothing is uploaded anywhere by the tool itself.

## Editing the item bank

The bank is the `ITEMS` list near the top of `diagnostic.html`. Each item has a plain-language stem, a mathematical-language stem, and options where exactly one carries `ok:1` and every wrong option carries an error tag (`e:"…"`) described in `ERRORS`. Skills live in `SKILLS` with a level (1 foundation, 2 core, 3 advanced). Append new skills at the end and never reorder the list: a skill's position is its bit in the share code.

## Sending results when file upload is not available

Every finish page offers a second option beside the file download: a short block of text built the same way as the share link, holding the same answers at slightly lower time precision. It fits in a few hundred characters even for the full bank, so it pastes into a paragraph question on a Google Form, a Moodle text box, a spreadsheet cell, or an email body typed by hand. The analysis page has a matching "paste text results" box that reads any number of these, one per line, alongside or instead of uploaded files.

If the submission link is a Microsoft Form (or anything else that supports pre-filled links, such as a Google Form) with a field meant to hold this code, put `{{CODE}}` (any case works) in the builder's link field where the code should go, in place of whatever placeholder value the form's own pre-fill feature generated. The finish page substitutes the real code into that link, so the student's browser opens straight to the form with the answer already filled in. An email address does the same automatically: the text goes into the body of the pre-filled email, not just the subject.

On the analysis page, the file picker also accepts the CSV that Microsoft Forms or Google Forms exports for that question, one row per response. It looks for the results code in the last column of each row and falls back to checking every other column if that one is not it, so a form with extra questions still works. A column literally named `Id`, which both Forms exports include, is used to avoid double-counting a response if the same, later, export is uploaded again. XLSX is deliberately not supported: reading it would need a real parsing library, which this project avoids for the sake of staying one dependency-free file, and CSV carries exactly the same data.

## The builder's wizard tabs

The builder's four tabs (Questions, Delivery, Results & Submission, Share) are numbered and styled deliberately larger than the analysis page's tabs, since this is the page a teacher is most likely to skim past on the way to the link. The sticky bar at the bottom shows "Next: <tab name>" on every tab except the last, and only offers "Copy link" once the Share tab is reached, so building a link means passing through every section at least once rather than grabbing the link from wherever it happens to be visible. Clicking a tab header directly still works, since this is a nudge, not a lock.

## Error citations

Every tagged error the analysis page shows (in the Skills tab, on a student's report card, and on the class-wide Errors tab) is followed by a real example pulled from the item bank itself: the question it was seen on and the wrong answer that was chosen. This is generated at render time from `ITEMS`, not written by hand, so it stays accurate as the bank grows and needs no separate upkeep.

## Reading the analysis page

The page is split into tabs: Overview, Students, Skills, Errors, Confidence and wording, Time, Data and Thresholds. Every label comes from a stated rule with a stated cutoff, and every cutoff can be changed on the Thresholds tab; the report is redrawn when a number changes and the settings stay in the browser. A band decided by a narrow margin is marked as narrow. Percentages count attempted questions only, and a student who ran out of time before reaching most of the questions is routed to foundation support because the pace is itself a signal.

Students can answer "I don't know", "I don't understand some of the words in this question" or "I don't understand what the question is asking me to do". The last two are counted separately so that a vocabulary or reading problem shows up as itself.

## Display settings

The "Display" button on every page sets appearance (light, dark, match device), colour scheme (navy and burnt orange, or slate and teal), font (serif, sans-serif, OpenDyslexic), text size and column width. The choice is stored in the browser and applies across the site.
