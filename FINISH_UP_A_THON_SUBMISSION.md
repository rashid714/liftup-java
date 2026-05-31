# LiftUp: From Academic Prototype to Polished Social Impact Platform

Author: Akbar Riyad Mohamed Rasid

Repository: https://github.com/rashid714/liftup-java.git

Challenge: GitHub Finish-Up-A-Thon

## The Comeback Story

LiftUp began as a JavaFX desktop project designed to combat poverty by connecting vulnerable individuals with livelihood opportunities. The core idea, matching people to jobs or training based on skill overlap, was solid. However, the initial build was a functional prototype, not a presentation-ready application. The core workflow existed, but the persistence flow was incomplete, and the app state was volatile.

For the GitHub Finish-Up-A-Thon, I returned to the codebase with a strict mandate: transform a fragile demo into a deterministic, stable desktop application. This was not a superficial color-change update. It was a finish-quality engineering pass focused on data reliability, lifecycle management, and user continuity.

If you are reviewing this for the challenge, focus on the completion arc: the product moved from a volatile prototype into a predictable desktop workflow with real persistence behavior.

## What LiftUp Does

LiftUp is a digital ecosystem for non-profits and community leaders. It allows administrators to:

- Manage Beneficiaries and Opportunities: Track vulnerable individuals and available livelihood programs.
- Intelligently Match: Connect individuals to opportunities based on skill overlap.
- Simulate Support: A wallet feature to demonstrate pathways for direct financial inclusion using MYR and RM.
- Visualize Impact: An interactive dashboard highlighting KPIs, top in-demand skills, and average household metrics.

## The Completion Arc: Before and After

Before:
The application lacked end-to-end persistence. Data management felt disjointed, user preferences disappeared on restart, and the application lacked the deliberate stability expected under real-world administrative usage.

After:
LiftUp now features deterministic save behavior. There is a clean architectural separation between domain data and UI preferences. Application surfaces are stable, preferences are respected across sessions, and the matching workflow provides immediate, dynamic feedback.

What this means practically: users can close the app and return without losing core context.

## Evidence of the Revival

Because the original prototype was not preserved with a complete screenshot set, I used commit history, code diffs, and reproducible local steps as the primary evidence of the before→after transformation.

- Git commit evidence: a focused commit series shows the functional changes (persistence, lifecycle save, CSS fix, chart typing) and provides transparent history for reviewers.
- Compact code excerpts: direct snippets highlight the behavior changes reviewers can inspect in the repo.
- Repro steps: short commands reviewers can run to reproduce the behavior (run the app, save, exit, relaunch and confirm persisted data).

### Review Evidence Included

This submission uses three forms of evidence to show the revival journey:

1. A focused commit series showing persistence, lifecycle, UI, and documentation improvements.
2. Representative code excerpts highlighting behavior changes that reviewers can inspect in the repository.
3. Reproducible local steps so reviewers can verify persistence behavior by running the app, saving data, exiting, and reopening it.

### Example git commands

```bash
# Run the app
mvn javafx:run

# Commit 1: persistence and lifecycle reliability
git add src/main/java/com/liftup/App.java src/main/java/com/liftup/services/SettingsService.java
git commit -m "Revival: add deterministic persistence and shutdown save flow"

# Commit 2: UI polish and chart behavior
git add src/main/resources/com/liftup/views/theme-light.css src/main/resources/com/liftup/views/theme-dark.css
git commit -m "Revival: polish UI styling and clean chart update behavior"

# Commit 3: submission documentation
git add README.md FINISH_UP_A_THON_SUBMISSION.md
git commit -m "Revival: document completion arc and Finish-Up-A-Thon submission"

# Push the finished revival arc
git push origin main

# Verify visible history
git log --oneline --decorate --graph -n 10
```

### Representative code excerpts (what changed)

Settings persistence (example):

```java
public void setTheme(String theme) {
	this.theme = theme;
	save(); // persist immediately so UI prefs survive restarts
}
```

App lifecycle save (example):

```java
@Override
public void stop() throws Exception {
	saveAll(); // saves beneficiaries + opportunities
	settings.save();
	super.stop();
}
```

CSS fix example (high level): removed an invalid numeric token that produced a JavaFX parse error, moving the sizing logic to Java code for deterministic layout.

### Suggested "Before / After" table to include in your post (copy into README or DEV)

| Area             | Before                    | After                               |
| ---------------- | ------------------------- | ----------------------------------- |
| Data persistence | Data lost after restart   | Saves to `.liftup/data.json`        |
| Preferences      | Theme/font reset each run | Saved to `.liftup/prefs.json`       |
| Matching         | Basic skill matching      | Slider-based threshold filtering    |
| UX               | Prototype-like            | Dashboard, icons, dark mode, export |

### Quick reviewer checklist (what judges can run locally)

1. `git clone <repo>` and inspect the commit messages for the focused "Revival" commits.
2. `mvn javafx:run` — open the app and navigate to Beneficiaries/Opportunities.
3. Create or modify an entry, press Save, close the app.
4. Reopen the app and confirm the new data is present (persistence proof).

## How to Run

```bash
git clone https://github.com/rashid714/liftup-java.git
cd liftup-java
mvn javafx:run
```

Notes: Java 17 and JavaFX are required. If you prefer a packaged artifact, build the JAR with `mvn -DskipTests package` and run the produced artifact under your JVM.

## Persistence Test

1. Run the app with `mvn javafx:run`.
2. Open the Beneficiaries or Opportunities tab and add or edit an item.
3. Click the Save button (or use File → Save if present).
4. Close the application window.
5. Re-open the application and confirm that your changes persist.

If the data saved correctly, open `~/.liftup/data.json` to show the saved JSON. Open `~/.liftup/prefs.json` to show saved theme/font preferences.

## My Experience with GitHub Copilot

GitHub Copilot was instrumental in shifting UI interactions from one-off demo actions to stable application behavior.

Specifically, Copilot helped architect a clean two-step flow for the matching engine. It assisted in wiring backend matching logic to a dynamic UI threshold filter, allowing the Minimum Skills in Common slider to instantly update results using overlapCount.

Beyond data flow, Copilot also sped up usability polish. It helped generate boilerplate for JavaFX keyboard shortcut bindings and the clamp logic used for root font scaling accessibility features.

## Technical Deep Dive

### Persistence Architecture (Gson)

To improve data reliability, LiftUp uses a dual-layer persistence model with Gson that saves directly to the user home directory:

- Domain Data: Beneficiaries and opportunities are serialized via DataStore.java into .liftup/data.json.
- UI Preferences: Theme and font scale configurations are handled by SettingsService.java and saved to .liftup/prefs.json.

Manual clicks on the Save button trigger saveAll(). The JavaFX stop() lifecycle hook also runs saveAll() when the window closes, reducing accidental data loss. Theme and font preferences persist through their setters, maintaining UI continuity.

### Explainable Matching Engine

To keep behavior transparent for administrators, the matching engine uses a straightforward, verifiable algorithm:

1. Candidate Selection: MatchingService.java returns opportunities where at least one skill overlaps.
2. Threshold Filtering: The UI applies the slider threshold with overlapCount, showing only opportunities that meet the minimum requirement.

## Tech Stack

- Language: Java 17
- UI Framework: JavaFX 21
- Build Tool: Apache Maven
- Data Handling: Gson

## Demo Evidence

The application can be verified through the persistence test above. Additional screenshots for the final post may include:

1. Dashboard view (KPIs and charts)
2. Beneficiaries tab (CRUD and filtering)
3. Opportunities tab (CRUD and filtering)
4. Match and Support tab (slider-driven threshold)
5. Save and relaunch persistence proof

## Final Takeaway

By establishing true persistence, refining JavaFX lifecycle behavior, and leveraging GitHub Copilot to bridge backend logic with dynamic UI controls, LiftUp now reflects the original vision: a robust and reliable tool for social impact.