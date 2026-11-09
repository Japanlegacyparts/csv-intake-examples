# CSV取込前点検の架空データと結果見本

行順だけの違い、値の変更、重複IDを見分けるための受注CSV見本です。実際の業務データを使う前に、入力と出力の関係を確認できます。[English](README.md)

## 比較と取込前点検を一つのジョブで実行した見本

[CSV専用の販売案内で、同梱物・無料見本・購入手順を確認できます](https://japanlegacyparts.gumroad.com/csv-workflow#japanese)。商品価格は買い切り9 USDです。支払前に最終総額と購入条件を確認してください。購入済みなら元のView contentを使い、買い直さないでください。

現在の有料キットには、前回と今回のCSVの比較に続けて、今回のCSVを合意済みのJSON契約で点検する実行器が入っています。購入前に、架空入力とジョブ設定と実際に生成したレポートを読めます。

- [契約PASSのケース](examples/one-job-workflow/reports/pass/workflow-result.json)：二工程が完了しています。比較には値の変更、前回だけのID、今回だけのIDが各一件あります。PASSはファイル同士の一致を意味しません。
- [契約FAILのケース](examples/one-job-workflow/reports/contract-fail/preflight.json)：二工程が完了し、不備が3件あります。点検が完了して指摘が出た結果です。
- [契約の設定誤記](examples/one-job-workflow/reports/contract-typo/workflow-result.json)：比較は完了していますが、契約点検は未完了です。`complete=false`、`preflight_result=null`で、途中の出力をPASSとして扱いません。

[一括実行の無料見本ZIP](https://github.com/Japanlegacyparts/csv-intake-examples/releases/download/workflow-results-2026-11-10/one-job-result-example-20261110.zip) / [SHA-256の照合用ファイル](https://github.com/Japanlegacyparts/csv-intake-examples/releases/download/workflow-results-2026-11-10/SHA256SUMS.txt) / [表と説明を付けた結果見本](https://factory-csv-preflight.kunaki970.chatgpt.site/csv-one-job-workflow-example.html)

架空データを販売者が実行した機能見本です。顧客実績や売上の証拠ではありません。無料ZIPに有料プログラムのコードは含みません。自分のCSVを実行する場合は、[既存のCSV Intake QA Workflow Kitの商品と決済画面 — 商品価格9 USD](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit?wanted=true&utm_source=github&utm_medium=repository&utm_campaign=csv_workflow_20261110&utm_content=readme_ja)で、プログラム、一括実行器、日英の手順を取得できます。実行にはPython3.10以降が必要です。支払前に決済画面の最終金額と購入条件を確認してください。データ修正や実システムへの取込は含みません。購入済みの場合はView contentから最新の完全版を取得し、この見本のために再購入しないでください。

## 見本一式をZIPで取得する

[架空CSVと結果見本をまとめてダウンロード](https://github.com/Japanlegacyparts/csv-intake-examples/releases/download/examples-2026-11-09/csv-intake-examples.zip) / [SHA-256の照合用ファイル](https://github.com/Japanlegacyparts/csv-intake-examples/releases/download/examples-2026-11-09/SHA256SUMS.txt)

ZIPを展開すると、入力CSVと生成済みの結果を確認できます。公開中の見本と説明を収録しています。比較と取込前点検を実行するプログラムは、別売りのキットに含まれます。

## 購入せずに見る

`examples/row-order/inputs` が入力です。各ケースの `summary.json` が件数、`comparison.csv` が結果の明細です。GitHubのテキスト表示とCSV表示で読めます。整形された表は [公開中の作業見本](https://factory-csv-preflight.kunaki970.chatgpt.site/order-csv-handoff-example.html) で確認できます。

| ケース | 同一行数 | 変更行数 | 左だけの行数 | 右だけの行数 | 要確認行数 |
| --- | ---: | ---: | ---: | ---: | ---: |
| 行順だけの変更 | 3 | 0 | 0 | 0 | 0 |
| 行順と金額の変更 | 2 | 1 | 0 | 0 | 0 |
| 注文IDの重複 | 1 | 0 | 1 | 0 | 3 |

識別子は `order_id`、比較列は `status` と `amount` です。文字列を厳密に比較します。重複IDの相手を推定しません。要確認3行は出力レコード数で、3注文の成立を意味しません。

## 一つのCSVを取込ルールと照合する

`examples/order-handoff/inputs/import-contract.json` が列、必須値、一意性、状態値、金額形式、行数のルールです。`current_orders.csv` の結果はPASSで問題0件、`invalid_orders.csv` は意図的な違反を含みFAILで問題3件です。`reports/preflight-*.json` で各指摘と入力ハッシュを確認できます。

PASSは、このファイルがこのルールに合ったという意味です。業務上の正しさや、CRM・ERPの取込成功を保証しません。データも結果も架空で、顧客実績ではありません。

## 購入済みのキットで再現する

このリポジトリにプログラムは含みません。比較と取込前点検の二つのプログラムは、別商品の **CSV Intake QA Workflow Kit** に含まれます。現在の販売表示は **買い切りUS$9** です。支払前に決済画面の総額を確認してください。ソフトウェアごとに同梱のライセンスが適用されます。

[商品と購入条件](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit) / [Windowsで最初の結果を出す手順](https://factory-csv-preflight.kunaki970.chatgpt.site/csv-kit-first-run.html)

プログラムを購入する場合は、[Gumroadの決済画面へ進めます — 商品価格9 USD](https://japanlegacyparts.gumroad.com/l/csv-intake-qa-workflow-kit?wanted=true&utm_source=github&utm_medium=repository&utm_campaign=csv_examples_20261109&utm_content=readme_ja)。支払前に最終金額と購入条件を確認してください。実行にはPython 3.10以降が必要です。

購入済みなら、この見本のための再購入は不要です。キットを新しいフォルダーへ展開し、`tools` と同じ階層にこのリポジトリの `examples` をコピーします。同名フォルダーを上書きしないでください。Python 3.10以降が必要です。コマンドは [English README](README.md#reproduce-with-the-csv-intake-qa-workflow-kit) に記載しています。

比較処理は差異があっても正常完了なら終了コード0です。出力先が既にある場合は終了コード2で拒否します。元の結果は残し、未使用の出力名へ変更します。取込前点検で架空の不正ファイルがFAILになるのは想定された結果です。

## 取扱い

入力を書き換えず、外部送信も行いません。システムへの取込、API連携、データ修正は行いません。比較結果には識別子と選択した値が残るため、実ファイルの結果は元データと同じ区分で保管してください。

入力は [公開中の見本](https://factory-csv-preflight.kunaki970.chatgpt.site/order-csv-handoff-example.html) から内容を変えずに複製しています。結果は、その公開入力の実バイトから変更していないキットのプログラムで再生成しました。各URL、元のハッシュ、出力ハッシュ、生成方法は `SOURCE_MANIFEST.json` にあります。取込前点検の日時は再生成した時刻です。有料プログラム、秘密情報、実顧客情報、決済記録は含みません。

Copyright Japan Legacy Parts. 手順と架空見本の著作権を保持します。この公開によって購入ソフトウェアの個別ライセンスを変更しません。
