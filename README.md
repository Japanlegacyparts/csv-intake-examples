# CSV intake examples: compare by ID, then check import rules

Small fictional order CSVs with complete example reports. Use them to inspect what a CSV check actually reports before trying a tool on business data.

[日本語の説明](README.ja.md)

## Inspect the examples without installing software

1. Open [the input CSV](examples/row-order/inputs/before.csv) in GitHub's file viewer.
2. Compare it with [the reordered file](examples/row-order/inputs/reordered.csv), [a changed amount](examples/row-order/inputs/value-changed.csv), and [a duplicated order ID](examples/row-order/inputs/duplicate-id.csv).
3. Read the corresponding `summary.json` and `comparison.csv` under [examples/row-order](examples/row-order). These open directly in GitHub's text and CSV viewers. For a formatted report, see [the public worked example](https://factory-csv-preflight.kunaki970.chatgpt.site/order-csv-handoff-example.html).

All customers and orders here are fictional. The reports describe these fixtures; they are not customer results or evidence of sales.

## What each ID comparison reports

The key is `order_id`. Only `status` and `amount` are compared as exact strings. The tool does not trim, normalize, convert numbers, guess matches, or pair duplicate keys.

| Fixture | Matching rows | Changed rows | Left-only rows | Right-only rows | Rows needing review |
| --- | ---: | ---: | ---: | ---: | ---: |
| [Row order only](examples/row-order/reordered/summary.json) | 3 | 0 | 0 | 0 | 0 |
| [Row order and one amount](examples/row-order/value-changed/summary.json) | 2 | 1 | 0 | 0 | 0 |
| [Duplicated ID](examples/row-order/duplicate-id/summary.json) | 1 | 0 | 1 | 0 | 3 |

The duplicate case's three review rows are output records, not three completed orders. Ambiguous matches remain unresolved.

## A separate check: does one file satisfy an agreed import contract?

[import-contract.json](examples/order-handoff/inputs/import-contract.json) specifies required columns, unique order IDs, allowed statuses, decimal format and record limits. [invalid_orders.csv](examples/order-handoff/inputs/invalid_orders.csv) deliberately breaks three checks.

| Input file | Contract result | Reported issues |
| --- | --- | ---: |
| [current_orders.csv](examples/order-handoff/inputs/current_orders.csv) | [PASS](examples/order-handoff/reports/preflight-valid.json) | 0 |
| [invalid_orders.csv](examples/order-handoff/inputs/invalid_orders.csv) | [FAIL](examples/order-handoff/reports/preflight-invalid.json) | 3 |

PASS means only that this file matched this contract. It does not establish business correctness or acceptance by a CRM or ERP. The reports keep source hashes so you can identify the exact input used.

## Reproduce with the CSV Intake QA Workflow Kit

The repository contains inputs and pre-generated reports. The comparison and preflight programs are supplied separately in the **CSV Intake QA Workflow Kit**, currently **US$9 for a one-time purchase**. Review the checkout's total before payment. Each program's included license applies to that program.

[View the kit and purchase terms](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit) · [Read the Windows first-run guide](https://factory-csv-preflight.kunaki970.chatgpt.site/csv-kit-first-run.html)

If you already own the kit, do not purchase it again to run these examples. Extract a fresh copy into a new folder. Copy this repository's `examples` folder beside the kit's `tools` folder. Requires Python 3.10 or newer. Run these commands from that kit folder, choosing a new output name each time:

```text
python tools/data-quality-report/compare_csv.py --left examples/row-order/inputs/before.csv --right examples/row-order/inputs/reordered.csv --key order_id --columns status amount --out example-reordered-result
```

Change `reordered.csv` to `value-changed.csv` or `duplicate-id.csv`, with a different unused `--out` name, to reproduce the other comparisons. Completed comparisons return exit code 0 even when differences or review rows exist. An existing output directory is refused with exit code 2; keep the previous report and choose a new name.

For the contract check, create a new folder named `example-preflight-run` first (PowerShell: `New-Item -ItemType Directory example-preflight-run`; macOS/Linux: `mkdir example-preflight-run`). If that name exists, use another new name in both steps.

```text
python tools/csv-import-preflight/preflight.py --contract examples/order-handoff/inputs/import-contract.json --input examples/order-handoff/inputs/invalid_orders.csv --json-report example-preflight-run/report.json --csv-report example-preflight-run/issues.csv
```

The intentional invalid fixture returns FAIL with three issues. It is not a failed installation. Use `current_orders.csv` and new output paths for the passing example.

## Limits and provenance

- These local programs read CSVs without modifying them. They do not upload data, connect to an ERP, or execute an import.
- Comparison reports retain selected values and IDs. Protect reports from real files as sensitive source data.
- Input files are byte-for-byte copies from [the public worked examples](https://factory-csv-preflight.kunaki970.chatgpt.site/order-csv-handoff-example.html). Reports were regenerated with the unchanged kit programs from those exact public input bytes. [SOURCE_MANIFEST.json](SOURCE_MANIFEST.json) records source URLs, source hashes, output hashes and the operation for each file. Preflight timestamps record the regeneration time.
- No paid program code, credentials, analytics, customer files or payment records are in this repository.

Copyright Japan Legacy Parts. The workflow guides and fictional examples remain copyrighted; this repository does not change the separate licenses supplied with purchased software.
