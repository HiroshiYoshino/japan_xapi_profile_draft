# Core Profile 記述ガイドライン

## 1. 概要

本ドキュメントは、Japan xAPI における **Core Concept Profile**（以下、Core Profile）の記述方式を定めるガイドラインである。

Core Profile は、日本の初等中等教育分野において共通に使用される xAPI 語彙（Verb、ActivityType、Extension 等）を定義し、各 Domain Profile（CBT、LMS、eBook、Group Learning Support Tool 等）から参照される基盤となるプロファイルである。

---

## 2. Core Profile の位置づけ

### 2.1 全体アーキテクチャにおける役割

Japan xAPI Profileは以下の階層構造を持つ：

- **Core Concept Profile（語彙の核）** ← 本ガイドラインの対象
  - 日本独自 Concept（verbs / activityTypes / extensions 等）を定義
  - Domain に共通する語彙を集約
  - Pattern / Template は Core には原則置かない
  - ルールは Domain 側へ

- **Domain Template Profile（ebook / cbt / lms / group-lst …）**
  - 各TFのプロファイルを、「Domain Template Profile」と呼ぶ
  - Statement Templates / Patterns を中心に定義
  - verb/activityType は Core または既存（ADL 等）を参照（再定義しない）

- **Catalog / Registry（運用補助）**
  - Profile 間の依存・互換（例：ebook 1.0.0 は core 1.x を前提）
  - IRI 一覧、命名規則、廃止（deprecate）情報
  - ※仕様上必須ではないが、複数Profile運用で極めて有効

### 2.2 Core Profile の特徴

- **役割**: 組織独自のVerb、ActivityType、Extensionsを「定義」する場所
- **特徴**:
  - **concepts がメイン**（templates は基本的になし）
  - **既存(ADL等)のVerbは書かない**（新規定義のみ）
  - Domain Profile から参照される語彙の定義に集中

---

## 3. Core Profile の構成

### 3.1 ドキュメント構成

#### 必須セクション

Core Profile のドキュメントは以下の構成に従う：

##### 1. 本プロファイルの位置づけ
- Core Profile としての役割を明記
- Domain Profile との関係を説明

##### 2. 目的
- 共通語彙の定義と管理の目的を記述

##### 3. 前提条件
- xAPI Profile 仕様への準拠を明記
- ADL 等の既存標準との関係を説明

##### 4. 定義範囲
- Concepts の定義を対象とすることを明記
- Templates / Patterns は対象外であることを明記

##### 5. 本ドキュメントの構成
- プロファイルに含まれる要素を列挙

##### 6. メタ情報
- プロファイル全体のメタデータを記載

##### 7. バージョン履歴
- 改訂履歴を記録

##### 8. Concepts
- Verb、ActivityType、Extension 等の語彙定義

##### 9. Context Category / Parent Activity 等の語彙（将来拡張）
- 現バージョンではスコープ外

### 3.2 JSON-LD 構成

Core Profile の JSON-LD ファイルには以下の要素を含む：

- **メタ情報**（id, type, conformsTo, prefLabel, definition, versions, publisher, languages）
- **バージョン履歴**（versions セクション）
- **Concepts**（Verb, ActivityType, Extension の定義）
- **Templates**（基本的に空）
- **Patterns**（基本的に空）

---

## 4. メタ情報

### 4.1 プロファイル識別とメタ情報

以下の項目は、SWGとして統一の内容とする：

| 項目                     | 説明                                   | Core Profile の値                                            |
| :----------------------- | :------------------------------------- | :----------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/core`                  |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                    |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                         |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI Core Profile                                      |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                       |
| 作成者/管理者 publisher  | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                      |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                   |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語, English                                              |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育を主対象とする学習ログ（xAPI Statement）の共通語彙（Concept）を定義するコア・プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                   |

### 4.2 バージョン履歴

versions セクションには以下の情報を含む：

- **本バージョンの識別子**（IRI）
- **wasRevisionOf**（直前版へのリンク）
- **変更点**（changelog / notes）
- **互換性メモ**：breaking / non-breaking の区別（推奨）

**記述例（JSON-LD）：**
```json
"versions": [
  {
    "id": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
    "generatedAtTime": "2026-04-01",
    "wasRevisionOf": "https://w3id.org/japan-xapi/profiles/core/v0.9.0"
  }
]
```

---

## 5. Concepts の定義

### 5.1 Concepts の対象

Core Profile で定義する Concepts は以下の4つ：

1. **Verb**（動詞）
2. **ActivityType**（アクティビティタイプ）
3. **Extension**（拡張フィールド）
4. **その他**（将来拡張：Context Category / Parent Activity 等）

**重要原則**：
- **新しく作る言葉だけを書く**
- **ADLの言葉は書かない**（既存標準は Domain Profile から直接参照）

### 5.2 Actor（アクター）

ドキュメントでの記述：
- 全てのStatementで `Agent` を使用することを明記
- 特別な定義は Core に含めない（xAPI 標準に準拠）

### 5.3 Verb（動詞）

#### 5.3.1 定義対象

- **SWG 独自に定義した動詞**のみを記載
- ADL 等の既存標準で定義済みの Verb（例：completed, attempted）は記載しない

#### 5.3.2 記述形式（Markdown）

```markdown
#### Verb: [動詞名]

- **IRI**: `https://w3id.org/japan-xapi/verbs/[verb-id]`
- **prefLabel**:
  - ja: [日本語表示名]
  - en: [英語表示名]
- **definition**:
  - ja: [日本語定義]
  - en: [英語定義]
- **使用例**: [どのような場面で使用されるかの説明]
```

**例：**
```markdown
#### Verb: highlighted

- **IRI**: `https://w3id.org/japan-xapi/verbs/highlighted`
- **prefLabel**:
  - ja: ハイライトした
  - en: highlighted
- **definition**:
  - ja: テキストや画像の一部を強調表示する行為。
  - en: The act of highlighting a part of text or image.
- **使用例**: 電子書籍でテキストをハイライトした際に使用。
```

#### 5.3.3 記述形式（JSON-LD）

```json
{
  "id": "https://w3id.org/japan-xapi/verbs/[verb-id]",
  "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
  "type": "Verb",
  "prefLabel": {
    "ja": "[日本語表示名]",
    "en": "[英語表示名]"
  },
  "definition": {
    "ja": "[日本語定義]",
    "en": "[英語定義]"
  }
}
```

### 5.4 ActivityType（アクティビティタイプ）

#### 5.4.1 定義対象

- **SWG 独自に定義したアクティビティタイプ**のみを記載
- ADL 等の既存標準で定義済みの ActivityType（例：assessment, lesson）は記載しない

#### 5.4.2 記述形式（Markdown）

```markdown
#### ActivityType: [アクティビティタイプ名]

- **IRI**: `https://w3id.org/japan-xapi/activity-types/[type-id]`
- **prefLabel**:
  - ja: [日本語表示名]
  - en: [英語表示名]
- **definition**:
  - ja: [日本語定義]
  - en: [英語定義]
- **使用例**: [どのような場面で使用されるかの説明]
```

#### 5.4.3 記述形式（JSON-LD）

```json
{
  "id": "https://w3id.org/japan-xapi/activity-types/[type-id]",
  "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
  "type": "ActivityType",
  "prefLabel": {
    "ja": "[日本語表示名]",
    "en": "[英語表示名]"
  },
  "definition": {
    "ja": "[日本語定義]",
    "en": "[英語定義]"
  }
}
```

### 5.5 Extension（拡張フィールド）

#### 5.5.1 Extension の分類

Extension は以下の2つに分類される：

1. **Activity Extension**（Activity 定義に含まれる拡張）
   - `object.definition.extensions` に配置
2. **Context Extension**（Context に含まれる拡張）
   - `context.extensions` に配置

#### 5.5.2 定義対象

- 教科、学年、学習指導要領コード等のメタデータ項目
- 複数 Domain で共通に使用される拡張フィールド

**重要事項**：
- **プロパティ名（キー）を規定**する
- メタデータの記載ルール（値の形式）については、Core Profile では規定しない（Domain Profile に委ねる）

#### 5.5.3 記述形式（Markdown）

```markdown
#### Extension: [拡張フィールド名]

- **IRI**: `https://w3id.org/japan-xapi/extensions/[extension-id]`
- **type**: `ActivityExtension` または `ContextExtension`
- **prefLabel**:
  - ja: [日本語表示名]
  - en: [英語表示名]
- **definition**:
  - ja: [日本語定義]
  - en: [英語定義]
- **使用例**: [どのような場面で使用されるかの説明]
- **値の形式**: [推奨される値の形式や例]
```

**例：**
```markdown
#### Extension: difficulty

- **IRI**: `https://w3id.org/japan-xapi/extensions/difficulty`
- **type**: `ContextExtension`
- **prefLabel**:
  - ja: 難易度
  - en: difficulty
- **definition**:
  - ja: 学習コンテンツの難易度を示す（1-5など）。
  - en: Indicates the difficulty level of the learning content (e.g., 1-5).
- **使用例**: CBT問題の難易度を記録する際に使用。
- **値の形式**: 整数（例：1, 2, 3, 4, 5）
```

#### 5.5.4 記述形式（JSON-LD）

```json
{
  "id": "https://w3id.org/japan-xapi/extensions/[extension-id]",
  "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
  "type": "ContextExtension",
  "prefLabel": {
    "ja": "[日本語表示名]",
    "en": "[英語表示名]"
  },
  "definition": {
    "ja": "[日本語定義]",
    "en": "[英語定義]"
  }
}
```

#### 5.5.5 Core Profile に定義する拡張フィールド一覧

Core Profile では以下の 11 個の拡張フィールドを定義し、各 Domain Profile で活用される：

**1. subject（教科）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/subject`
- **type**: `ActivityExtension` および `ContextExtension`（両方で使用可能）
- **prefLabel**:
  - ja: 教科
  - en: subject
- **definition**:
  - ja: 学習コンテンツが対象とする教科を示す
  - en: Indicates the school subject targeted by learning content
- **Scope Note**: 複数の教科に対応可能
- **Schema**: `type: array, items: { type: string }`

**2. grade（学年）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/grade`
- **type**: `ActivityExtension` および `ContextExtension`
- **prefLabel**:
  - ja: 学年
  - en: grade
- **definition**:
  - ja: 学習コンテンツが対象とする学年を示す
  - en: Indicates the grade level targeted by learning content
- **Scope Note**: 複数の学年に対応可能
- **Schema**: `type: array, items: { type: string }`

**3. course-of-study-code（学習指導要領コード）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/course-of-study-code`
- **type**: `ActivityExtension` および `ContextExtension`
- **prefLabel**:
  - ja: 学習指導要領コード
  - en: course of study code
- **definition**:
  - ja: 文部科学省が定める学習指導要領のコード体系に基づくコードを示す
  - en: Indicates a code based on the course of study code system defined by the Ministry of Education, Culture, Sports, Science and Technology
- **Scope Note**: 複数のコードに対応可能
- **Schema**: `type: array, items: { type: string }`

**4. unit（単元）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/unit`
- **type**: `ActivityExtension` および `ContextExtension`
- **prefLabel**:
  - ja: 単元
  - en: unit
- **definition**:
  - ja: 学習の単元名を示す
  - en: Indicates the name of a learning unit
- **Scope Note**: 複数の単元に対応可能
- **Schema**: `type: array, items: { type: string }`

**5. purpose-of-question（問題の趣旨）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/purpose-of-question`
- **type**: `ActivityExtension`
- **prefLabel**:
  - ja: 問題の趣旨
  - en: purpose of question
- **definition**:
  - ja: CBT/ドリル等の問題の出題意図・趣旨を示す
  - en: Indicates the purpose or intent of a question in CBT/drill assessments
- **Scope Note**: 複数の趣旨に対応可能
- **Schema**: `type: array, items: { type: string }`

**6. content-type（コンテンツの種類）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/content-type`
- **type**: `ActivityExtension`
- **prefLabel**:
  - ja: コンテンツの種類
  - en: content type
- **definition**:
  - ja: 参照されるコンテンツの種類（ヒント、解答、解説など）を示す
  - en: Indicates the type of referenced content (hint, answer, explanation, etc.)
- **Scope Note**: このプロファイルでは hint, result, explanation の3値をサポート
- **Schema**: `type: string, enum: ["hint", "result", "explanation"]`

**7. question-order（問題の出題順序）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/question-order`
- **type**: `ActivityExtension`
- **prefLabel**:
  - ja: 問題の出題順序
  - en: question order
- **definition**:
  - ja: テスト内での問題の出題順序を示す
  - en: Indicates the order of a question within a test
- **Scope Note**: 整数値で出題順序を管理
- **Schema**: `type: integer`

**8. difficulty（難易度）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/difficulty`
- **type**: `ContextExtension`
- **prefLabel**:
  - ja: 難易度
  - en: difficulty
- **definition**:
  - ja: 学習コンテンツまたは問題の難易度を示す
  - en: Indicates the difficulty level of learning content or a question
- **Scope Note**: Domain Profile で具体的な難易度値（例：1-5スケール）を定義
- **Schema**: `type: string`

**9. assessment-type（評価のタイプ）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/assessment-type`
- **type**: `ContextExtension`
- **prefLabel**:
  - ja: 評価のタイプ
  - en: assessment type
- **definition**:
  - ja: 評価の種類（診断的、形成的、総括的）を示す
  - en: Indicates the type of assessment (diagnostic, formative, summative)
- **Scope Note**: このプロファイルでは diagnostic, formative, summative の3値をサポート
- **Schema**: `type: string, enum: ["diagnostic", "formative", "summative"]`

**10. scrapbook-item-type（スクラップブック項目タイプ）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/scrapbook-item-type`
- **type**: `ActivityExtension`
- **prefLabel**:
  - ja: スクラップブック項目タイプ
  - en: scrapbook item type
- **definition**:
  - ja: グループ学習支援ツール内でスクラップボードに保存されたアイテムのタイプを示す
  - en: Indicates the type of item stored in a scrapboard in group learning support tools
- **Scope Note**: Domain Profile で具体的なアイテムタイプ（例：テキスト、画像、URL など）を定義
- **Schema**: `type: string`

**11. due-date（期限）**

- **IRI**: `https://w3id.org/japan-xapi/extensions/due-date`
- **type**: `ContextExtension`
- **prefLabel**:
  - ja: 期限
  - en: due date
- **definition**:
  - ja: LMS の課題提出等における期限日時を示す
  - en: Indicates the due date and time for task submission in LMS and similar systems
- **Scope Note**: ISO 8601 形式の日時で管理
- **Schema**: `type: string, format: "date-time"`

**注意**：
- メタデータの具体的な値のフォーマット規定（例：学年の表記方法、難易度の数値スケール）については、Core Profile では詳細に規定しない
- 各 Domain Profile が用途に応じて具体的な値の形式と許容値を定めるものとする

---

## 6. JSON-LD ファイルの構成

### 6.1 Core Profile の JSON-LD 構造

#### ファイル: core/v1.0.0/profile.jsonld

```json
{
  "@context": "https://w3id.org/xapi/profiles/context",
  "id": "https://w3id.org/japan-xapi/profiles/core",
  "type": "Profile",
  "conformsTo": "https://w3id.org/xapi/profiles#1.0",
  "prefLabel": {
    "ja": "Japan xAPI Core Profile",
    "en": "Japan xAPI Core Profile"
  },
  "definition": {
    "ja": "日本の初等中等教育を主対象とする学習ログ（xAPI Statement）の共通語彙（Concept）を定義するコア・プロファイル。ebook/CBT/LMS等のドメイン別プロファイルは、本プロファイルのConceptおよび既存標準（例：ADL）を参照し、Statement Templateを定義する。",
    "en": "A core profile that defines common vocabulary (Concepts) for learning logs (xAPI Statements) primarily targeting elementary and secondary education in Japan. Domain-specific profiles such as ebook/CBT/LMS reference the Concepts in this profile and existing standards (e.g., ADL) to define Statement Templates."
  },
  "versions": [
    {
      "id": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "generatedAtTime": "2026-04-01"
    }
  ],
  "publisher": {
    "type": "Organization",
    "name": "ICT CONNECT 21 xAPI SWG"
  },

  // ▼【重要】ここは「新しく作る言葉」だけを書く。ADLの言葉は書かない。
  "concepts": [
    {
      "id": "https://w3id.org/japan-xapi/verbs/highlighted",
      "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "type": "Verb",
      "prefLabel": {
        "ja": "ハイライトした",
        "en": "highlighted"
      },
      "definition": {
        "ja": "テキストや画像の一部を強調表示する行為。",
        "en": "The act of highlighting a part of text or image."
      }
    },
    {
      "id": "https://w3id.org/japan-xapi/extensions/subject",
      "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "type": "ActivityExtension",
      "prefLabel": { "ja": "教科", "en": "subject" },
      "definition": { 
        "ja": "学習コンテンツが対象とする教科を示す。",
        "en": "Indicates the school subject targeted by learning content."
      }
    },
    {
      "id": "https://w3id.org/japan-xapi/extensions/grade",
      "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "type": "ActivityExtension",
      "prefLabel": { "ja": "学年", "en": "grade" },
      "definition": { 
        "ja": "学習コンテンツが対象とする学年を示す。",
        "en": "Indicates the grade level targeted by learning content."
      }
    },
    {
      "id": "https://w3id.org/japan-xapi/extensions/difficulty",
      "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "type": "ContextExtension",
      "prefLabel": { "ja": "難易度", "en": "difficulty" },
      "definition": { 
        "ja": "学習コンテンツまたは問題の難易度を示す。",
        "en": "Indicates the difficulty level of learning content or a question."
      }
    },
    {
      "id": "https://w3id.org/japan-xapi/extensions/assessment-type",
      "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "type": "ContextExtension",
      "prefLabel": { "ja": "評価のタイプ", "en": "assessment type" },
      "definition": { 
        "ja": "評価の種類（診断的、形成的、総括的）を示す。",
        "en": "Indicates the type of assessment (diagnostic, formative, summative)."
      }
    },
    {
      "id": "https://w3id.org/japan-xapi/extensions/due-date",
      "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0",
      "type": "ContextExtension",
      "prefLabel": { "ja": "期限", "en": "due date" },
      "definition": { 
        "ja": "LMS の課題提出等における期限日時を示す。",
        "en": "Indicates the due date and time for task submission in LMS and similar systems."
      }
    }
  ],
  "templates": [],
  "patterns": []
}
```

---

## 7. 語彙の追加・変更フロー

### 7.1 新規語彙の追加

Domain Profile の実装時に新しい語彙が必要になった場合：

1. **既存標準で定義されているか確認**
   - ADL xAPI 標準、IEEE、IMS 等をチェック
   - YES → 既存標準を直接参照（Core に追加しない）

2. **複数 Domain で共通に使用されるか確認**
   - YES → Core Profile への追加を検討
   - NO → Domain 固有語彙として Domain Profile に定義

3. **Core Profile への追加提案**
   - SWG で議論・合意
   - 承認後、Core Profile に追加

### 7.2 語彙の廃止（Deprecation）

語彙を廃止する場合：

1. **deprecated フラグの追加**
   - JSON-LD に `"deprecated": true` を追加

2. **代替語彙の明示**
   - 新しい語彙への参照を記載

3. **バージョン履歴への記録**
   - changelog に廃止理由と代替語彙を記録

---

## 8. IRI 設計規則

### 8.1 IRI の基本構造

Core Profile で定義する語彙の IRI は以下の構造に従う：

**Verb**:
```
https://w3id.org/japan-xapi/verbs/[verb-id]
```

**ActivityType**:
```
https://w3id.org/japan-xapi/activity-types/[type-id]
```

**Extension**:
```
https://w3id.org/japan-xapi/extensions/[extension-id]
```

### 8.2 命名規則

- **小文字とハイフン**を使用（例：`curriculum-code`）
- **英語**で命名（日本語は prefLabel / definition に記載）
- **簡潔で明確**な名称を選択

### 8.3 バージョン管理

- IRI にはバージョン番号を含めない
- バージョンは `inScheme` で管理

**例：**
```json
{
  "id": "https://w3id.org/japan-xapi/verbs/highlighted",
  "inScheme": "https://w3id.org/japan-xapi/profiles/core/v1.0.0"
}
```

---

## 9. Domain Profile との連携

### 9.1 Core Profile の参照

Domain Profile から Core Profile を参照する方法：

**Markdown での記述：**
```markdown
1. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科 (Core Profile参照)
```

**JSON-LD での記述：**
- Domain Profile の template の rules で JSONPath を指定
- Core Profile の IRI を直接参照（再定義しない）

### 9.2 既存標準との併用

- Core Profile に定義されていない語彙は、既存標準（ADL 等）を直接参照
- Domain Profile で「ADL xAPI 標準語彙」と明記

---

## 10. 品質管理

### 10.1 一貫性チェック

Core Profile の語彙定義時に以下を確認：

- [ ] IRI が命名規則に従っているか
- [ ] prefLabel に日本語と英語の両方が含まれているか
- [ ] definition に明確な説明があるか
- [ ] 既存標準との重複がないか確認したか
- [ ] inScheme が正しいバージョンを指しているか

### 10.2 レビュープロセス

新規語彙の追加・変更時：

1. **提案**：Domain TF から Core に提案
2. **議論**：SWG 全体で議論
3. **合意**：SWG で合意形成
4. **追加**：Core Profile に追加
5. **公開**：更新されたプロファイルを公開

---

## 11. 附則

### 11.1 更新履歴

| 日付 | バージョン | 変更内容 |
|---|---|---|
| 2026-02-11 | v1.0.0 | 初版作成（全体アーキテクチャを統合） |

### 11.2 参考資料

- [xAPI Profile Specification](https://github.com/adlnet/xapi-profiles)
- [xAPI Vocabulary](https://registry.tincanapi.com/)
- Japan xAPI Domain Profile Guidelines
- 全体アーキテクチャ.md（統合済み）

---
