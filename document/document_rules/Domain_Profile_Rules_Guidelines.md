# Domain Profile Rules 記述ガイドライン

## 1. 概要

本ドキュメントは、Japan xAPI Profile における Domain Profile（CBT, LMS, eBook, Group Learning Support Tool等）の Statement Template Rules セクションの記述方式を統一するためのガイドラインである。

各 Domain Profile が独立して Rules を定義する際に、以下の原則に従うことで、プロファイル間での解釈の一貫性を確保し、実装者による混乱を低減する。

---

## 2. 基本原則

### 2.1 Rule 粒度の考え方

**Domain Profile ごとに異なる粒度でよい**

- CBT Profile：得点・正誤情報が重要 → 細粒度（9-16項目/テンプレート）
- LMS Profile：課題配布・評価プロセスが重要 → 中程度（4-8項目/テンプレート）
- eBook Profile：ページ閲覧・操作ログが重要 → 簡潔（1-4項目/テンプレート）
- Group Learning Support Tool Profile：協働操作ログが重要 → 簡潔～中程度（0-5項目/テンプレート）

**粒度の統一は必須ではない**。各ドメインの特性に合わせて、必要な詳細度を選択する。

### 2.2 Rules 記述の構成

すべての Domain Profile で以下の統一構成を採用する：

```
#### X.X.X.Y　記述規則（Rules）

1. [JSONPath]
   1. [presence]
   2. [説明]
```

---

## 3. 詳細記述ガイドライン

### 3.1 JSONPath の記述方式

**形式**：`$.path.to.property`（JSONPath 標準形式）

**例**：
- `$.object.definition.name.ja-JP` - オブジェクト定義の日本語名称
- `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` - 拡張フィールド
- `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']` - コンテキスト拡張
- `$.result.score.scaled` - 結果の得点率

**注意点**：
- 拡張フィールドの IRI は **必ずクォーテーション**で囲む
- 言語コード（`ja-JP`, `en`等）も同じく通常の JSONPath 記法に従う
- 配列要素は `[*]` で表記（例：`$.context.contextActivities.grouping[*].id`）

### 3.2 Presence フィールドの定義

| Presence | 説明 | 使用例 |
|---|---|---|
| **included** | 必須。Statement に必ず含む。 | 得点情報、タイムスタンプ |
| **recommended** | 推奨。含まれることが望ましい。 | メタデータ（教科、学年等） |
| **optional** | 任意。含まれる場合と含まれない場合がある。 | ドメイン固有の追加情報 |

### 3.3 説明（ScopeNote）の記述方式

**基本形**：簡潔に 1 行で記述

```
2. 値の説明や注記
```

**拡張形**：値の取り方や条件がある場合、詳細に記述

```
2. [説明]
   - 値の範囲：[範囲]
   - デフォルト値：[値]
   - 条件付き必須の場合は条件を明記
   - Core Profile 参照の場合は「(Core Profile参照)」と明記
```

**例**：
```
1. $.result.score.scaled
   1. included
   2. 得点率 (0.0 - 1.0)
   
2. $.context.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Activity拡張 (Core Profile参照)
   
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/purpose-of-question']
   1. recommended
   2. 問題の趣旨 (Core Profile参照)
```

### 3.4 Extension 拡張フィールドの表記規約

**拡張フィールドの記述時**：以下の順序で記載する

1. 拡張フィールドの IRI
2. Activity拡張か Context拡張かの明記
3. Core Profile 参照か Domain 固有かの明記

**例**：

```
1. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科 (Activity拡張, Core Profile参照)

2. $.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']
   1. recommended
   2. 評価タイプ (Context拡張, Core Profile参照)

3. $.context.extensions['https://w3id.org/japan-xapi/extensions/ebook/launch-reason']
   1. recommended
   2. ビューア起動の理由 (Context拡張, eBook Domain固有)
```

---

## 4. Markdown テーブルの書き方

### 4.1 基本構成

すべての StatementTemplate は Rules リスト の後に、以下の構成の Markdown テーブルを配置する。

```markdown
#### X.X.X.Z　Markdownテーブル

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |
| :--- | :--- | :--- |
| [説明] | [JSONPath] | [Presence] |
```

### 4.2 テーブル列の定義

| 列名 | 説明 | 記述例 |
|---|---|---|
| **項目説明** | 日本語による説明と補注（ScopeNote）。複数行の場合は `<br>` で改行。 | `**教科**<br>Core Profile で定義された教科 Extension。` |
| **Location** | JSONPath 形式での位置。Extensions は IRI をクォーテーション。 | `$.object.definition.extensions['https://...']` |
| **Presence** | included, recommended, optional のいずれか。 | `included` |

### 4.3 テーブル内の説明書き方

**簡潔形**：1 行で記述

```
| **得点率**<br>0.0 から 1.0 の実数。 | `$.result.score.scaled` | included |
```

**詳細形**：複数の情報を含める場合

```
| **教科（Activity拡張）**<br>Core Profile で定義された教科 Extension。推奨値は学習指導要領コードに準じる。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
```

### 4.4 複数拡張がある場合の記述例

```markdown
| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |
| :--- | :--- | :--- |
| **教科（Activity拡張）**<br>Core Profile で定義。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
| **教科（Context拡張）**<br>Core Profile で定義。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
| **評価タイプ**<br>diagnostic(診断的)、formative(形成的)、summative(総括的)のいずれか。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']` | recommended |
```

---

## 5. Core Profile 参照ルール

### 5.1 語彙の分類と参照方法

Domain Profile で使用する語彙は以下の3つに分類される：

**（1） SWG 独自定義語彙** → Core Profile に定義
- SWGにおいて新規に定義された Verb、ActivityType、Extension
- 複数 Domain で使用される共通語彙
- Domain Profile では「Core Profile参照」と表記

**（2） ADL 等の既存標準語彙** → 直接参照（Core に重複定義しない）
- xAPI 標準仕様で既に定義されている Verb（例：completed、attended）
- ADL の ActivityType や Extension
- Domain Profile では条件付きで「既存標準参照」と表記

**（3） Domain 固有語彙** → Domain Profile のみで定義
- 特定 Domain でのみ必要な Extension（例：eBook の launch-reason）
- Domain Profile では「Domain固有」と表記

### 5.2 記述パターン

#### パターン A：SWG独自定義（Core 参照）

**記述方式**：
```
[説明] (Core Profile参照)
```

**例**：
```
1. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科 (Core Profile参照)

2. $.object.definition.type
   1. included
   2. アクティビティタイプ assessment (Core Profile参照)
```

#### パターン B：既存標準語彙（直接参照）

**記述方式**：
```
[説明] (ADL xAPI 標準)
```

**例**：
```
1. $.verb.id
   1. included
   2. 動詞 completed (ADL xAPI 標準語彙)

2. $.object.definition.type
   1. included
   2. アクティビティタイプ http://adlnet.gov/expapi/activities/lesson (ADL xAPI 標準)
```

#### パターン C：Domain 固有語彙

**記述方式**：
```
[説明] ([Domain名] Domain固有)
```

**例**：
```
1. $.context.extensions['https://w3id.org/japan-xapi/extensions/ebook/launch-reason']
   1. recommended
   2. ビューア起動の理由 (eBook Domain固有)
```

### 5.3 新規語彙の検討フロー

Domain Profile の実装時に、Core に定義されていない語彙が必要な場合：

1. **すでに既存標準で定義されているか？**　→　YES → **既存標準を直接参照**（Core に追加しない）
2. **複数 Domain で共通に使用されるか？**　→　YES → **Core への移動を検討** → SWG 決議後に Core に追加
3. **特定 Domain のみで使用されるか？**　→　YES → **Domain 固有として本プロファイルで定義**

**確認フロー**：
- ユーザーに新規語彙の定義を提案
- 共通性の判定
- Core 移行か Domain 固定かを決定

---

## 6. 数値とデータ型の記述規約

### 6.1 スコア・得点情報

| 項目 | 形式 | 範囲 | 説明 |
|---|---|---|---|
| **score.scaled** | float | 0.0 - 1.0 | 正規化得点 |
| **score.raw** | integer | >= 0 | 素点 |
| **score.max** | integer | > 0 | 最大点 |
| **score.min** | integer | >= 0 | 最小点（Optional） |

**記述例**：
```
1. $.result.score.scaled
   1. included
   2. 得点率 (0.0 - 1.0，float)

2. $.result.score.raw
   1. included
   2. 素点 (integer)

3. $.result.score.max
   1. included  
   2. 最大点 (integer)
```

### 6.2 期間・時間情報

ISO 8601 形式に統一する。

| 項目 | 形式 | 説明 | 例 |
|---|---|---|---|
| **timestamp** | ISO 8601 date-time | 活動の発生日時 | `2026-02-09T10:30:00Z` |
| **result.duration** | ISO 8601 duration | 所要時間 | `PT1H30M` (1時間30分) |

**記述例**：
```
1. $.timestamp
   1. included
   2. 活動の発生日時 (ISO 8601 format)

2. $.result.duration
   1. recommended
   2. 所要時間 (ISO 8601 duration, 例: PT1H30M)
```

### 6.3 配列型フィールド

複数の値を取ることを明示する場合：

```
1. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科 (Core Profile参照、配列型)
```

---

## 7. プロファイル間の差異と統一ポイント

### 7.1 粒度の差異（許容される）

| プロファイル | 粒度 | 理由 |
|---|---|---|
| **CBT** | 細粒度（9-16項目） | 得点・正誤判定がドメインの中心 |
| **LMS** | 中程度（4-8項目） | 課題配布・評価が主要プロセス |
| **eBook** | 簡潔（1-4項目） | ページ操作ログが中心で詳細不要 |
| **Group-LST** | 簡潔～中程度（0-5項目） | 協働操作ログが主体 |

**→ 各ドメインの特性に応じて粒度を選択してよい**

### 7.2 統一すべき事項

| 項目 | 統一内容 |
|---|---|
| **Presence 定義** | included / recommended / optional の定義を統一 |
| **JSONPath 形式** | `$.*` 方式で統一 |
| **Extension 表記** | IRI をクォーテーションで統一 |
| **テーブル列構成** | 3列（Item、Location、Presence）で統一 |
| **Core 参照表記** | 「(Core Profile参照)」で統一 |
| **Domain 固有表記** | 「([Domain名] Domain固有)」で統一 |

### 7.3 記載方法の整合性チェックリスト

各 StatementTemplate の Rules を記述した後、以下をチェック：

- [ ] JSONPath は `$.` で始まり、Extensions は IRI がクォーテーションされているか
- [ ] Presence は included / recommended / optional のいずれかか
- [ ] Core Profile 参照の場合「(Core Profile参照)」と記載されているか
- [ ] Domain 固有の場合「([Domain名] Domain固有)」と記載されているか
- [ ] Markdown テーブルの列構成は「項目説明｜Location｜Presence」か
- [ ] 説明は簡潔で、条件がある場合は詳細に記載されているか

---

## 8. 附則：プロファイル実装時のワークフロー

### 8.1 新しい Statement Template を追加する際

1. **テンプレートの目的と判定条件を定義**
   - Verb、objectActivityType を決定（既存参照か新規定義か）

2. **必要な Rule を列挙**
   - included（必須）
   - recommended（推奨）
   - optional（任意）

3. **Rule ごとに説明を作成**
   - JSONPath を指定
   - Presence を決定
   - C値 / 取り方を明記

4. **Markdown テーブルを生成**
   - Rules をテーブル化

5. **Core Profile 確認**
   - 使用する語彙が Core に定義されているか確認
   - 未定義の場合はユーザーに確認してから定義追加

### 8.2 Domain 固有語彙が必要な場合のフロー

```
新規語彙が必要
    ↓
複数ドメインで共通? → Yes → Core Profile に提案
    ↓ No
Domain 固有か
    ↓ Yes
本プロファイルで定義（IRI に [domain] を含める）
    ↓
Rules で「([Domain名] Domain固有)」と記載
```

---

## 参考：各現在のプロファイル構成

### CBT Profile
- StatementTemplate: 4個
- Rules 平均: 9-16項目
- 粒度: 細粒度（推奨仕様含み詳細）

### LMS Profile  
- StatementTemplate: 9個
- Rules 平均: 4-8項目
- 粒度: 中程度

### eBook Profile
- StatementTemplate: 5個
- Rules 平均: 1-4項目  
- 粒度: 簡潔

### Group Learning Support Tool Profile
- StatementTemplate: 6個
- Rules 平均: 0-5項目
- 粒度: 簡潔～中程度

---

**版履歴**

| 版 | 作成日 | 作成者 | 変更内容 |
|---|---|---|---|
| v1.0.0 | 2026-02-09 | ICT CONNECT 21 xAPI SWG | 初版作成 |
