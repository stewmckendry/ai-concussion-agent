# TO DO

## ✅ Enhancement 3: Enriching Task Completion

### 🎯 Goals
When a patch is finalized, we:
- ✅ Mark the task as `done: true` in `task.yaml`
- 📄 Generate a changelog from the patch summary
- 🧠 Store a reasoning trace from the GPT session

### 📂 Folder Structure
```
.logs/
├── patches/
│   └── patch_*.json
├── changelogs/
│   └── <task_id>.md
├── reasoning/
│   └── <task_id>_trace.md
```

### 🧠 GPT Output Example for Trace
```markdown
## 🧠 Reasoning Summary
- We focused on summarizing goals in < 5 bullets for clarity.
- Explored including KPIs, but deferred to project discovery.
- Feedback from kickoff doc was incorporated.
```

### 🛠 Tooling Plan
- ✅ Add a `complete_task.sh` script
- 🎯 Writes changelog from `summary` in patch metadata
- 🧠 Accepts optional `reasoning_trace.md` file
- ✅ Sets `done: true` in `task.yaml` under `tasks.<task_id>`

---

## 🤯 Enhancement 4: Make PRs Less Cryptic

### 🎯 Rethink PR Body as a Mini Demo or Project Note

### ✅ PR Template (Auto-Generated)
```markdown
## ✨ What was added?
- New file: `project_goals.md`
- Covers task: `1.1_capture_project_goals`

## 🎯 Why it matters
This lays the foundation for clear project alignment and memory bootstrapping.

## 🧠 Thought process
- We debated listing 3 goals vs 5 — settled on 4
- Incorporated team feedback from kickoff doc

## 📄 Related
- Task ID: 1.1
- Prompt: prompts/dev/capture_project_goals.txt
```

### 🛠 Plan
- Update `create_pr_from_patch.sh` to:
  - Read `summary` from `.json`
  - Read changelog + optional reasoning trace
  - Assemble PR body
  - Pass it to `gh pr create --body "$(cat <temp>)"`

---

## ✅ Next Steps
- [ ] Implement `complete_task.sh`
- [ ] Add changelog/trace folder scaffolding
- [ ] Patch PR creation script for markdown body
- [ ] Update onboarding to explain completion logging
- [ ] Add live test using task: `1.1_capture_project_goals`

We're one push away from closing the loop 🌱



# DONE

🧩 1. Hide the Metadata — Human-First UX

"Saving a metadata log file" = scary; “Upload your outputs” = delightful.
✅ Recommendations
Replace file save step with a GPT-generated “download block”:
Files zipped and named clearly
Metadata auto-attached in the ZIP or next to it
Script reads 1 zip folder only from chatgpt_repo/output_zips/
GPT can say:
“Download this zip and run:bash scripts/generate_patch_from_output.sh”
🔧 Implementation
Use one metadata file: metadata.json
Put outputs in chatgpt_repo/outputs/ and metadata.json alongside it
Auto-discover the .json file — no manual naming needed
🌿 2. Smarter Branch Management Across Pods

You nailed the core pain: we need structure, not sprawl.
✅ Branch Naming Convention
chatgpt/auto/feat/<task_id>         # For new features
chatgpt/auto/fix/<task_id>          # For fixes/updates
chatgpt/auto/test/<task_id>         # For QAPod validation
🧠 Rules of Thumb
Limit one active branch per task
Auto-delete branches when PR is merged (GitHub does this ✅)
Use --prune locally to clean up stale ones
🛠 Potential Enhancements
Add a cleanup script: scripts/prune_old_branches.sh
Label PRs by pod: [DevPod], [QAPod] etc. in title
✅ 3. Enriching Task Completion

When a patch is finalized, let’s close the loop by updating:


Signal	Source
✅ done: true	tasks.yaml or active_task.yaml
📝 Change log	Auto-generated from patch summary
🧠 Reasoning trace	Stored as markdown from GPT session
📂 Folder Structure
.logs/
├── patches/
│   └── patch_*.json
├── changelogs/
│   └── 1.1_capture_project_goals.md
├── reasoning/
│   └── 1.1_capture_project_goals_trace.md
🧠 Ideas
GPT can auto-generate reasoning summary:
“Why we chose this approach, what was rejected, what to revisit later”
Add create_changelog.py or extend complete_task.sh
🤯 4. Make PRs Less Cryptic for Humans

Let’s rethink the PR experience as a mini demo or story.

✅ PR Template (Auto-generated)
## ✨ What was added?
- New file: `project_goals.md`
- Covers task: `1.1_capture_project_goals`

## 🎯 Why it matters
This lays the foundation for clear project alignment and memory bootstrapping.

## 🧠 Thought process
- We debated listing 3 goals vs 5 — settled on 4
- Incorporated team feedback from kickoff doc

## 📄 Related
- Task ID: 1.1
- Prompt: `prompts/dev/capture_project_goals.txt`
GPT can fill this out and return as markdown for gh pr create --body.

🚀 TL;DR — Let's Supercharge the Flow


Area	Upgrade
Metadata	Hidden behind a clean ZIP + auto-detection
Branches	Clean naming, auto-deletion, PR labeling
Task Finalization	Auto mark done, changelog + reasoning stored
PR UX	Human-first template auto-filled by GPT
