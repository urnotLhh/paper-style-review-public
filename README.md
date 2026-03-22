# paper-style-review

Structured review pipeline for Chinese academic papers.

This repository is the public-safe release track of the skill. It keeps the runnable review pipeline, schemas, and publishable derived rules, while excluding private sample papers, runtime outputs, raw source attachments, and local workspace traces.

## What It Does

- build a canonical structure map for a target paper
- learn style profiles from user-provided reference papers
- review the target across format, terminology, logic, and style deviation
- inject structured findings back into Word comments

## Public Release Boundary

Included:
- runnable Python pipeline under `scripts/`
- skill instructions in `SKILL.md`
- publishable derived reference material under `references/`
- example runtime config without local absolute paths

Excluded:
- real papers and named sample corpora
- historical outputs, archives, and annotated deliverables
- local `tmp/` state and bytecode caches
- original `.doc` attachments and raw extraction artifacts
- workspace-specific absolute paths

## Quick Start

Run the full pipeline:

```bash
python3 scripts/run_review.py --config ./references/review-config.example.json
```

Run one stage only:

```bash
python3 scripts/run_review.py --config ./references/review-config.example.json --stage style_profile
python3 scripts/run_review.py --config ./references/review-config.example.json --stage style_annotation
python3 scripts/run_review.py --config ./references/review-config.example.json --stage annotation
```

Limit target-side LLM review to abstract and chapter 1:

```bash
python3 scripts/run_review.py --config ./references/review-config.example.json --chapters abstract,1
```

## Minimal Config Shape

```json
{
  "target": {
    "path": "./inputs/target.docx"
  },
  "refs": [
    {
      "id": "ref-style-01",
      "path": "./inputs/ref-style-01.docx",
      "enabled": true,
      "styleProfileEnabled": true
    }
  ],
  "outputDir": "./outputs"
}
```

## Notes

- Bring your own `target` and `refs`.
- The public repository does not ship built-in named reference papers.
- The default examples use relative, publishable paths only.
- Format-related materials in `references/` are derived summaries, not redistributed raw attachments.
