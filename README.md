# 予想外のインフレは政府債務をどれだけ軽くしたか――債務比率の分解、部門別の損得、統合政府：再現ノートブック

秋森弘「予想外のインフレは政府債務をどれだけ軽くしたか――債務比率の分解、部門別の損得、統合政府――」（『北星論集』、2027年3月刊行）の
表・図・本文の数値を、公開統計から再現するJupyterノートブックと、そこで使うデータです。
論文中の数値は、すべてこのリポジトリの実行済みノートブックから転記しています。

Replication notebook for "How Much Did Unexpected Inflation Lighten Japan's Government Debt? Debt Decomposition, Sectoral Gains and Losses, and the Consolidated Government"
(in Japanese, *Hokusei Review*, March 2027). All figures and tables in the paper are reproduced from the executed notebook in this repository.

## 内容

2003〜2025年度の日本について、次を行います。

1. **債務比率の分解**：普通国債残高の対名目GDP比の年ごとの変化を、利払い、事前に見込まれていた名目成長、予想外の物価（GDPデフレーターの実績−政府経済見通し）、予想外の実質成長、赤字等に分解します（論文4節）。
2. **頑健性**：政府見通しの偏り、民間予想・ナイーブな予想への置き換え、公表当時の統計、税収弾性値の感度（5節）。
3. **誰が負担したか**：資金循環統計による国債の保有者別の損失と、部門別の名目ネット・ポジションにもとづく損得（6節）。
4. **統合政府**：一般政府と日本銀行を合わせた名目ネット・ポジション、外部負債の構成、短期金利の感応度（7節）。
5. **本文の数値との突合せ**：論文本文に書かれた数値181件と、ノートブックの出力が一致するかを自動で判定します（出力は `output/tables/numbers_check.csv`）。

| ファイル | 内容 |
|---|---|
| `unexpected_inflation_government_debt.ipynb` | 上記すべてを再現する実行済みノートブック |
| `data/raw/` | ノートブックが読むデータ（下表） |
| `output/figures/` | 論文の図1〜5（白黒印刷用） |
| `output/tables/numbers_check.csv` | 本文の数値との突合せ結果 |

## 再現方法

1. Python 3.12で動作を確認しています。`pip install -r requirements.txt`
2. このフォルダで、ノートブックを上から順にすべて実行します。外部ネットワークは使いません（データはすべて `data/raw/` に入っています）。
   例：`jupyter nbconvert --to notebook --execute --inplace unexpected_inflation_government_debt.ipynb`
3. 最後の節に、突合せの件数（OK／NG）が表示されます。

## データの出所

年度は会計年度（4月〜翌年3月）です。各ファイルは、提供元が公表している表から必要な部分を取り出したものです。

| ファイル | 内容 | 出所 |
|---|---|---|
| `gaku-mfy2622.csv`, `gaku-jfy2622.csv` | 名目・実質GDP（年度、連鎖方式） | 内閣府「国民経済計算」2026年4-6月期2次速報 <https://www.esri.cao.go.jp/jp/sna/data/data_list/sokuhou/files/2026/qe262_2/gdemenuja.html> |
| `vintage/` | 公表当時の名目・実質GDP（各年の1-3月期2次速報、翌年6月） | 同、各年の1-3月期2次速報 |
| `jgb_general_bonds_balance_2002_2026.csv` | 普通国債残高（年度末、額面、兆円） | 財務省「最近20カ年間の年度末の国債残高の推移」 <https://www.mof.go.jp/jgbs/reference/appendix/zandaka01.pdf>（2006年度末以前は同表の2012年3月版） |
| `04_jgb_avg_coupon.csv` | 普通国債の利率加重平均（年度末） | 財務省「普通国債の利率加重平均の各年ごとの推移」 <https://www.mof.go.jp/jgbs/reference/appendix/zandaka05.pdf> |
| `mitoshi_gdp_forecast.csv`, `01_mitoshi_cpi_forecast.csv` | 実質・名目GDP成長率、消費者物価の見通し | 内閣府「政府経済見通し」各年度版 <https://www5.cao.go.jp/keizai1/mitoshi/mitoshikako.html> の閣議決定文書から転記 |
| `esp_jan_forecast.csv` | 民間予想（年度の実質・名目成長率の予測平均、2019〜2025年度） | 日本経済研究センター「ESPフォーキャスト」各年1月調査の結果概要から転記 <https://www.jcer.or.jp/esp-forecast-top/forecast/>。2020〜2022年度の名目成長率は要約中の図のラベルを読み取った値 |
| `02_cpi_monthly.csv` | 消費者物価指数（総合、月次） | 総務省「消費者物価指数」 <https://www.stat.go.jp/data/cpi/1.html> |
| `06_tax_revenue_fy.csv` | 一般会計税収 | 財務省「税収の推移」 <https://www.mof.go.jp/tax_policy/summary/condition/a03.htm> |
| `ff_dl_fof_fiscal-year_jp.csv` | 資金循環統計（年度末ストック、部門別） | 日本銀行「資金循環統計」 <https://www.boj.or.jp/statistics/sj/index.htm> |

## ライセンス

コードはMIT Licenseです（`LICENSE`）。データの利用条件は、それぞれの提供元に従ってください。
