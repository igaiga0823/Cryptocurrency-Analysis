# Cryptocurrency-Security-Analysis
安全性の高い暗号資産（“Safe Tokens”）を自動抽出する  
AR-ARCH 予測 × 特徴量抽出 × PCA × DBSCAN クラスタリング



## 概要
本リポジトリは早稲田大学創造理工学研究科五十嵐弘樹の学士研究 **「Analysis of Cryptocurrency Safety via Time-Series Analysis and Feature-Based Classification」** の Python 解析コードとデータをまとめたものです。  

300 超の暗号資産について  

1. **AR-ARCH モデル**で価格・出来高を予測し  
2. **24 個の統計・時間変化・極値特徴量**を抽出  
3. **PCA** で次元圧縮 (3 主成分 ≒ 全分散の 70 %+)  
4. **DBSCAN** により密度ベースでクラスタリング  

を行い、「上場維持率 97 %以上」の **Safe Token** を季次でスクリーニングするワークフローを構築しました。


## リポジトリ構成
（主要ノートブックのみ抜粋）

| フォルダ / ファイル | 役割 |
|--------------------|------|
|  |
| `get_2024_data.ipynb` | 2024 Q1 の価格・出来高データ取得 |
| `get_delisted_data.ipynb` | BINANCE で上場廃止になったトークン一覧取得 |
| `make_price_model.ipynb` / `make_volume_model.ipynb` | AR-ARCH モデル学習 & 予測系列生成 |
| `get_feature.ipynb` | 24 特徴量計算 |
| `check_feature.ipynb` | PCA 適用 & 主成分解析 |
| `judge_stock.ipynb` | DBSCAN によるクラスタリング＆安全度判定 |
| `safe_index.ipynb` | Precision 等メトリクス計算、可視化 |


## 環境
- Python ≥ 3.9  
- 推奨 `python=3.10`  
- 使用ライブラリ   

```bash
pip install pandas numpy scipy statsmodels scikit-learn pycoingecko matplotlib tqdm
```

## データソース
CoinGecko API – 価格・出来高データ

BINANCE – 上場 / 上場廃止判定（2024年）

#### API 規約に従い、商用利用時は各サービスの利用許諾を確認してください。


## 結果ハイライト
2023 年データ → Safe Token = 37 銘柄 / Precision 97.3 %

2024 Q1 実データ → Precision 97.8 %

詳細グラフ・テーブルは safe_index.ipynb を参照。

## 今後の課題
外生情報（ニュースセンチメント・規制イベント）の統合

極端リスク捕捉のためのモデル改良（他の時系列モデル（GARCH Model）、機械学習モデル、深層学習モデル等）
