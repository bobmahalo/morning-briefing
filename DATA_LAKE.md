# 🗄️ Open SEC XBRL Data Lake & Wide-Net Market Scanner
**Generated:** 2026-11-07 16:49 UTC | **Coverage:** `5,356` Active `10-K`/`10-Q` Operating Companies (`68` Normalized Columns)

[☕ Daily Morning Briefing](https://bobmahalo.github.io/morning-briefing/) | [📈 $100K Model Portfolio](https://bobmahalo.github.io/morning-briefing/PORTFOLIO.html) | [🗄️ Open SEC Data Lake](https://bobmahalo.github.io/morning-briefing/DATA_LAKE.html) | [🏛️ S&P 1500 Screen](https://bobmahalo.github.io/morning-briefing/SP1500_SCREEN.html) | [🎓 Master Curriculum](https://bobmahalo.github.io/morning-briefing/CURRICULUM.html) | [🔬 SSR Executive Curriculum](https://bobmahalo.github.io/morning-briefing/SSR_CURRICULUM.html) | [🗂️ Single Stock Directory](https://bobmahalo.github.io/Single-Stock-Scan/)

> **🏛️ True Stock Ownership & Custody Education:** Holding shares in broker "Street Name" means you only hold a beneficial entitlement while Cede & Co. holds legal title. Learn how Direct Registration (DRS) protects your shares from broker insolvency and short-lending at **[WhyDRS.org](https://www.whydrs.org)** ([Advocacy](https://www.whydrs.org/advocacy) | [Free Resources](https://www.whydrs.org/free-resources)).

> **Disclaimer:** *This report and open dataset are for educational and informational purposes only and do not constitute financial advice. The author is not a licensed financial advisor. All investments carry risk, and you should conduct your own due diligence before making any financial decisions.*

## 1. Centralized SEC XBRL Data Lake (Direct Download & Query Endpoints)

Instead of burning paid API tokens querying slow-moving quarterly balance sheets one ticker at a time, this repository compiles the SEC EDGAR nightly bulk archives (`companyfacts.zip` + `submissions.zip`, `~2.8 GB` raw XBRL) through a deterministic CPA tag-fallback normalizer into a compact **`~2.6 MB`** dataset covering **`5,356` active `10-K`/`10-Q` operating companies** across **`68` columns** (Financials and REITs in `SIC 6000–6799` are excluded due to non-standard working capital and debt structures). Updated every weekend.

| Dataset Artifact | Scope & Row Count | Format | Direct Download / Query Link | Raw GitHub Endpoint (For Scripts & Bots) |
| :--- | :--- | :---: | :---: | :---: |
| **Master Universe (All Operating Filers)** | `5,356` rows × `68` cols | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Master_Universe_All_Stocks.csv) | [`raw/.../Master_Universe_All_Stocks.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Master_Universe_All_Stocks.csv) |
| **Master Universe SQLite Database** | `5,356` rows (`master_universe` table) | `SQLite3` | [📥 Download SQLite](https://bobmahalo.github.io/morning-briefing/data/master_universe.sqlite) | [`raw/.../master_universe.sqlite`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/master_universe.sqlite) |
| **Non-Dilutive Hunting Bucket Qualifiers** | `1,052` rows (`>= 1` bucket, non-dilutive) | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Hunting_Buckets_Sub5_and_DeepValue.csv) | [`raw/.../Hunting_Buckets_Sub5_and_DeepValue.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Hunting_Buckets_Sub5_and_DeepValue.csv) |
| **Stage 1 Forensic Convergence Shortlist** | `41` multi-bucket forensic survivors | `CSV` | [📥 Download CSV](https://bobmahalo.github.io/morning-briefing/data/Stage1_Convergence_Shortlist.csv) | [`raw/.../Stage1_Convergence_Shortlist.csv`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Stage1_Convergence_Shortlist.csv) |
| **CPA XBRL Tag Fallback Dictionary** | Ranked `us-gaap` aliases & derived identities | `YAML` | [📥 View YAML](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml) | [`raw/.../xbrl_aliases.yaml`](https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/xbrl_aliases.yaml) |

<details markdown="1">
<summary>⚡ <b>Quick-Start Code Snippets: Query All `5,356` Stocks in 1 Line (Python, SQLite, Google Sheets — Zero API Tokens)</b></summary>

### Option A: Python (`pandas`) — Zero Clone Required
```python
import pandas as pd

# Pull the entire normalized SEC operating universe directly over HTTPS:
url = "https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Master_Universe_All_Stocks.csv"
df = pd.read_csv(url)

# Run your own custom screen (Columns 1-60 are pure un-opinionated fundamentals & forensics):
custom_screen = df[
    (df["ROIC_TTM_Pct"] >= 15.0)
    & (df["FCF_to_Price_Yield_Pct"] >= 8.0)
    & (df["Share_Count_1Y_Change_Pct"] <= 0.0)
    & (df["Piotroski_F_Score"] >= 7)
].sort_values("FCF_to_Price_Yield_Pct", ascending=False)
print(custom_screen[["Ticker", "Company_Name", "Share_Price", "FCF_to_Price_Yield_Pct", "ROIC_TTM_Pct"]].head(20))
```

### Option B: Google Sheets — Live Auto-Updating Sheet
Paste this into cell `A1` of any blank Google Sheet to import the Stage 1 Forensic Shortlist (or replace with `Master_Universe_All_Stocks.csv`):
```text
=IMPORTDATA("https://raw.githubusercontent.com/bobmahalo/morning-briefing/main/data/Stage1_Convergence_Shortlist.csv")
```

### Option C: Local SQLite Query (`master_universe.sqlite`)
```sql
SELECT Ticker, Company_Name, Share_Price, Market_Cap_M, FCF_to_Price_Yield_Pct, Net_Cash_Ex_Debt_Per_Share, Piotroski_F_Score
FROM master_universe
WHERE Is_Dilution_Vampire = 0
  AND Net_Cash_to_Price_Yield_Pct >= 30.0
  AND Piotroski_F_Score >= 6
ORDER BY FCF_to_Price_Yield_Pct DESC;
```

</details>

<details markdown="1">
<summary>🤝 <b>Community Formula & CPA XBRL Tag Bounty ("Contribute Rules, Never Raw Data")</b></summary>

> **Why Contributors Submit Rules Instead of Mutated CSVs:**  
> Every weekend, the bulk scanner rebuilds all `5,356` rows from scratch out of the SEC EDGAR bulk archives. If a contributor manually edits a CSV, the next weekend refresh will overwrite it—and manual CSV edits cannot be audited for lookahead bias or unit errors.

| Contribution Type | Where It Lives in the Pipeline | How to Propose an Upgrade | Community Benefit |
| :--- | :--- | :--- | :--- |
| **1. Missing CPA XBRL Tag Fallback** | [`xbrl_aliases.yaml`](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml) | Identify a ticker where a standard GAAP line item shows `NR` due to an unusual CPA taxonomy tag and submit the `us-gaap:TagName` rank order. | Eliminates blank cells across all filers using that accounting convention. |
| **2. New Un-Opinionated Fundamental Column** | `models/wide_net_scoreboard.py` | Propose a deterministic accounting ratio or balance-sheet metric built from SEC `10-K`/`10-Q` line items (e.g., Interest Coverage, Cash Conversion Cycle, Gross Profitability). | Once verified by `pytest`, our weekend engine compiles and hosts your column across all `5,356` stocks automatically every week. |
| **3. Custom Strategy Sieve / Factor Idea** | Community Discussion / PR | Use Columns `1–60` (pure fundamentals & forensics) to test your own risk-tolerance rules, then share high-signal mathematical sieves for review. | Shared alpha discovery without duplicating `2.8 GB` SEC data pulls. |

</details>

---

## 2. Wide-Net Market Scanner: Universe Health & 4 Hunting Buckets

- **Total Operating `10-K`/`10-Q` Companies Scanned:** `5,356` (`4,051` non-dilutive operating filers + `1,305` quarantined by Step A Dilution Sieve)
- **Companies with Live Exchange Price:** `4,336` (`1,136` trading at `<= $5.00/sh`)
- **Stage 1 Multi-Bucket Forensic Survivors:** `41` companies passing all binary solvency, dilution, and F-Score gates

### Summary of the 4 Hunting Buckets

| Hunting Bucket | Total Qualifiers | Sub-$5.00 (`<= $5`) | `$5.01 - $20.00` | `> $20.00` |
| :--- | ---: | ---: | ---: | ---: |
| **1. Net Cash Floor / Graham Net-Net (`Bucket_1_Net_Cash_Floor`)** | **270** | `99` | `113` | `58` |
| **2. High-FCF Deep Value Turnaround (`Bucket_2_High_FCF_Turnaround`)** | **152** | `34` | `45` | `73` |
| **3. Cannibal Share Buybacks (`Bucket_3_Cannibal_Buybacks`)** | **509** | `18` | `72` | `419` |
| **4. C-Suite / Cluster Insider Buying (`Bucket_4_Cluster_Insider_Buy`)** | **353** | `108` | `107` | `123` |

## Bucket 1: Net Cash Floor & Graham Net-Nets (`Bucket_1_Net_Cash_Floor`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PMCB** | PharmaCyte Biotech, Inc. | `$0.38` | $4.03M | `$1.66` | `$2.24` | `$2.56` | **NR** | `57.98%` | `3/9` | `1_NET_CASH_FLOOR` |
| **NBRG** | Newbridge Acquisition Ltd | `$10.17` | $15.80M | `$38.81` | `$-0.55` | `$2.13` | **NR** | `-42.20%` | `3/9` | `1_NET_CASH_FLOOR` |
| **IRLA** | IRulya Therapeutics Inc. | `$30.91` | $31.44M | `$114.04` | `$106.09` | `$-34.73` | **-149.51%** | `-98.11%` | `2/9` | `1_NET_CASH_FLOOR` |
| **MNTN** | MNTN, Inc. | `$4.67` | $66.54M | `$16.65` | `$17.07` | `$19.82` | **NR** | `96.02%` | `6/9` | `1_NET_CASH_FLOOR` |
| **LABT** | Lakewood-Amedex Biotherapeut | `$0.60` | $1.42M | `$1.85` | `$1.78` | `$1.83` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **GTEC** | Greenland Technologies Holdi | `$0.48` | $9.20M | `$1.31` | `$3.21` | `$4.66` | **156.91%** | `40.01%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PLRX** | PLIANT THERAPEUTICS, INC. | `$0.82` | $50.52M | `$2.09` | `$1.94` | `$2.37` | **-140.34%** | `0.87%` | `3/9` | `1_NET_CASH_FLOOR` |
| **PHUN** | Phunware, Inc. | `$1.73` | $35.40M | `$4.24` | `$4.30` | `$4.20` | **-52.08%** | `1.37%` | `2/9` | `1_NET_CASH_FLOOR` |
| **SHAZ** | SharonAI Holdings Inc. | `$19.51` | $365.91M | `$45.58` | `$39.69` | `$59.07` | **2.45%** | `93.88%` | `2/9` | `1_NET_CASH_FLOOR` |
| **FBIO** | Fortress Biotech, Inc. | `$1.84` | $61.29M | `$4.29` | `$4.05` | `$3.60` | **-130.83%** | `11.96%` | `5/9` | `1_NET_CASH_FLOOR` |
| **CIIT** | Tianci International, Inc. | `$1.55` | $1.84M | `$3.59` | `$4.50` | `$4.71` | **NR** | `-92.84%` | `6/9` | `1_NET_CASH_FLOOR` |
| **SRXH** | SRX Global Inc. | `$0.79` | $16.03M | `$1.77` | `$3.10` | `$3.09` | **-27.44%** | `-18.46%` | `2/9` | `1_NET_CASH_FLOOR` |
| **TPET** | Trio Petroleum Corp | `$1.48` | $7.88M | `$3.25` | `$4.37` | `$6.85` | **NR** | `-36.93%` | `4/9` | `1_NET_CASH_FLOOR` |
| **VIDA** | VIDA Global Inc. | `$0.73` | $6.92M | `$1.52` | `$1.49` | `$1.82` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **ACXP** | Acurx Pharmaceuticals, Inc. | `$0.97` | $5.11M | `$2.02` | `$0.19` | `$1.55` | **NR** | `232.53%` | `4/9` | `1_NET_CASH_FLOOR` |
| **MRLN** | Merlin, Inc. | `$0.77` | $78.19M | `$1.51` | `$0.46` | `$-0.99` | **NR** | `28.67%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **XBIT** | XBiotech Inc. | `$1.87` | $57.01M | `$3.59` | `$3.48` | `$4.21` | **-71.63%** | `0.00%` | `4/9` | `1_NET_CASH_FLOOR` |
| **EROC** | ERock, Inc. | `$6.67` | $321.08M | `$12.39` | `$3.33` | `$5.33` | **NR** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **RNA** | Atrium Therapeutics, Inc. | `$8.39` | $143.52M | `$15.33` | `$12.22` | `$12.54` | **-42.14%** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **MBLY** | Mobileye Global Inc. | `$5.12` | $1,292.31M | `$9.33` | `$5.76` | `$9.19` | **24.53%** | `16.85%` | `5/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **LAB** | STANDARD BIOTOOLS INC. | `$0.62` | $245.32M | `$1.10` | `$1.06` | `$1.05` | **-26.76%** | `2.66%` | `4/9` | `1_NET_CASH_FLOOR` |
| **PMN** | ProMIS Neurosciences Inc. | `$3.54` | $31.75M | `$5.96` | `$5.51` | `$5.51` | **-53.66%** | `-82.69%` | `3/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$4.66` | $56.13M | `$7.59` | `$6.29` | `$8.07` | **36.12%** | `-4.18%` | `4/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **NCRA** | NOCERA, INC. | `$1.37` | $2.92M | `$2.23` | `$1.11` | `$2.54` | **-71.68%** | `-85.13%` | `4/9` | `1_NET_CASH_FLOOR` |
| **CLDI** | Calidi Biotherapeutics, Inc. | `$0.63` | $1.63M | `$1.02` | `$0.53` | `$1.21` | **NR** | `-24.58%` | `3/9` | `1_NET_CASH_FLOOR` |
| **AFCG** | Advanced Flower Capital Inc. | `$2.94` | $65.87M | `$4.56` | `NR` | `$8.55` | **NR** | `-0.84%` | `3/9` | `1_NET_CASH_FLOOR` |
| **FRVO** | Fervo Energy Co | `$7.78` | $1,221.64M | `$11.26` | `$10.19` | `$17.79` | **-53.22%** | `NR` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SEER** | Seer, Inc. | `$1.64` | $90.53M | `$2.36` | `$2.44` | `$4.08` | **-48.86%** | `NR` | `3/9` | `1_NET_CASH_FLOOR` |
| **DRMA** | Dermata Therapeutics, Inc. | `$0.77` | $3.10M | `$1.10` | `$0.83` | `$0.87` | **NR** | `490.14%` | `3/9` | `1_NET_CASH_FLOOR` |
| **AIDX** | 20/20 Biolabs, Inc. | `$0.18` | $2.36M | `$0.26` | `$0.17` | `$0.11` | **NR** | `116.52%` | `4/9` | `1_NET_CASH_FLOOR` |
| **FAC** | Factorial Energy Inc. | `$3.95` | $74.79M | `$5.54` | `$3.06` | `$4.49` | **NR** | `2.77%` | `NR/9` | `1_NET_CASH_FLOOR` |
| **SION** | Sionna Therapeutics, Inc. | `$3.27` | $147.84M | `$4.49` | `$4.39` | `$5.88` | **-51.55%** | `2.43%` | `4/9` | `1_NET_CASH_FLOOR` |
| **RXST** | RxSight, Inc. | `$4.53` | $189.73M | `$5.83` | `$5.47` | `$6.08` | **9.83%** | `1.98%` | `3/9` | `1_NET_CASH_FLOOR` |
| **INAB** | IN8BIO, INC. | `$0.84` | $9.10M | `$1.06` | `$0.99` | `$1.31` | **NR** | `133.22%` | `4/9` | `1_NET_CASH_FLOOR` |
| **NNDM** | Nano Dimension Ltd. | `$1.25` | $247.79M | `$1.56` | `$1.98` | `$2.10` | **NR** | `-4.32%` | `1/9` | `1_NET_CASH_FLOOR` |
| [**IZEA**](https://bobmahalo.github.io/Single-Stock-Scan/IZEA.html) | IZEA Worldwide, Inc. | `$2.18` | $37.97M | `$2.67` | `$2.57` | `$2.58` | **6.25%** | `2.40%` | `7/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS` |
| **CELZ** | CREATIVE MEDICAL TECHNOLOGY  | `$0.61` | $4.63M | `$0.74` | `$0.87` | `$0.87` | **NR** | `194.42%` | `5/9` | `1_NET_CASH_FLOOR` |
| **MED** | MEDIFAST INC | `$12.79` | $143.03M | `$13.58` | `$12.74` | `$16.12` | **-2.71%** | `1.74%` | `4/9` | `1_NET_CASH_FLOOR` |
| **ASBP** | Aspire-Lakewood Holdings, In | `$6.83` | $9.58M | `$6.85` | `$8.33` | `$8.38` | **NR** | `-97.17%` | `3/9` | `1_NET_CASH_FLOOR` |
| **ALZN** | Alzamend Neuro, Inc. | `$1.53` | $7.38M | `$1.51` | `$1.14` | `$1.20` | **NR** | `53.69%` | `2/9` | `1_NET_CASH_FLOOR` |

## Bucket 2: High-FCF Deep Value Turnarounds (`Bucket_2_High_FCF_Turnaround`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **ITP** | IT TECH PACKAGING, INC. | `$0.12` | $1.96M | `$-0.06` | `$0.71` | `$8.96` | **194.39%** | `68.54%` | `6/9` | `2_HIGH_FCF_TURNAROUND` |
| **GTEC** | Greenland Technologies Holdi | `$0.48` | $9.20M | `$1.31` | `$3.21` | `$4.66` | **156.91%** | `40.01%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MOBX** | MOBIX LABS, INC | `$0.56` | $7.10M | `$-0.23` | `$-1.64` | `$-1.75` | **142.12%** | `159.10%` | `6/9` | `2_HIGH_FCF_TURNAROUND` |
| **TOON** | Kartoon Studios, Inc. | `$0.49` | $30.47M | `$0.05` | `$0.36` | `$0.58` | **85.89%** | `29.63%` | `3/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MKTW** | MARKETWISE, INC. | `$21.73` | $63.76M | `$7.34` | `$-124.76` | `$-23.43` | **81.72%** | `12.97%` | `3/9` | `2_HIGH_FCF_TURNAROUND` |
| **FLUX** | Flux Power Holdings, Inc. | `$0.31` | $6.81M | `$-0.16` | `$-0.17` | `$-0.05` | **72.91%** | `2.92%` | `3/9` | `2_HIGH_FCF_TURNAROUND` |
| **WETH** | Wetouch Technology Inc. | `$0.77` | $10.30M | `$9.40` | `$10.02` | `$11.04` | **68.63%** | `12.15%` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **KODK** | EASTMAN KODAK CO | `$7.42` | $728.39M | `$2.01` | `$-0.18` | `$6.37` | **63.84%** | `1.76%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **WTI** | W&T OFFSHORE INC | `$3.12` | $484.05M | `$-1.12` | `$-5.59` | `$-1.23` | **63.01%** | `4.11%` | `4/9` | `2_HIGH_FCF_TURNAROUND` |
| **EBS** | Emergent BioSolutions Inc. | `$5.83` | $300.01M | `$-6.57` | `$-2.41` | `$1.18` | **62.80%** | `-2.10%` | `8/9` | `2_HIGH_FCF_TURNAROUND` |
| [**CRMD**](https://bobmahalo.github.io/Single-Stock-Scan/CRMD.html) | CorMedix Inc. | `$5.22` | $407.26M | `$3.25` | `$0.48` | `$0.93` | **61.49%** | `4.41%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **TTEC** | TTEC Holdings, Inc. | `$1.47` | $72.22M | `$0.31` | `$-14.01` | `$-8.33` | **56.89%** | `1.72%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **PLTK** | Playtika Holding Corp. | `$2.29` | $874.41M | `$-4.98` | `$-7.61` | `$-6.27` | **55.04%** | `1.76%` | `4/9` | `2_HIGH_FCF_TURNAROUND` |
| **PAGP** | PLAINS GP HOLDINGS LP | `$26.41` | $5,225.66M | `$-38.41` | `$-104.00` | `$-13.23` | **45.35%** | `0.08%` | `6/9` | `2_HIGH_FCF_TURNAROUND` |
| **DXC** | DXC Technology Co | `$15.19` | $2,360.82M | `$-13.47` | `$-25.16` | `$7.46` | **43.63%** | `-10.72%` | `6/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **COLL** | COLLEGIUM PHARMACEUTICAL, IN | `$25.08` | $779.37M | `$-3.66` | `$-38.22` | `$-33.21` | **43.15%** | `-1.69%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **SCOR** | COMSCORE, INC. | `$3.29` | $49.88M | `$0.93` | `$-3.99` | `$-6.40` | **39.58%** | `202.79%` | `5/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| [**DLTH**](https://bobmahalo.github.io/Single-Stock-Scan/DLTH.html) | DULUTH HOLDINGS INC. | `$4.07` | $148.07M | `$-2.47` | `$-0.99` | `$4.87` | **38.86%** | `4.98%` | `7/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **KSS** | KOHLS Corp | `$23.95` | $2,715.93M | `$-28.34` | `$-46.07` | `$36.76` | **38.07%** | `1.16%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **MYPS** | PLAYSTUDIOS, Inc. | `$4.66` | $56.13M | `$7.59` | `$6.29` | `$8.07` | **36.12%** | `-4.18%` | `4/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **VSNT** | Versant Media Group, Inc. | `$34.06` | $4,718.60M | `$-13.53` | `$-15.35` | `$-4.13` | **34.76%** | `-3.91%` | `4/9` | `2_HIGH_FCF_TURNAROUND` |
| **GOLD** | Gold.com, Inc. | `$37.56` | $1,095.15M | `$3.10` | `$12.80` | `$15.41` | **34.11%** | `18.31%` | `6/9` | `2_HIGH_FCF_TURNAROUND` |
| **DK** | Delek US Holdings, Inc. | `$62.44` | $3,784.44M | `$-34.91` | `$-54.27` | `$13.11` | **31.75%** | `0.94%` | `5/9` | `2_HIGH_FCF_TURNAROUND` |
| **UFI** | UNIFI INC | `$5.95` | $110.60M | `$-3.81` | `$3.31` | `$12.41` | **31.61%** | `1.24%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PBF** | PBF Energy Inc. | `$68.50` | $8,408.82M | `$-1.12` | `$-8.95` | `$64.75` | **31.22%** | `4.07%` | `2/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **VLGEA** | VILLAGE SUPER MARKET INC | `$42.62` | $179.15M | `$-43.00` | `$-68.19` | `$119.66` | **30.73%** | `NR` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **HOS** | HORNBECK OFFSHORE SERVICES,  | `$5.33` | $785.55M | `$0.28` | `$-0.32` | `$10.73` | **29.96%** | `0.27%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **UPBD** | UPBOUND GROUP, INC. | `$24.88` | $1,450.56M | `$-6.00` | `NR` | `$-0.72` | **29.89%** | `0.68%` | `5/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **PARR** | PAR PACIFIC HOLDINGS, INC. | `$68.93` | $3,451.80M | `$-2.51` | `$5.56` | `$43.80` | **29.75%** | `-0.43%` | `6/9` | `2_HIGH_FCF_TURNAROUND` |
| **HOV** | HOVNANIAN ENTERPRISES INC | `$104.86` | $672.36M | `$-73.80` | `NR` | `$127.68` | **29.42%** | `-6.90%` | `4/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **JVA** | COFFEE HOLDING CO INC | `$4.82` | $27.52M | `$0.17` | `$4.29` | `$4.98` | **28.99%** | `0.00%` | `2/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **VHI** | VALHI INC /DE/ | `$14.54` | $411.93M | `$-12.54` | `$-9.93` | `$24.44` | **28.79%** | `0.07%` | `3/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **PMTS** | CPI Card Group Inc. | `$24.62` | $286.39M | `$-21.98` | `$-17.96` | `$-6.75` | **28.40%** | `2.15%` | `4/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **METC** | Ramaco Resources, Inc. | `$6.20` | $276.93M | `$-5.16` | `$-4.90` | `$8.12` | **28.21%** | `NR` | `3/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **IMMR** | IMMERSION CORP | `$6.63` | $220.16M | `$4.17` | `$5.82` | `$6.92` | **27.77%** | `0.86%` | `5/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| [**CRWS**](https://bobmahalo.github.io/Single-Stock-Scan/CRWS.html) | CROWN CRAFTS INC | `$2.55` | $27.44M | `$-1.78` | `$1.78` | `$3.17` | **27.70%** | `1.85%` | `8/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND` |
| **CRI** | CARTERS INC | `$32.59` | $1,195.63M | `$-17.79` | `$-5.42` | `$15.76` | **26.74%** | `0.67%` | `4/9` | `2_HIGH_FCF_TURNAROUND` |
| **STUB** | StubHub Holdings, Inc. | `$6.29` | $2,382.09M | `$0.71` | `$-4.48` | `$-5.16` | **26.62%** | `24.28%` | `4/9` | `2_HIGH_FCF_TURNAROUND` |
| **ADT** | ADT Inc. | `$9.88` | $7,386.45M | `$-10.24` | `$-15.18` | `$-8.19` | **26.09%** | `NR` | `7/9` | `2_HIGH_FCF_TURNAROUND` |
| **SKYW** | SKYWEST INC | `$79.68` | $3,030.56M | `$-49.43` | `$-96.97` | `$73.76` | **25.19%** | `-5.16%` | `6/9` | `1_NET_CASH_FLOOR | 2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |

## Bucket 3: Cannibal Buybacks (`Bucket_3_Cannibal_Buybacks`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **STRO** | SUTRO BIOPHARMA, INC. | `$9.16` | $151.97M | `$9.02` | `$-7.37` | `$-6.23` | **7.32%** | `-80.44%` | `3/9` | `3_CANNIBAL_BUYBACKS` |
| **IIIV** | i3 Verticals, Inc. | `$19.37` | $378.56M | `$-5.95` | `$-8.35` | `$-7.95` | **13.19%** | `-42.41%` | `5/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **SCHL** | SCHOLASTIC CORP | `$36.87` | $648.91M | `$-21.61` | `$-19.24` | `$21.73` | **3.30%** | `-27.57%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| **AMCX** | AMC Global Media Inc. | `$8.43` | $362.62M | `$-29.56` | `$-35.30` | `$13.40` | **52.54%** | `-23.66%` | `6/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS` |
| **EIG** | Employers Holdings, Inc. | `$47.29` | $829.35M | `$-2.25` | `NR` | `$41.96` | **5.38%** | `-21.98%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **IBTA** | Ibotta, Inc. | `$57.92` | $1,352.38M | `$5.34` | `$5.21` | `$10.21` | **6.02%** | `-20.52%` | `4/9` | `3_CANNIBAL_BUYBACKS` |
| **FOUR** | Shift4 Payments, Inc. | `$43.05` | $3,226.71M | `$-57.35` | `$-67.53` | `$-55.49` | **19.34%** | `-20.08%` | `4/9` | `3_CANNIBAL_BUYBACKS` |
| **PAYC** | Paycom Software, Inc. | `$249.91` | $11,254.64M | `$-13.98` | `$-21.99` | `$13.95` | **5.86%** | `-19.97%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **YEXT** | Yext, Inc. | `$7.64` | $756.15M | `$-1.36` | `$-2.52` | `$-1.55` | **7.01%** | `-19.68%` | `7/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **POST** | Post Holdings, Inc. | `$84.93` | $3,733.25M | `$-173.92` | `$-176.74` | `$-103.34` | **14.82%** | `-19.08%` | `4/9` | `3_CANNIBAL_BUYBACKS` |
| **ACI** | Albertsons Companies, Inc. | `$13.22` | $6,222.13M | `$-33.23` | `$-39.82` | `$-3.81` | **8.47%** | `-18.28%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **BFH** | BREAD FINANCIAL HOLDINGS, IN | `$103.02` | $3,910.77M | `$-14.98` | `$-5.78` | `$71.68` | **45.52%** | `-16.86%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **PRKS** | United Parks & Resorts Inc. | `$37.73` | $1,714.12M | `$-52.10` | `$-64.88` | `$-13.53` | **8.76%** | `-16.71%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **DAN** | DANA Inc | `$22.12` | $2,157.79M | `$-14.07` | `$-11.45` | `$14.46` | **4.03%** | `-16.53%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **ZD** | ZIFF DAVIS, INC. | `$54.36` | $1,799.44M | `$15.54` | `$8.40` | `$18.25` | **6.03%** | `-16.21%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| **PINS** | PINTEREST, INC. | `$19.75` | $11,507.38M | `$0.40` | `$1.18` | `$4.37` | **10.97%** | `-16.11%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **PBI** | PITNEY BOWES INC /DE/ | `$15.62` | $2,117.36M | `$-12.71` | `$-20.54` | `$-11.71` | **23.83%** | `-15.76%` | `6/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **PD** | PagerDuty, Inc. | `$16.20` | $1,274.13M | `$-4.62` | `$-1.68` | `$1.03` | **9.94%** | `-15.65%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| [**NRDS**](https://bobmahalo.github.io/Single-Stock-Scan/NRDS.html) | NERDWALLET, INC. | `$11.54` | $730.39M | `$1.06` | `$2.05` | `$2.92` | **19.99%** | `-15.31%` | `8/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **BFAM** | BRIGHT HORIZONS FAMILY SOLUT | `$55.42` | $2,656.34M | `$-35.29` | `$-50.00` | `$-22.54` | **9.54%** | `-15.25%` | `8/9` | `3_CANNIBAL_BUYBACKS` |
| **DBX** | DROPBOX, INC. | `$35.78` | $8,055.20M | `$0.33` | `$-16.59` | `$-11.85` | **11.36%** | `-15.09%` | `6/9` | `3_CANNIBAL_BUYBACKS` |
| **PGNY** | Progyny, Inc. | `$34.58` | $2,546.72M | `$2.30` | `$2.75` | `$5.28` | **7.05%** | `-14.57%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| [**HOG**](https://bobmahalo.github.io/Single-Stock-Scan/HOG.html) | HARLEY-DAVIDSON, INC. | `$32.60` | $3,292.35M | `$2.08` | `$2.66` | `$29.34` | **9.47%** | `-14.52%` | `8/9` | `1_NET_CASH_FLOOR | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **WRLD** | WORLD ACCEPTANCE CORP | `$148.47` | $692.34M | `$-158.78` | `NR` | `$75.35` | **37.76%** | `-14.37%` | `4/9` | `3_CANNIBAL_BUYBACKS` |
| **CHTR** | CHARTER COMMUNICATIONS, INC. | `$125.69` | $14,699.33M | `$-922.84` | `$-1,378.98` | `$-164.59` | **26.73%** | `-14.26%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **BILL** | BILL Holdings, Inc. | `$50.87` | $4,368.44M | `$-19.64` | `$6.49` | `$8.80` | **9.47%** | `-14.25%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **CRM** | Salesforce, Inc. | `$222.80` | $183,364.40M | `$-36.87` | `$-59.73` | `$-32.82` | **8.26%** | `-13.55%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| **CPRI** | Capri Holdings Ltd | `$21.18` | $2,189.46M | `$-13.35` | `$-19.09` | `$-6.61` | **8.40%** | `-13.26%` | `8/9` | `3_CANNIBAL_BUYBACKS` |
| **SMPL** | Simply Good Foods Co | `$12.61` | $1,094.90M | `$-3.08` | `$-1.74` | `$-0.61` | **14.33%** | `-13.01%` | `5/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **CARS** | Cars.com Inc. | `$13.46` | $700.94M | `$-7.58` | `$-6.77` | `$-4.06` | **21.48%** | `-12.94%` | `6/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS` |
| **ETSY** | ETSY INC | `$91.19` | $7,861.11M | `$-8.30` | `$-14.41` | `$-8.42` | **7.54%** | `-12.66%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **EEFT** | EURONET WORLDWIDE, INC. | `$71.21` | $2,616.09M | `$-51.40` | `$-21.54` | `$0.87` | **11.74%** | `-12.62%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **FCNCA** | FIRST CITIZENS BANCSHARES IN | `$2,301.89` | $25,897.46M | `$-2,117.41` | `NR` | `$1,849.69` | **9.53%** | `-12.44%` | `4/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **TENB** | Tenable Holdings, Inc. | `$44.24` | $4,623.94M | `$-3.31` | `$-9.45` | `$-7.84` | **6.06%** | `-12.43%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| **RICK** | RCI HOSPITALITY HOLDINGS, IN | `$29.35` | $224.37M | `$-31.64` | `$-38.43` | `$1.42` | **15.49%** | `-12.34%` | `6/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **AN** | AUTONATION, INC. | `$187.38` | $5,993.08M | `$-130.97` | `$-268.86` | `$-12.65` | **0.38%** | `-12.31%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **ZG** | ZILLOW GROUP, INC. | `$31.16` | $7,020.50M | `$-3.11` | `$3.01` | `$5.11` | **4.46%** | `-12.07%` | `7/9` | `3_CANNIBAL_BUYBACKS` |
| **CROX** | Crocs, Inc. | `$153.22` | $7,005.99M | `$-32.80` | `$-41.73` | `$-8.13` | **10.76%** | `-11.92%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **FCN** | FTI CONSULTING, INC | `$196.37` | $5,351.90M | `$-36.68` | `$-21.74` | `$2.62` | **6.61%** | `-11.73%` | `5/9` | `3_CANNIBAL_BUYBACKS` |
| **FUSB** | FIRST US BANCSHARES, INC. | `$16.43` | $83.75M | `$3.74` | `NR` | `$17.50` | **10.57%** | `-11.61%` | `5/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |

## Bucket 4: Cluster & C-Suite Insider Buying (`Bucket_4_Cluster_Insider_Buy`)

| Ticker | Company | Price | Market Cap ($M) | Net Cash (Ex-Debt)/Sh | Graham NCAV/Sh | TBV/Sh | FCF Yield | 1Y Shares % | Piotroski | Buckets |
| :--- | :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | :--- |
| **PBLS** | Parabilis Medicines, Inc. | `$27.94` | $3,406.97M | `$8.81` | `$8.18` | `$8.59` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MAIR** | Madison Air Solutions Corp | `$21.40` | $11,345.99M | `$-1.03` | `$-1.88` | `$-0.85` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **BRVE** | Braveheart Bio, Inc. | `$17.42` | $1,568.48M | `$1.36` | `$1.27` | `$-1.07` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SMMT** | Summit Therapeutics Inc. | `$14.39` | $11,512.60M | `$0.76` | `$0.67` | `$0.70` | **-4.58%** | `7.43%` | `1/9` | `4_CLUSTER_INSIDER_BUY` |
| **ROL** | ROLLINS INC | `$38.79` | $18,543.38M | `$-2.08` | `$-2.84` | `$-1.39` | **3.62%** | `-1.36%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| [**GME**](https://bobmahalo.github.io/Single-Stock-Scan/GME.html) | GameStop Corp. | `$24.05` | $12,130.73M | `$-6.81` | `$1.83` | `$12.11` | **5.67%** | `12.70%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **KARD** | Kardigan, Inc. | `$13.94` | $1,303.44M | `$6.25` | `$5.39` | `$6.30` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **DPC** | DPC Holdings PLC | `$27.22` | $4,066.48M | `$1.71` | `$1.95` | `$4.06` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SCTX** | Scribe Therapeutics, Inc. | `$15.52` | $293.73M | `$-0.01` | `$-3.03` | `$-8.71` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LFTO** | Liftoff Mobile, Inc. | `$17.20` | $2,912.50M | `$-6.53` | `$-8.14` | `$-7.18` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **ATTO** | Attovia Therapeutics, Inc. | `$14.98` | $684.08M | `$2.43` | `$2.25` | `$-3.19` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **LILA** | Liberty Latin America Ltd. | `$8.93` | $1,738.67M | `$-45.59` | `$-46.82` | `$-15.15` | **23.19%** | `-6.26%` | `6/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **LYEL** | Lyell Immunopharma, Inc. | `$14.68` | $360.92M | `$5.40` | `$4.27` | `$7.84` | **-38.78%** | `15.87%` | `2/9` | `4_CLUSTER_INSIDER_BUY` |
| **AVO** | Mission Produce, Inc. | `$11.59` | $1,016.19M | `$-4.88` | `$-4.62` | `$4.51` | **-0.23%** | `24.16%` | `8/9` | `4_CLUSTER_INSIDER_BUY` |
| **AVR** | Anteris Technologies Global  | `$5.57` | $542.36M | `$2.53` | `$2.46` | `$2.58` | **-16.26%** | `170.25%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| [**LRN**](https://bobmahalo.github.io/Single-Stock-Scan/LRN.html) | Stride, Inc. | `$75.32` | $3,167.12M | `$-1.38` | `$21.29` | `$33.67` | **15.93%** | `-4.13%` | `7/9` | `2_HIGH_FCF_TURNAROUND | 3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **QTTB** | Q32 Bio Inc. | `$8.86` | $265.13M | `$9.51` | `$9.41` | `$9.61` | **-12.65%** | `143.20%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| **PNAQ** | Pinnacle Acquisition Corp | `$9.78` | NR | `NR` | `NR` | `NR` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **SUJA** | SUJA LIFE, INC. | `$10.21` | $242.77M | `$-7.14` | `$-7.01` | `$-3.58` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **MSM** | MSC INDUSTRIAL DIRECT CO INC | `$110.56` | $6,175.69M | `$-8.28` | `$4.23` | `$11.31` | **3.65%** | `0.12%` | `8/9` | `4_CLUSTER_INSIDER_BUY` |
| **BLSM** | BlossomHill Therapeutics, In | `$12.12` | $385.23M | `$2.30` | `$1.85` | `$-5.50` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **QNT** | Quantinuum Inc. | `$29.85` | $1,012.36M | `$61.15` | `$-19.70` | `$-13.61` | **NR** | `NR` | `NR/9` | `4_CLUSTER_INSIDER_BUY` |
| **RAPP** | Rapport Therapeutics, Inc. | `$23.78` | $1,409.67M | `$6.51` | `$6.41` | `$6.60` | **-8.60%** | `24.38%` | `2/9` | `4_CLUSTER_INSIDER_BUY` |
| **NTSK** | Netskope Inc | `$21.73` | $8,799.62M | `$0.83` | `$-0.42` | `$0.19` | **-0.80%** | `274.71%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **ET** | Energy Transfer LP | `NR` | NR | `$-20.26` | `$-19.78` | `$10.53` | **NR** | `0.32%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **GSHD** | Goosehead Insurance, Inc. | `$56.69` | $2,024.40M | `$-9.78` | `$-14.28` | `$-4.50` | **3.94%** | `-7.37%` | `4/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |
| **BGDE** | Big Digital Energy, Inc. | `$2.58` | $14.61M | `$-7.76` | `$-2.57` | `$2.20` | **-170.33%** | `-72.83%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **CV** | CapsoVision, Inc | `$6.25` | $312.54M | `$-0.01` | `$0.24` | `$0.26` | **-8.92%** | `7.00%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| **UBER** | Uber Technologies, Inc | `$68.80` | $140,482.59M | `$-3.76` | `$-11.87` | `$7.69` | **7.42%** | `-1.73%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **FBIN** | Fortune Brands Innovations,  | `$47.02` | $5,570.73M | `$-19.94` | `$-15.91` | `$-6.62` | **9.96%** | `-1.38%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| **AMR** | Alpha Metallurgical Resource | `$142.96` | $1,810.17M | `$25.50` | `$7.16` | `$114.49` | **-0.76%** | `-1.52%` | `4/9` | `1_NET_CASH_FLOOR | 4_CLUSTER_INSIDER_BUY` |
| **PMTS** | CPI Card Group Inc. | `$24.62` | $286.39M | `$-21.98` | `$-17.96` | `$-6.75` | **28.40%** | `2.15%` | `4/9` | `2_HIGH_FCF_TURNAROUND | 4_CLUSTER_INSIDER_BUY` |
| **TUSK** | MAMMOTH ENERGY SERVICES, INC | `$2.95` | $141.98M | `$0.70` | `$0.62` | `$5.43` | **-100.62%** | `-0.14%` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **GLXY** | Galaxy Digital Inc. | `$12.97` | $2,502.00M | `$-8.93` | `$-4.59` | `$8.95` | **-75.54%** | `-48.11%` | `1/9` | `4_CLUSTER_INSIDER_BUY` |
| **ACDC** | ProFrac Holding Corp. | `$2.67` | $486.27M | `$-6.07` | `$-6.42` | `$0.71` | **-3.27%** | `0.69%` | `3/9` | `4_CLUSTER_INSIDER_BUY` |
| **CDNL** | Cardinal Infrastructure Grou | `$12.55` | $541.47M | `$2.76` | `$3.11` | `$0.23` | **-3.38%** | `NR` | `4/9` | `4_CLUSTER_INSIDER_BUY` |
| **BSX** | BOSTON SCIENTIFIC CORP | `$44.60` | $64,653.75M | `$-8.20` | `$-8.05` | `$0.02` | **5.15%** | `-2.22%` | `7/9` | `4_CLUSTER_INSIDER_BUY` |
| **GLOO** | Gloo Holdings, Inc. | `$2.72` | $228.74M | `$-0.07` | `$-0.52` | `$-0.24` | **-28.98%** | `923.44%` | `6/9` | `4_CLUSTER_INSIDER_BUY` |
| **LWAY** | Lifeway Foods, Inc. | `$22.13` | $334.31M | `$0.43` | `$-0.04` | `$4.46` | **-8.17%** | `-0.79%` | `5/9` | `4_CLUSTER_INSIDER_BUY` |
| [**APTV**](https://bobmahalo.github.io/Single-Stock-Scan/APTV.html) | Aptiv PLC | `$40.92` | $8,283.44M | `$-24.82` | `$-15.92` | `$15.01` | **4.74%** | `-6.32%` | `8/9` | `3_CANNIBAL_BUYBACKS | 4_CLUSTER_INSIDER_BUY` |

---

<details markdown="1">
<summary><b>📖 Open SEC Data Lake Methodology, `68`-Column Schema Dictionary & Forensic Formulas (Click to Expand)</b></summary>

### 1. Why a Normalized SEC XBRL Data Lake?
Publicly traded U.S. operating companies file quarterly (`10-Q`) and annual (`10-K`) financial statements with the SEC using XBRL (`us-gaap` taxonomy). Because different CPA firms use different XBRL tags for identical economic concepts, raw SEC queries frequently return blank cells (`NR`). Our ingestion layer maps ranked tag hierarchies and derived accounting identities ([`xbrl_aliases.yaml`](https://bobmahalo.github.io/morning-briefing/data/xbrl_aliases.yaml)) across **`5,356` active `10-K`/`10-Q` operating companies**, computes discrete Q4 values ($\text{FY} - \text{YTD}_3$), applies 1,000x share-unit scaling guards, and exports **`68` standardized columns**.

### 2. Schema Separation: Un-Opinionated Building Blocks vs. Strategy Buckets

| Column Group | Column Names / Examples | Intended Use Case |
| :--- | :--- | :--- |
| **Identity & Classification (`Cols 1–8`)** | `Ticker`, `CIK`, `Company_Name`, `Exchange`, `SIC_Code`, `SIC_Description`, `Is_Financial_Or_REIT`, `Latest_Period_End` | Universe filtering, sector/SIC peer benchmarking, and filing freshness checks. |
| **Market Pricing & Enterprise Scale (`Cols 9–13`)** | `Share_Price`, `Google_Sheets_Live_Price_Formula`, `Shares_Outstanding_M`, `Market_Cap_M`, `Enterprise_Value_M` | Live valuation multiples and Google Sheets integration. |
| **Per-Share Liquidation Floors & Yields (`Cols 14–24`)** | `Net_Cash_Ex_Debt_Per_Share`, `Graham_NCAV_Per_Share`, `Tangible_Book_Per_Share`, `FCF_Per_Share_TTM`, `FCF_to_Price_Yield_Pct`, `EBIT_to_EV_Yield_Pct` | Downside floor anchoring and inverted yield ranking (avoids negative-denominator P/E distortion). |
| **Raw TTM Flow & Balance Sheet Totals (`Cols 25–39`)** | `Revenue_TTM_M`, `Operating_Income_TTM_M`, `Net_Income_TTM_M`, `Operating_Cash_Flow_TTM_M`, `Free_Cash_Flow_TTM_M`, `Total_Cash_M`, `Total_Debt_M`, `Total_Liabilities_M`, `Stock_Buybacks_TTM_M`, `Stock_Issued_TTM_M`, `Dividends_Paid_TTM_M` | Raw dollar building blocks ($M) so external quants can construct any custom formula without re-parsing SEC filings. |
| **Efficiency, Growth & Share Dilution (`Cols 40–50`)** | `Gross_Margin_TTM_Pct`, `Operating_Margin_TTM_Pct`, `ROIC_TTM_Pct`, `ROIC_5Y_Median_Pct`, `Current_Ratio`, `Revenue_5Y_CAGR_Pct`, `Share_Count_1Y_Change_Pct`, `Share_Count_5Y_CAGR_Pct`, `Shareholder_Yield_Pct` | Quality compounder screening, capital allocation audits, and cannibal buyback tracking. |
| **Forensic Accounting & Insider Flow (`Cols 51–60`)** | `Piotroski_F_Score`, `Altman_Z_Score`, `Altman_Zone`, `Beneish_M_Score`, `SBC_Pct_OCF_TTM`, `Insider_Open_Market_Buys_12M`, `Insider_C_Suite_Buyers_12M`, `Insider_Net_Buy_USD_12M` | Solvency verification, earnings manipulation screening, and OpenInsider Form 4 cluster tracking. |
| **Optional Strategy Sieves (`Cols 61–68`)** | `Is_Dilution_Vampire` (`1,305` flagged), `Bucket_1_Net_Cash_Floor` (`270`), `Bucket_2_High_FCF_Turnaround` (`152`), `Bucket_3_Cannibal_Buybacks` (`509`), `Bucket_4_Cluster_Insider_Buy` (`353`), `Buckets_Count` | Optional deep-value hunting buckets feeding our `41`-stock Stage 1 Convergence Shortlist. |

### 3. Core Mathematical & Forensic Formulas

| Metric | Exact Mathematical Formula | Institutional Interpretation |
| :--- | :--- | :--- |
| **Net Cash (Ex-Debt) / Share** | $$\frac{\text{Cash \& ST Investments} - \text{Total Debt}}{N_{\text{diluted}}}$$ | Hard net cash cushion per share after extinguishing 100% of funded debt. |
| **Graham NCAV / Share** | $$\frac{\text{Current Assets} - \text{Total Liabilities} - \text{Preferred Stock}}{N_{\text{diluted}}}$$ | Benjamin Graham Net-Net liquidation floor (strict arbitrage requires $P \le 0.67 \times \text{NCAV}$). |
| **Tangible Book Value (TBV) / Share** | $$\frac{\text{Stockholders' Equity} - \text{Goodwill} - \text{Intangibles}}{N_{\text{diluted}}}$$ | Physical net worth per share stripping out M&A accounting goodwill. |
| **Altman Z-Score (5-Factor)** | $$Z = 1.2 X_1 + 1.4 X_2 + 3.3 X_3 + 0.6 X_4 + 0.999 X_5$$ | Solvency index across Operating Universe (`> 2.99` Safe, `1.81–2.99` Grey, `< 1.81` Distress). |
| **Step A Dilution Quarantine** | `Share_Count_1Y_Change_Pct > 10%` or (`FCF < 0` & `Stock_Issued > 5% MCap`) | Quarantines `{vampires:,}` chronic equity diluters (`Is_Dilution_Vampire = True`). |

</details>
