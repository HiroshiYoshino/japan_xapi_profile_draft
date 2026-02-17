# Domain Profile 記述ガイドライン

## 1. 概要

本ドキュメントは、Japan xAPI Profile における Domain Profile（CBT, LMS, eBook, Group Learning Support Tool等）の記述方式を統一するためのガイドラインである。

各 Domain Profile が Statement Template および Rules を定義する際に、本ガイドラインに従うことで、プロファイル間での解釈の一貫性を確保し、実装者による混乱を低減する。

---

## 2. Domain Profile の位置づけ

### 2.1 全体アーキテクチャにおける役割

Japan xAPI Profileは以下の階層構造を持つ：

- **Core Concept Profile（語彙の核）**
  - 日本独自 Concept（verbs / activityTypes / extensions 等）を定義
  - Domain に共通する語彙を集約
  - Pattern / Template は Core には原則置かない
  - ルールは Domain 側へ

- **Domain Template Profile（ebook / cbt / lms / group-lst …）**
  - 各TFのプロファイルを、「Domain Template Profile」と呼ぶ
  - Statement Templates / Patterns を中心に定義
  - verb/activityType は Core または既存（ADL 等）を参照（再定義しない）
  - 参考：[xAPI Profiles Structure](https://adlnet.github.io/xapi-profiles/xapi-profiles-structure.html)

- **Catalog / Registry（運用補助）**
  - Profile 間の依存・互換（例：ebook 1.0.0 は core 1.x を前提）
  - IRI 一覧、命名規則、廃止（deprecate）情報
  - ※仕様上必須ではないが、複数Profile運用で極めて有効

### 2.2 Domain Profile の特徴

- **役割**: どのVerbを、どんな条件で使うかを「規定」する場所
- **特徴**:
  - templates がメイン（concepts は空）
  - ADLやCoreのVerbを参照する
  - 各Domainプロファイルで共通のlaunchedなども各Domainプロファイルに記述する

---

## 3. ドキュメント構成

### 3.1 必須セクション

すべての Domain Profile は以下の構成に従う：

#### 1. 本ドキュメントについて

##### 1.1 位置づけ
- 本プロファイルの標準仕様としての位置づけを記述
- 対象とする学習ログの範囲を明示

**記述例：**
```markdown
本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである[ドメイン名]TFにおける学習ログを対象として取りまとめた **Japan xAPI [Domain] Profile** 標準仕様である。
```

##### 1.2 目的
- プロファイルの策定目的を記述

##### 1.3 前提条件
- xAPIプロファイル仕様への準拠を明記
- Core Profileへの語彙定義委譲を説明
- 省略する項目（id, type, inSchema, prefLabel）とその理由を記載

**統一記述（必須）：**
```markdown
本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。
本ドキュメントに記載されるStatementTemplateで使用される語彙（Verb、ActivityType、Extension等）は以下のいずれかに整理される。(1) SWG独自に定義した語彙を使用する場合、Core Profile内のConceptsに定義されている。(2) ADLや他の標準で定義済みの語彙を使用する場合、それらを直接参照し、Domain Profileで再定義しない。Domain Profile（本プロファイルはDomain Profileの1つ）として[Domain] Profileは Statement Templateおよび Rules の定義に集中し、語彙定義はCore Profileに委譲する。
各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。
```

省略項目の理由（4項目すべて記載）：
- **idに期待されるURI**: プロファイル公開形態確定後に設計されるべき
- **typeに期待される固定値StatementTemplate**: 章構成で明示済み
- **inSchemaに期待されるURI**: 文書構成で管理済み
- **prefLabel**: 見出しで識別可能

##### 1.4 定義範囲
- メタ情報、StatementTemplate、Rulesを定義対象とすることを明記
- patternsは定義対象外（非線形特性のため）

##### 1.5 本ドキュメントの構成について
- プロファイルに含まれる要素を列挙

#### 2. メタ情報

##### 2.1 本章の位置づけ
- メタ情報の役割を説明

##### 2.2 構成要素
- プロファイルのメタ情報項目を表形式で記載

**必須項目（すべてのDomainで統一）：**

| 項目                     | 説明                                   | 値の例                                                       |
| :----------------------- | :------------------------------------- | :----------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/[domain]`              |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                    |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                         |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI [Domain] Profile                                  |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                       |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                      |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                   |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                       |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育における[ドメイン]学習ログ標準プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                   |

##### 2.3 共通記述規則

すべてのStatementTemplateに適用される共通Rulesを表形式で記載。

**必須テーブル（すべてのDomainで統一）：**

| 項目                               | Location (JSONPath)                        | Presence    |
| :--------------------------------- | :----------------------------------------- | :---------- |
| **ステートメントID**               | `$.id`                                     | included    |
| **タイムスタンプ**                 | `$.timestamp`                              | included    |
| **アクター**                       | `$.actor`                                  | included    |
| **アクターのオブジェクトタイプ**   | `$.actor.objectType`                       | included    |
| **アクターのアカウントホームページ** | `$.actor.account.homePage`                 | included    |
| **アクターのアカウント名**         | `$.actor.account.name`                     | included    |
| **動詞の表示名(英語)**             | `$.verb.display.en`                        | included    |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType`                      | included    |
| **オブジェクトID**                 | `$.object.id`                              | included    |
| **オブジェクト定義のタイプ**       | `$.object.definition.type`                 | included    |
| **オブジェクト定義の名称(日本語)** | `$.object.definition.name['ja-JP']`        | recommended |
| **オブジェクト定義の説明(日本語)** | `$.object.definition.description['ja-JP']` | recommended |
| **コンテキスト**                   | `$.context`                                | included    |
| **コンテキストの言語**             | `$.context.language`                       | included    |
| **コンテキストのプラットフォーム** | `$.context.platform`                       | included    |
| **プロファイルバージョン**         | `$.version`                                | included    |

#### 3. ユースケース（ドメイン固有）

Domain Profile は以下の3.1～3.3の構成で記述する。

##### 3.1 本章の位置づけ
- 対象ドメインにおける学習活動の特性を述べる
- 本プロファイルで定義するStatementTemplateの背景にある考え方を示す

##### 3.2 [ドメイン特性と主な活動]
- ドメインの特性を記述（例：非線形行動、協働特性、等）
- 主な学習活動の例を列挙

##### 3.3 本プロジェクトの成果と今後の課題

**本プロジェクトの成果**
- 本プロファイルで定義されたStatementTemplateの範囲と実装内容を記述
- プロファイルに含まれる学習ログ記録機能を簡潔に説明
- スコープ外の機能や今後の課題への前置きを記述

**今後の課題**
- 番号付きリストで、実装仕様の拡張や改善の方向性を列挙
- 複数項目記載を推奨（3～4項目程度）
- 各項目は簡潔に1行で説明した後、詳細があれば続ける

#### 4. StatementTemplate

##### 4.1 本章の位置づけ
- StatementTemplateの役割を説明

##### 4.2 前提条件
- 基本仕様、記述規則（Rules）、Markdownテーブルの構成を説明

##### 4.3 StatementTemplate一覧
- 各Templateを以下の構成で記述

---

## 4. StatementTemplate の記述方式

### 4.1 基本構成

各 StatementTemplate は以下の3つのセクションで構成される：

#### X.X.X.1　基本仕様
- Templateの目的と記録対象操作の説明
- 識別情報（3要素）
- 判定条件（Verb, objectActivityType）

**記述例：**
```markdown
#### 4.3.1.1　基本仕様

- [操作内容]を記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                             |
| :------- | :--------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/[domain]/[template-name] |
| inScheme | https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0            |
| prefLabel | [テンプレート名]                                              |

- 判定条件

| 項目              | 値                              |
| :---------------- | :------------------------------ |
| verb              | [Verb IRI]                      |
| objectActivityType | [ActivityType IRI] (該当する場合) |
```

#### X.X.X.2　記述規則（Rules）
- Statement内の各プロパティに対する制約を番号付きリストで記述

**記述形式：**
```markdown
#### X.X.X.2　記述規則（Rules）

1. [JSONPath]
   1. [presence]
   2. [説明]
```

#### X.X.X.3　Markdownテーブル
- システム設計・実装用の一覧表

---

## 5. Rules 記述の詳細ガイドライン

### 5.1 Rule 粒度の考え方

**Domain Profile ごとに異なる粒度でよい**

各ドメインの特性に合わせて、必要な詳細度を選択する：

| Domain | 粒度 | 理由 |
|---|---|---|
| **CBT** | 細粒度（9-16項目/テンプレート） | 得点・正誤情報が重要 |
| **LMS** | 中程度（4-8項目/テンプレート） | 課題配布・評価プロセスが重要 |
| **eBook** | 簡潔（1-4項目/テンプレート） | ページ閲覧・操作ログが重要 |
| **Group-LST** | 簡潔～中程度（0-5項目/テンプレート） | 協働操作ログが重要 |

**粒度の統一は必須ではない**。各ドメインの特性に合わせて調整可能。

### 5.2 JSONPath の記述方式

**形式**：`$.path.to.property`（JSONPath 標準形式）

**例**：
- `$.object.definition.name.ja-JP` - オブジェクト定義の日本語名称
- `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` - 拡張フィールド
- `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']` - コンテキスト拡張
- `$.result.score.scaled` - 結果の得点率

**注意点**：
- 拡張フィールドの IRI は **必ずクォーテーション**で囲む
- 言語コード（`ja-JP`, `en`等）も JSONPath 記法に従う
- 配列要素は `[*]` で表記（例：`$.context.contextActivities.grouping[*].id`）

### 5.3 Presence フィールドの定義

| Presence | 説明 | 使用例 |
|---|---|---|
| **included** | 必須。Statement に必ず含む。 | 得点情報、タイムスタンプ |
| **recommended** | 推奨。含まれることが望ましい。 | メタデータ（教科、学年等） |
| **optional** | 任意。含まれる場合と含まれない場合がある。 | ドメイン固有の追加情報 |

### 5.4 説明（ScopeNote）の記述方式

**基本形**：簡潔に 1 行で記述

```
2. 値の説明や注記
```

**拡張形**：値の取り方や条件がある場合、詳細に記述

```
2. [説明]
   - 値の範囲：[範囲]
   - 値の例：[例]
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

### 5.5 Extension 拡張フィールドの表記規約

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

## 6. Markdown テーブルの記述方式

### 6.1 基本構成

すべての StatementTemplate は Rules リスト の後に、以下の構成の Markdown テーブルを配置する。

```markdown
#### X.X.X.3　Markdownテーブル

| 項目 | 説明 | Location (JSONPath) | Presence |
| :--- | :--- | :--- | :--- |
| [項目名] | [説明] | [JSONPath] | [Presence] |
```

### 6.2 テーブル列の定義

| 列名 | 説明 | 記述例 |
|---|---|---|
| **項目** | 項目名。 | `**教科**` |
| **説明** | 日本語による説明と補注（ScopeNote）。複数行の場合は `<br>` で改行。 | `Core Profile で定義された教科 Extension。` |
| **Location** | JSONPath 形式での位置。Extensions は IRI をクォーテーション。 | `$.object.definition.extensions['https://...']` |
| **Presence** | included, recommended, optional のいずれか。 | `included` |

### 6.3 テーブル内の説明書き方

**簡潔形**：1 行で記述

```
| **得点率** | 0.0 から 1.0 の実数。 | `$.result.score.scaled` | included |
```

**詳細形**：複数の情報を含める場合

```
| **教科（Activity拡張）** | Core Profile で定義された教科 Extension。推奨値は学習指導要領コードに準じる。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
```

### 6.4 複数拡張がある場合の記述例

```markdown
| 項目 | 説明 | Location (JSONPath) | Presence |
| :--- | :--- | :--- | :--- |
| **教科（Activity拡張）** | Core Profile で定義。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
| **教科（Context拡張）** | Core Profile で定義。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
| **評価タイプ** | diagnostic(診断的)、formative(形成的)、summative(総括的)のいずれか。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']` | recommended |
```

---

### 6.5 注記（[!NOTE]）

RulesやMarkdownテーブルの補足説明は、必要に応じて [!NOTE] ブロックで記述する。

**例**:
```markdown
> [!NOTE]
> - 採点が未実施の場合は result.score を出力しない。
> - 数値の丸めは小数点以下7桁・8桁目を四捨五入とする。
```

## 7. Core Profile 参照ルール

### 7.1 語彙の分類と参照方法

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

### 7.2 記述パターン

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

### 7.3 新規語彙の検討フロー

Domain Profile の実装時に、Core に定義されていない語彙が必要な場合：

1. **すでに既存標準で定義されているか？**　→　YES → **既存標準を直接参照**（Core に追加しない）
2. **複数 Domain で共通に使用されるか？**　→　YES → **Core への移動を検討** → SWG 決議後に Core に追加
3. **特定 Domain のみで使用されるか？**　→　YES → **Domain 固有として本プロファイルで定義**

**確認フロー**：
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

## 8. 数値とデータ型の記述規約

### 8.1 スコア・得点情報

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

### 8.2 期間・時間情報

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

### 8.3 配列型フィールド

複数の値を取ることを明示する場合：

```
1. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科 (Core Profile参照、配列型)
```

---

## 9. プロファイル間の統一事項と差異

### 9.1 粒度の差異（許容される）

各ドメインの特性に応じて粒度を選択してよい。

### 9.2 統一すべき事項

| 項目 | 統一内容 |
|---|---|
| **Presence 定義** | included / recommended / optional の定義を統一 |
| **JSONPath 形式** | `$.*` 方式で統一 |
| **Extension 表記** | IRI をクォーテーションで統一 |
| **テーブル列構成** | 4列（項目、説明、Location、Presence）で統一 |
| **Core 参照表記** | 「(Core Profile参照)」で統一 |
| **Domain 固有表記** | 「([Domain名] Domain固有)」で統一 |
| **共通記述規則** | 2.3節の17項目テーブルで統一 |
| **メタ情報項目** | 2.2節の10項目で統一 |

### 9.3 記載方法の整合性チェックリスト

各 StatementTemplate の Rules を記述した後、以下をチェック：

- [ ] JSONPath は `$.` で始まり、Extensions は IRI がクォーテーションされているか
- [ ] Presence は included / recommended / optional のいずれかか
- [ ] Core Profile 参照の場合「(Core Profile参照)」と記載されているか
- [ ] Domain 固有の場合「([Domain名] Domain固有)」と記載されているか
- [ ] Markdown テーブルの列構成は「項目｜説明｜Location｜Presence」か
- [ ] 説明は簡潔で、条件がある場合は詳細に記載されているか

---

## 10. プロファイル実装時のワークフロー

### 10.1 新しい Statement Template を追加する際

1. **テンプレートの目的と判定条件を定義**
   - Verb、objectActivityType を決定（既存参照か新規定義か）

2. **必要な Rule を列挙**
   - included（必須）
   - recommended（推奨）
   - optional（任意）

3. **Rule ごとに説明を作成**
   - JSONPath を指定
   - Presence を決定
   - 値 / 取り方を明記

4. **Markdown テーブルを生成**
   - Rules をテーブル化

5. **Core Profile 確認**
   - 使用する語彙が Core に定義されているか確認
   - 未定義の場合は新規語彙検討フローに従う

### 10.2 Domain 固有語彙が必要な場合のフロー

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

## 11. JSON-LD ファイルの構成

### 11.1 Domain Profile の JSON-LD 構造

#### ファイル: [domain]/v1.0.0/profile.jsonld

```json
{
  "@context": "https://w3id.org/xapi/profiles/context",
  "id": "https://w3id.org/japan-xapi/profiles/[domain]",
  "type": "Profile",
  "prefLabel": { "ja": "Japan xAPI [Domain] Profile" },
  "versions": [
    {
      "id": "https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0",
      "generatedAtTime": "2026-04-01"
    }
  ],
  "publisher": {
    "type": "Organization",
    "name": "ICT CONNECT 21 xAPI SWG"
  },

  "concepts": [], // 基本的に空（用語定義はCoreに任せるため）

  // ▼【重要】ここで「既存Verb」と「Core定義Verb」を組み合わせてルールを作る
  "templates": [
    {
      "id": "https://w3id.org/japan-xapi/templates/[domain]/[template-name]",
      "inScheme": "https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0",
      "prefLabel": { "ja": "[テンプレート名]" },
      "definition": {
        "ja": "[テンプレートの説明]"
      },

      // 1. Verbの指定（ADLの既存Verbまたは Core 定義Verbを参照）
      "verb": "[Verb IRI]",

      // 2. Objectの指定（ADLの既存ActivityTypeまたは Core 定義を参照）
      "objectActivityType": "[ActivityType IRI]",

      // 3. ルール（必須項目の定義）
      "rules": [
        {
          "location": "[JSONPath]",
          "presence": "included|recommended|optional"
        }
      ]
    }
  ],

  // テンプレートの順序や構造を定義（オプションだが推奨）
  "patterns": []
}
```

---

## 12. 附則

### 12.1 更新履歴

| 日付 | バージョン | 変更内容 |
|---|---|---|
| 2026-02-11 | v1.0.0 | 初版作成（既存ガイドラインと全体アーキテクチャを統合） |

### 12.2 参考資料

- [xAPI Profile Specification](https://github.com/adlnet/xapi-profiles)
- [xAPI Profiles Structure](https://adlnet.github.io/xapi-profiles/xapi-profiles-structure.html)
- Japan xAPI Core Profile Guidelines
- 全体アーキテクチャ.md（統合済み）
- Domain_Profile_Rules_Guidelines.md（統合済み）

---
