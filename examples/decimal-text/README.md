# CSV quantities: `10` and `10.0` are different text

This fictional example uses the unchanged CSV comparison tool in CSV Intake QA Workflow Kit. The key is `part_id`; the selected comparison column is `quantity`.

Open [before.csv](before.csv), [after.csv](after.csv), and the generated [comparison.csv](reports/comparison.csv). P-001 changes from `10` to `10.0`; P-002 stays `5`. The actual result is one changed record and one same record, with no left-only, right-only or needs-review records. See [summary.json](reports/summary.json) for source hashes and counts.

The tool compares text exactly. It does not decide that these quantities are numerically equivalent, round values, convert units, or rewrite the source. A changed record identifies a difference to review; it does not prove an incorrect quantity. Same applies only to the selected column for matched keys, not the whole file or business meaning. Successful execution is not import approval.

## Which task fits?

Use the kit when you want a record of exactly what changed between two CSV exports. If your requirement is numerical equivalence, a tolerance such as ±0.01, or automatic format correction, this example does not establish that the kit meets it. Confirm those requirements before buying.

These input files and generated reports are free to inspect. They contain no customer data or paid program code. To run the comparison on your own files you need Python 3.10 or later and the [CSV Intake QA Workflow Kit — base price US$9](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit?utm_source=github&utm_medium=repository&utm_campaign=decimal_text_20261117&utm_content=example_en). Check the final total and terms before paying. Existing buyers can use View content from their original receipt; no repurchase is required for this example.

## 日本語：数量の表記差をどう読むか

架空の品目P-001の数量だけを `10` から `10.0` に変え、P-002は `5` のまま比較しました。現行商品の変更していない比較プログラムによる結果は、変更1件、一致1件、左のみ0件、右のみ0件、要確認0件です。識別列は `part_id`、比較列は `quantity` です。

この道具は文字列を厳密に比較します。数値として同じ量だと判定したり、丸め、単位換算、入力修正をしたりしません。「変更」は確認すべき表記差であり、数量の誤りの確定ではありません。「一致」も選択した比較列の範囲だけです。比較の正常終了を実システムへの取込許可と解釈しないでください。

CSVの前後で何が変わったかを記録したい用途の見本です。数値としての同値判定、許容差、表記の自動修正が必要な場合、この見本だけで商品が適合すると判断しないでください。

入力CSVと生成済みレポートの閲覧は無料です。実顧客データや有料プログラムは含みません。自分のCSVで比較するにはPython 3.10以降と[有料キット（商品価格9 USD）](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit?utm_source=github&utm_medium=repository&utm_campaign=decimal_text_20261117&utm_content=example_ja)が必要です。支払前に最終金額と購入条件を確認してください。購入済みなら元の領収メールのView contentから取得でき、この見本のための買い直しは不要です。
