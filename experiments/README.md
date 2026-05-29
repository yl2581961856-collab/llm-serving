# Experiments

Each experiment should be a self-contained slice.

Recommended layout:

```text
experiments/YYYY-MM-DD-short-name/
  README.md
  commands.sh
  env.md
  results.csv
  figures/
  raw/      # ignored by git unless force-added
```

Rules:

- One slice answers one question.
- Save exact commands and environment.
- Keep raw logs locally or in external storage if they are large.
- Commit processed tables, figures, and the written interpretation.
- Change one major variable at a time.
