Evidence and Reviewer Guide (no screenshots)
==========================================

If you do not have before/after screenshots, this file explains how to provide equivalent, verifiable evidence using commits, diffs, and reproducible steps.

1) Commit strategy (recommended)

- Commit 1 — `feat(persistence): domain data -> ~/.liftup/data.json`
  - Adds save/load to `DataStore` and calls from `App.saveAll()`.

- Commit 2 — `feat(settings): persist UI preferences -> ~/.liftup/prefs.json`
  - Adds immediate `save()` calls in `SettingsService` setters and ensures `settings.save()` is called on `App.stop()`.

- Commit 3 — `fix(ui): css parse error, chart typing, misc polish`
  - Removes invalid CSS token, moves layout sizing to Java, updates chart series types.

2) Commands judges can run locally

```bash
git clone https://github.com/rashid714/liftup-java.git
cd liftup-java
git log --oneline --decorate --patch --reverse --no-merges | sed -n '1,200p'

# Build and run (Java + JavaFX required)
mvn -DskipTests package
mvn javafx:run
```

3) Diffs and patches

If you prefer not to push intermediate commits, create a patch for the final diff:

```bash
# produce a single patch file for the final commit
git format-patch -1 --stdout HEAD > finish-up-athon-evidence.patch

# Or show staged changes
git diff --staged -- src/main/java/com/liftup/services/SettingsService.java src/main/java/com/liftup/App.java
```

4) Example assertions reviewers can perform

- After `mvn javafx:run`: create or edit a beneficiary, press Save, close the app, then reopen. Verify the new beneficiary appears (persistence proof).
- Open `~/.liftup/data.json` and show the saved JSON content as direct evidence.
- Open `~/.liftup/prefs.json` to show theme/font preferences saved.

5) Release guidance

Build the project and attach the JAR to a GitHub Release so reviewers can quickly download and run without building locally.

```bash
mvn -DskipTests package
# JAR is under target/ (attach to GitHub Release)
ls -lh target/*.jar
```

6) Post template (copy into DEV / README)

Use the "Before / After" table from the main submission and then paste a short `git show HEAD` or `git diff` excerpt beneath each bullet to prove the change.
