# PandasAI詳細
#AI #PandasAI #Python #データ分析 #会話型

## 概要

**PandasAI**は、Pythonのデータ分析ライブラリPandasとLLMを統合し、**データフレームを対話的に分析**できるオープンソースフレームワーク。「データフレームのChatGPT」とも称され、非エンジニアでも自然言語でデータ分析が可能。

## 基本機能

### コア概念

**会話型データ分析**:
- 自然言語でデータに質問
- 自動コード生成・実行
- 結果の可視化と解釈

**対象ユーザー**:
- データアナリスト
- ビジネスユーザー
- 研究者
- 非技術者

### 基本的な使用例

```python
import pandas as pd
from pandasai import PandasAI

# データフレーム準備
df = pd.read_csv('sales_data.csv')

# PandasAI初期化
pandas_ai = PandasAI()

# 自然言語で質問
result = pandas_ai.run(df, "このデータの概要を教えて")
print(result)

# 可視化も自動生成
pandas_ai.run(df, "年度ごとの売上推移をグラフで表示して")
```

## バージョン別進化

### v2.0（2024年2月リリース）

#### 学習機能

**インストラクション学習**:
```python
# ビジネスルールを教える
agent.train(
    instructions=[
        "売上は必ず税抜きで計算する",
        "四半期は4-6月を Q1とする",
        "ARRは年間経常収益を指す"
    ]
)
```

**Q&A学習**:
```python
# 特定の質問に対する回答パターンを学習
agent.train(
    queries_and_codes=[
        {
            "query": "月次売上トレンドを表示して",
            "code": """
                monthly_sales = df.groupby('month')['revenue'].sum()
                monthly_sales.plot(kind='line', title='月次売上推移')
                """
        }
    ]
)
```

#### データセット説明機能

```python
# 列の意味を事前定義
df_with_description = df.copy()
df_with_description._description = {
    'customer_id': '顧客の一意識別子',
    'purchase_date': '購入日時',
    'amount': '購入金額（税込）',
    'category': '商品カテゴリ'
}
```

#### マルチターン対話

```python
# 文脈を保持した連続質問
agent = PandasAI()

# 最初の質問
result1 = agent.run(df, "今月の売上は？")

# 関連する追加質問（文脈を理解）
result2 = agent.run(df, "前月と比較してどう？")
result3 = agent.run(df, "その要因は何？")
```

#### BigQuery統合

```python
from pandasai.connectors import BigQueryConnector

# BigQuery直接接続
bq_connector = BigQueryConnector(
    project_id="your-project",
    dataset="analytics",
    table="sales_data",
    credentials_path="path/to/credentials.json"
)

# PandasAIで直接クエリ
agent = PandasAI()
result = agent.run(bq_connector, "過去3ヶ月の地域別売上を分析して")
```

### v3.0（2024年夏ベータ版）

#### セマンティックレイヤー

**マルチテーブル対応**:
```python
from pandasai import SemanticAgent

# 複数テーブル間のリレーション定義
semantic_model = {
    "tables": {
        "sales": {
            "columns": ["customer_id", "product_id", "amount", "date"],
            "relationships": {
                "customers": {"on": "customer_id"},
                "products": {"on": "product_id"}
            }
        },
        "customers": {
            "columns": ["customer_id", "name", "segment", "region"]
        },
        "products": {
            "columns": ["product_id", "name", "category", "price"]
        }
    }
}

# セマンティックエージェント作成
agent = SemanticAgent(semantic_model)

# 複数テーブルにまたがる質問
result = agent.run("地域別・商品カテゴリ別の売上分析を作って")
```

#### JSON中間表現

**クエリ構造の可視化**:
```json
{
  "intent": "sales_analysis_by_region_category",
  "operations": [
    {
      "type": "join",
      "tables": ["sales", "customers", "products"],
      "conditions": ["sales.customer_id = customers.customer_id", "sales.product_id = products.product_id"]
    },
    {
      "type": "groupby",
      "columns": ["customers.region", "products.category"]
    },
    {
      "type": "aggregate",
      "function": "sum",
      "column": "sales.amount"
    }
  ],
  "visualization": {
    "type": "heatmap",
    "x_axis": "region",
    "y_axis": "category",
    "values": "total_sales"
  }
}
```

**説明可能性の向上**:
- AIの思考過程を段階的に表示
- 中間結果の検証が可能
- 結果の妥当性チェック支援

## 業界別活用事例

### 保険業界

#### Underwriting（引受査定）

```python
# 自然言語での査定分析
questions = [
    "年齢層と保険種類ごとの平均支払額は？",
    "高リスク案件の特徴を教えて",
    "不正請求の疑いがある案件を抽出して"
]

for question in questions:
    result = agent.run(insurance_df, question)
    print(f"Q: {question}")
    print(f"A: {result}\n")
```

#### 自動レポート生成

```python
# 月次レポート自動作成
monthly_report = agent.run(
    insurance_df, 
    """
    以下の分析を含む月次レポートを作成して：
    1. 新規契約数の推移
    2. 商品別収益性
    3. 解約率の分析
    4. リスク要因の特定
    """
)
```

### マーケティング

#### キャンペーン分析

```python
# ROI分析
campaign_analysis = agent.run(
    marketing_df,
    """
    キャンペーン別のROIを計算し、
    最も効果的なチャネルとターゲット層を特定して。
    結果を可視化も含めて報告して。
    """
)

# 顧客セグメント分析
segment_analysis = agent.run(
    customer_df,
    "顧客を行動パターンでセグメント化し、各セグメントの特徴を分析して"
)
```

#### A/Bテスト分析

```python
# 統計的有意性の自動判定
ab_test_result = agent.run(
    experiment_df,
    """
    A/Bテストの結果を分析して：
    - 統計的有意性の検定
    - 効果サイズの計算
    - 信頼区間の算出
    - ビジネス的解釈の提供
    """
)
```

### 金融分析

#### ポートフォリオ分析

```python
# リスク分析
risk_analysis = agent.run(
    portfolio_df,
    """
    ポートフォリオのリスク要因を分析して：
    1. 各銘柄のリスク貢献度
    2. セクター集中度
    3. 相関リスク
    4. VaRの計算
    """
)

# パフォーマンス分析
performance_report = agent.run(
    returns_df,
    "月次リターンから年率リターン、シャープレシオ、最大ドローダウンを計算して"
)
```

### 研究開発

#### 実験データ分析

```python
# 科学実験データの統計分析
experiment_result = agent.run(
    research_df,
    """
    実験結果を統計的に分析して：
    - 各条件間の有意差検定
    - 効果量の計算
    - 交互作用の分析
    - 結果の可視化
    """
)
```

## 高度な活用パターン

### カスタム関数の組み込み

```python
def custom_business_metric(df):
    """独自のビジネス指標計算"""
    return (df['revenue'] - df['cost']) / df['customer_acquisition_cost']

# PandasAIにカスタム関数を登録
agent.add_custom_function("business_metric", custom_business_metric)

# 自然言語で呼び出し
result = agent.run(df, "business_metricを使って収益性を分析して")
```

### 複数データソース統合

```python
# 異なるソースからのデータ統合分析
sources = {
    "sales": sales_df,
    "marketing": marketing_df,
    "support": support_df
}

# 統合分析
integrated_analysis = agent.run(
    sources,
    """
    売上、マーケティング、サポートデータを統合して
    カスタマージャーニー全体の分析を行って
    """
)
```

### 時系列予測

```python
# 時系列分析と予測
forecast_result = agent.run(
    time_series_df,
    """
    売上データの時系列分析を行い、
    季節性、トレンド、異常値を特定して、
    向こう3ヶ月の予測も作成して
    """
)
```

## パフォーマンス最適化

### 大規模データ対応

```python
# チャンク処理での大規模データ分析
chunk_size = 10000
results = []

for chunk in pd.read_csv('large_dataset.csv', chunksize=chunk_size):
    chunk_result = agent.run(chunk, "月次売上トレンドを計算")
    results.append(chunk_result)

# 結果統合
final_result = pd.concat(results)
```

### キャッシュ機能

```python
# 頻繁な質問の結果をキャッシュ
agent.enable_cache()

# 同じ質問の再実行は高速化
result1 = agent.run(df, "売上サマリーを作成")  # 初回実行
result2 = agent.run(df, "売上サマリーを作成")  # キャッシュから取得
```

## 制限事項・注意点

### 技術的制限

**データサイズ制限**:
- メモリ内処理のため大規模データは分割が必要
- 複雑な集計でのパフォーマンス低下

**AI精度の限界**:
- 複雑なビジネスロジックの理解不足
- ドメイン固有用語の誤解釈
- 統計的手法の不適切な選択

### セキュリティとプライバシー

**データ保護**:
- LLM APIへのデータ送信リスク
- 機密情報の適切なマスキング
- ローカルモデル利用の検討

**アクセス制御**:
- ユーザー権限の管理
- 分析結果の共有範囲制限
- 監査ログの記録

### 結果の妥当性

**Human in the Loop**:
- AI生成コードの確認
- 結果の業務的妥当性チェック
- 異常値や外れ値の検証

## 導入・学習リソース

### 学習パス

1. **基本操作の習得**（1週間）
2. **業務データでの実践**（2-3週間）
3. **高度な機能の活用**（1ヶ月以上）
4. **チーム展開とガバナンス**（継続的）

### サポートコミュニティ

- **公式ドキュメント**: 包括的なAPI仕様
- **GitHub**: オープンソース開発参加
- **Discord**: リアルタイムサポート
- **ブログ**: 業界別活用事例

## 将来展望

### PandaAGI構想

**汎用AIエージェントプラットフォーム**:
- データ分析以外の用途拡張
- マルチモーダル対応
- エージェント間の連携

### エコシステム統合

- **Jupyter Notebook**との深い統合
- **BI툰**（Tableau、Power BI）連携
- **クラウドプラットフォーム**対応強化

---

**関連リンク**
- [[分析向けAIツールまとめ]]
- [[LangChain活用詳細]]
- [[dbt AI支援詳細]]

**Tags:** #PandasAI #Python #会話型分析 #データフレーム #機械学習 #ビジネスインテリジェンス
