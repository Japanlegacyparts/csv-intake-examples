# Leading zeros in CSV IDs / CSVの識別値と先頭のゼロ

This is fictional input data and an actual result from the current paid kit. It is not customer data or evidence of demand.

Compare [before.csv](before.csv) with [after.csv](after.csv): the first part ID changes from `00123` to `123`, while its quantity stays `10`. `A-2` stays unchanged.

The tool matches exact strings. It reports **one only-left record, one only-right record and one same record**. It does not silently treat `00123` and `123` as the same part. There are zero `changed` and zero `needs_review` records: those zeros do **not** mean the files are identical. Read all result categories.

Inspect [comparison.csv](reports/comparison.csv), [comparison.json](reports/comparison.json), and [summary.json](reports/summary.json). Download [comparison.html](reports/comparison.html) to view the formatted report locally. Source hashes in the summary identify the exact input bytes.

If the two IDs should represent the same business item, confirm that with the data owner and agree on an identifier format before preparing a new export. If they represent different items, preserve the difference. This tool does not decide that business rule, restore lost zeros, edit the source files or import records into a live system.

## 日本語

架空の部品データを、現行の有料キットで実際に比較した見本です。顧客データや需要実績ではありません。

前回の識別値 `00123` が今回 `123` になり、数量はどちらも `10`。もう一つの `A-2` は同じです。完全一致で比較するため、結果は **前回のみ1件、今回のみ1件、同じ1件** になります。先頭のゼロを捨てて同じ部品と推定しません。

「変更0件」「要確認0件」でも、二つのCSVが同一とは限りません。「前回のみ」「今回のみ」も確認してください。同じ部品のつもりなら、元データの担当者と識別値の形式を決めてから改めて出力します。別部品なら違いを残します。この道具は業務上の同一性を判断せず、ゼロの復元、CSV修正、本番システムへの取込を行いません。

## Run on your own files / 自分のCSVで使う

These free files contain inputs and generated reports, not the paid program. The [CSV Compare & Import Check kit](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit?utm_source=github&utm_medium=example&utm_campaign=leading_zero_20261116) has a USD 9 base price. Review the checkout total and terms. Python 3.10+ is required. Existing buyers should use their original receipt rather than buy the same download again.

無料見本に有料プログラムは含みません。任意CSVの実行には既存キットとPython 3.10以上が必要です。基本価格は9米ドルで、購入画面の総額と条件を確認してください。購入済みの方は元の受領メールから取得し直し、重複購入しないでください。

[Requirements and limits / 動作条件と対象範囲](https://factory-csv-preflight.kunaki970.chatgpt.site/csv-qa-kit-buying-guide.html)

The comparison accepts UTF-8 CSVs with an optional BOM, one key column and 1–10 selected comparison columns, up to 10,000,000 bytes per file and 10,000 data records across both files. This example checks `part_id` and `quantity` only.

この比較はUTF-8（BOM可）、識別列1列、比較列1～10列、各ファイル10,000,000バイト以内、2ファイル合計10,000データ行以内が対象です。この見本で比較した列は `part_id` と `quantity` だけです。
