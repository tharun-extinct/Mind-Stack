This is a Copilot Skill named release-note-generation in microsoft/PowerToys that provides a structured release-notes pipeline for PowerToys releases.

What the skill does (end-to-end)
It guides an agent/human through 4 phases to produce final release notes:

Collect PRs for a release window

Finds merged/squash PRs between last release commit/tag and stable head.
Builds:
milestone_prs.json
sorted_prs.csv (Id, Title, Labels, Author, Url, Body, CopilotSummary, NeedThanks)
Ensure milestones + labels are correct

Checks/assigns missing milestone (PowerToys {{ReleaseVersion}}).
Finds unlabeled PRs, suggests/apply labels, then refreshes PR export.
Request Copilot review summaries + group PRs

Requests Copilot reviews for each PR.
Re-collects PR data so CopilotSummary is populated.
Groups PR rows into per-label CSV files.
Generate publishable notes

Creates per-group markdown summaries.
Consolidates into v{{ReleaseVersion}}-release-notes.md with Highlights + module sections.
It also includes rules for:

contributor attribution (NeedThanks)
label filtering (Product-*, Area-*, GitHub*, *Plugin, Issue-*)
preserving PR order and batch generation workflow.
/references folder (what each file is for)
SampleOutput.md
Example of the expected final bullet style (user-facing language, PR link, optional attribution).

step1-collection.md
Phase 1 playbook:

verify gh auth
create MemberList.md from core team
find previous release SHA
run PR collection
apply/check milestones
step2-labeling.md
Phase 2 playbook:

detect unlabeled PRs
suggest labels with confidence
generate prs_label_review.md + prs_to_label.csv
apply labels and re-collect
includes common keyword→label mapping table
step3-review-grouping.md
Phase 3 playbook:

request Copilot reviews via MCP
refresh PR dump to capture summaries
group PR CSVs by labels
step4-summarization.md
Phase 4 playbook:

create grouped markdown summaries
then generate final consolidated release notes
defines structure and writing constraints (including no explicit security/privacy wording)
/scripts folder (what each script does)
dump-prs-since-commit.ps1 (core collector)
Builds release PR dataset between commits/tags.
Extracts PR IDs from merge/squash commits, fetches metadata via gh, filters labels, pulls Copilot summaries, computes contributor fields (Author, NeedThanks), outputs JSON + CSV.

collect-or-apply-milestones.ps1
Three modes:

collect current PR milestones
local assign default milestone in output only
remotely apply missing milestone via GitHub API
Supports dry-run (-WhatIf).
apply-labels.ps1
Reads Id,Label CSV and applies labels to PRs via gh pr edit (supports dry run).

group-prs-by-label.ps1
Groups sorted_prs.csv into one CSV per normalized label combination; handles unlabeled rows as Unlabeled.csv.

find-commit-by-title.ps1
When previous release SHA isn’t reachable in target branch history, finds equivalent commit in branch by matching commit subject/title.

diff_prs.ps1
Compares two PR CSV exports and emits incremental-only rows (new PRs since baseline).

Net effect
This skill is essentially a repeatable release-note production system: data collection + milestone/label hygiene + AI-assisted summarization + final publication formatting, with concrete scripts and strict process docs to make releases consistent.