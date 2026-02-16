# Japan xAPI Profile プロジェクト管理ガイドライン

## 1. 概要

本ドキュメントは、Japan xAPI Profile プロジェクト全体の運用・管理に関するガイドラインである。以下の3つの要素を統合的に定義する：

1. **IRI 設計規則**：語彙やプロファイルの識別子（IRI）の設計方針
2. **バージョン管理規則**：セマンティックバージョニングに基づくバージョン管理方針
3. **ディレクトリ構造規則**：リポジトリの構造とファイル配置

本ガイドラインは、Core Profile および各 Domain Profile の開発・運用に共通して適用される。

---

## 2. IRI 設計規則

### 2.1 基本方針

Japan xAPI Profile における IRI（Internationalized Resource Identifier）は、以下の基本方針に従って設計する：

- **永続性**：一度公開した IRI は変更しない
- **一意性**：グローバルに一意な識別子を使用
- **可読性**：人間が理解しやすい命名を心がける
- **標準準拠**：既存の xAPI 標準や他のプロファイルとの整合性を保つ

### 2.2 Verb（動詞）の設計規則

#### 2.2.1 既存 Verb の優先利用（原則）

**原則**：既存 Verb がある場合は、新しい Verb は作らない

既存 Verb の参照順序：

1. **ADL xAPI 標準 Verb**
   - IRI 形式：`http://adlnet.gov/expapi/verbs/[verb-id]`
   - 例：`http://adlnet.gov/expapi/verbs/launched`
   - 既存で過去形ではない verb はそのまま運用する
   - ExactMatch を使って本プロファイルで再定義することはしない

2. **ADL Authored Profile 内の w3id ドメインの Verb**（推奨）
   - IRI 形式：`https://w3id.org/xapi/adl/verbs/[verb-id]`
   - 例：`https://w3id.org/xapi/adl/verbs/launched`

3. **Authorized されている IRI**
   - xAPI Registry で認証されている Verb

4. **報告書等に記載されている SIP や京大プロファイルの Verb**
   - 国内プロジェクトで既に定義されている Verb

#### 2.2.2 複数の既存 Verb がある場合（推奨）

意味（description）が同じ場合は、上記の順序（1→2→3→4）で選択する。

#### 2.2.3 独自 Verb の定義

**既存 Verb に該当するものがない場合のみ**、w3id ドメインで新規定義する：

- IRI 形式：`https://w3id.org/japan-xapi/verbs/[verb-id]`
- 例：`https://w3id.org/japan-xapi/verbs/highlighted`

**定義手順：**
1. 既存 Verb の調査（ADL Registry、既存プロファイル等）
2. Core Profile への提案
3. SWG での議論・合意
4. Core Profile への追加

### 2.3 ActivityType の設計規則

Verb と同様の方針を適用する：

#### 2.3.1 既存 ActivityType の優先利用

1. **ADL xAPI 標準 ActivityType**
   - IRI 形式：`http://adlnet.gov/expapi/activities/[type-id]`
   - 例：`http://adlnet.gov/expapi/activities/assessment`

2. **その他の標準 ActivityType**
   - TinCan API Registry 等

#### 2.3.2 独自 ActivityType の定義

既存に該当するものがない場合のみ、新規定義する：

- IRI 形式：`https://w3id.org/japan-xapi/activity-types/[type-id]`
- 例：`https://w3id.org/japan-xapi/activity-types/group-lst/tool`

### 2.4 Extension の設計規則

Extension は原則として独自定義する。一つの Extension は「ActivityExtension のみ」「ContextExtension のみ」「両方兼用」のいずれかに分類される。

#### 2.4.1 Extension IRI の形式

IRI 形式は Extension のタイプによらず統一される：

**Core Profile の Extension:**
- IRI 形式：`https://w3id.org/japan-xapi/extensions/[extension-id]`
- 例（ActivityExtension のみ）：`https://w3id.org/japan-xapi/extensions/purpose-of-question`
- 例（ContextExtension のみ）：`https://w3id.org/japan-xapi/extensions/assessment-type`
- 例（両方兼用）：`https://w3id.org/japan-xapi/extensions/subject`

**Domain 固有 Extension:**
- IRI 形式：`https://w3id.org/japan-xapi/extensions/[domain]/[extension-id]`
- 例：`https://w3id.org/japan-xapi/extensions/ebook/launch-reason`

#### 2.4.2 Extension のタイプ

各 Extension は以下のいずれかのタイプを持つ：

| タイプ | 説明 | 用途 |
|--------|------|------|
| **ActivityExtension のみ** | Object（コンテンツ、課題等）に付与される | 学習コンテンツ自体のメタデータ記録 |
| **ContextExtension のみ** | Context（学習行為の文脈）に付与される | 学習活動時の状況・環境を記録 |
| **両方兼用** | Object と Context の両方に付与可能 | 教科・学年など、複数の文脈で使用される | 

**実装例（Core Profile の 11 Extension）：**

- **ActivityExtension のみ**：
  - `purpose-of-question`（問題の趣旨）
  - `content-type`（コンテンツの種類：hint, result, explanation）
  - `question-order`（問題の出題順序）
  - `scrapbook-item-type`（スクラップブック項目タイプ）

- **ContextExtension のみ**：
  - `difficulty`（難易度）
  - `assessment-type`（評価のタイプ：diagnostic, formative, summative）
  - `due-date`（期限日）

- **両方兼用**：
  - `grade`（学年）
  - `subject`（教科）
  - `course-of-study-code`（学習指導要領コード）
  - `unit`（単元名）

#### 2.4.3 Extension の定義場所

- **Core Profile**：複数 Domain で共通に使用される Extension（上記 11 Extension）
- **Domain Profile**：特定 Domain のみで使用される Extension

### 2.5 Statement に書く Concept IRI（推奨：unversioned）

実際の Statement に記述する Concept IRI は、**バージョンを含まない形式**（unversioned）を使用する：

```
https://w3id.org/japan-xapi/verbs/[verb-id]
https://w3id.org/japan-xapi/activity-types/[type-id]
https://w3id.org/japan-xapi/extensions/[extension-id]
```

**理由**：
- バージョンアップ時に既存の Statement が無効にならない
- IRI の永続性を保つ
- バージョン管理は Profile 側で行う

### 2.6 Profile 実体の置き場（推奨：versioned）

Profile の JSON-LD ファイルは、**バージョンを含む IRI**（versioned）を使用する：

```
https://w3id.org/japan-xapi/profiles/core/v1.0.0/profile.jsonld
https://w3id.org/japan-xapi/profiles/ebook/v1.0.0/profile.jsonld
https://w3id.org/japan-xapi/profiles/lms/v1.0.0/profile.jsonld
https://w3id.org/japan-xapi/profiles/cbt/v1.0.0/profile.jsonld
https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0/profile.jsonld
```

**理由**：
- Profile のバージョン管理を明確にする
- 異なるバージョンの Profile を並行して参照可能にする

### 2.7 IRI 命名規則

#### 2.7.1 基本ルール

- **小文字とハイフン**を使用（例：`curriculum-code`）
- **英語**で命名（日本語は prefLabel / definition に記載）
- **簡潔で明確**な名称を選択
- **複数形より単数形**を優先（例：`verb` not `verbs` in concept ID）

#### 2.7.2 禁止事項

- アンダースコア（`_`）の使用
- 大文字の使用
- 日本語の使用（IRI 内）
- バージョン番号の直接埋め込み（Concept IRI）

---

## 3. バージョン管理規則

### 3.1 基本方針

Japan xAPI Profile は、**セマンティックバージョニング**（Semantic Versioning）の考え方に準拠する。

**バージョン形式**：`MAJOR.MINOR.PATCH`（例：`v1.0.0`）

- **個々のプロファイルが独自のバージョンを持つ**
- Core Profile と各 Domain Profile は独立してバージョン管理される
- xAPI Profile 仕様書で推奨されている方式に従う

### 3.2 初期バージョン

本プロジェクトの初期バージョンは以下の通り：

- **プロファイルバージョン**：`v1.0.0`
- **ドキュメントバージョン**：`2026年度版`（日付ベース）

### 3.3 Major バージョン（v1.0.0 → v2.0.0）

**破壊的変更（Breaking Changes）**：過去のデータとの互換性がなくなる場合

#### 3.3.1 Major 更新の条件

以下のいずれかに該当する場合、Major バージョンを上げる：

**1. ルールの厳格化**
- プロファイル検証において、これまで許可されていたデータがエラーになるような変更
- 例：推奨（recommended）から必須（included）への変更
- 例：optional から included への変更

**2. 語彙の削除**
- 使用されていた Verb や Extension をプロファイルから削除する場合
- 注意：deprecated フラグを設定する場合も、削除と同等に扱う

**3. 構造の変更**
- Statement Template の構造要件を変更し、既存のデータが適合しなくなる場合
- 例：必須プロパティの追加
- 例：JSONPath の変更

**4. Core プロファイルの変更による影響**
- 共通語彙（Core）で破壊的変更があり、それに依存する各プロファイル（LMS, CBT 等）も修正を余儀なくされる場合

#### 3.3.2 Major 更新の手順

1. **影響範囲の分析**
   - 既存の Statement への影響を評価
   - 依存する Profile への影響を確認

2. **移行ガイドの作成**
   - 変更内容の詳細説明
   - データ移行方法の提示
   - 互換性情報の提供

3. **SWG での承認**
   - 破壊的変更の必要性を議論
   - 全体合意の形成

4. **公開とアナウンス**
   - 新バージョンの公開
   - 利用者への通知

### 3.4 Minor バージョン（v1.0.0 → v1.1.0）

**機能追加（New Features）**：後方互換性があり、以前のデータもそのまま有効（Valid）である場合

#### 3.4.1 Minor 更新の条件

以下のいずれかに該当する場合、Minor バージョンを上げる：

**1. 概念（Concept）の追加**
- 新しい Verb、Activity Type、Extension 定義を追加する場合
- 例：LMS プロファイルに新たな学習操作を表す Verb を追加

**2. Template / Pattern の追加**
- 新たなユースケースに対応するための定義を追加する場合
- 既存の Template は変更しない

**3. ルールの緩和**
- 必須（included）だった項目を推奨（recommended）に変更するなど、制約を緩める場合
- recommended から optional への変更

**4. Core プロファイルの拡張への追従**
- Core に新しい語彙が追加され、それを各プロファイルで採用する場合

#### 3.4.2 Minor 更新の手順

1. **機能仕様の作成**
   - 追加する機能の詳細を定義

2. **TF での議論**
   - 該当する Domain TF で議論
   - 必要に応じて SWG 全体で共有

3. **実装とレビュー**
   - Profile への追加実装
   - レビューと承認

4. **公開**
   - 新バージョンの公開
   - 変更履歴の記録

### 3.5 Patch バージョン（v1.0.0 → v1.0.1）

**バグ修正・軽微な変更（Fixes）**：機能的な変更がなく、各 TF（タスクフォース）で判断可能なレベル

#### 3.5.1 Patch 更新の条件

以下のいずれかに該当する場合、Patch バージョンを上げる：

**1. ドキュメントの修正**
- 誤字脱字の修正
- 説明文（description）の明確化
- 日本語訳の改善
- サンプルコードの修正

**2. メタデータの更新**
- 作成者情報の更新
- 更新日の変更
- バージョン番号のみの変更

**3. 非規範的な内容の追記**
- 実装者の理解を助けるための例示（Example）の追加
- 補足説明の追加
- 注釈の追加

#### 3.5.2 Patch 更新の手順

1. **修正内容の確認**
   - 機能的な変更がないことを確認

2. **TF での承認**
   - 該当 TF 内で承認（SWG 全体の承認は不要）

3. **即時適用**
   - 修正を適用し、バージョン番号を更新

### 3.6 バージョン履歴の記録

すべてのバージョン更新は、以下の情報を記録する：

#### 3.6.1 Profile JSON-LD の versions セクション

```json
"versions": [
  {
    "id": "https://w3id.org/japan-xapi/profiles/[domain]/v1.1.0",
    "generatedAtTime": "2026-06-01",
    "wasRevisionOf": "https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0"
  },
  {
    "id": "https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0",
    "generatedAtTime": "2026-04-01"
  }
]
```

#### 3.6.2 CHANGELOG.md

各プロファイルディレクトリに CHANGELOG.md を配置する：

```markdown
# Changelog

## [1.1.0] - 2026-06-01

### Added
- 新しい Verb `xxx` を追加
- 新しい Template `yyy` を追加

### Changed
- Extension `zzz` の description を明確化

## [1.0.0] - 2026-04-01

### Added
- 初版リリース
```

### 3.7 互換性の管理

#### 3.7.1 後方互換性

- **Minor / Patch 更新**：既存の Statement は有効なまま
- **Major 更新**：既存の Statement が無効になる可能性あり

#### 3.7.2 前方互換性

- 新しいバージョンで追加された語彙を古いバージョンのバリデータが拒否する可能性
- Catalog で依存関係を明示

---

## 4. ディレクトリ構造規則

### 4.1 基本構造

Japan xAPI Profile のリポジトリは、以下の構造に従う：

```
japan-xapi-profiles/ (ルート)
├── core/                               # Core プロファイル（共通の用語定義）
│   ├── v1.0.0/
│   │   ├── core_profile.md             # Markdown ドキュメント
│   │   └── profile.jsonld              # JSON-LD プロファイル定義
│   ├── v1.0.1/
│   │   ├── core_profile.md
│   │   └── profile.jsonld
│   ├── CHANGELOG.md                    # バージョン履歴
│   └── README.md                       # プロファイル概要
│
├── ebook/                              # eBook プロファイル（電子書籍）
│   ├── v1.0.0/
│   │   ├── ebook_profile.md            # Markdown ドキュメント
│   │   └── profile.jsonld              # JSON-LD プロファイル定義
│   ├── v1.1.0/
│   │   ├── ebook_profile.md
│   │   └── profile.jsonld
│   ├── CHANGELOG.md
│   └── README.md
│
├── lms/                                # LMS プロファイル（学習管理システム）
│   ├── v1.0.0/
│   │   ├── lms_profile.md
│   │   └── profile.jsonld
│   ├── CHANGELOG.md
│   └── README.md
│
├── cbt/                                # CBT プロファイル（デジタルドリル）
│   ├── v1.0.0/
│   │   ├── cbt_profile.md
│   │   └── profile.jsonld
│   ├── CHANGELOG.md
│   └── README.md
│
├── group-lst/                          # Group Learning Support Tool プロファイル
│   ├── v1.0.0/
│   │   ├── group-lst_profile.md
│   │   └── profile.jsonld
│   ├── CHANGELOG.md
│   └── README.md
│
├── catalog/                            # 互換性・依存関係情報
│   └── v1/
│       └── catalog.json                # Catalog 定義
│
├── document/                           # プロジェクト全体のドキュメント
│   └── document_rules/
│       ├── Domain_Profile_Guidelines.md
│       ├── Core_Profile_Guidelines.md
│       ├── Project_Management_Guidelines.md
│       └── draft共通テンプレート_new.md
│
└── README.md                           # プロジェクト全体の README
```

### 4.2 各ディレクトリの役割

#### 4.2.1 Core プロファイル（core/）

**役割**：日本独自の Verb、ActivityType、Extension を定義

**特徴**：
- 各 Domain プロファイルで使用する共通の用語を定義
- 各 Domain プロファイルに必須というわけではない
- Concept の定義がメイン（Template は原則置かない）

**必須ファイル**：
- `v[x.y.z]/core_profile.md`：Markdown ドキュメント
- `v[x.y.z]/profile.jsonld`：JSON-LD 定義
- `README.md`：プロファイル概要
- `CHANGELOG.md`：変更履歴

#### 4.2.2 Domain プロファイル（ebook/, lms/, cbt/, group-lst/）

**役割**：Statement Template と Pattern を定義

**特徴**：
- ドメイン固有のユースケースと操作を定義
- Core または既存標準の語彙を参照（再定義しない）
- Template と Pattern の定義がメイン（Concept は原則置かない）

**必須ファイル**：
- `v[x.y.z]/[domain]_profile.md`：Markdown ドキュメント
- `v[x.y.z]/profile.jsonld`：JSON-LD 定義
- `README.md`：プロファイル概要
- `CHANGELOG.md`：変更履歴

#### 4.2.3 Catalog（catalog/）

**役割**：プロファイル間の依存関係と互換性を管理

**内容**：
- Profile 間の依存（例：ebook v1.0.0 は core v1.x を前提）
- IRI 一覧
- 命名規則
- 廃止（deprecate）情報

**ファイル**：
- `v1/catalog.json`：Catalog 定義

**注意**：
- 仕様上必須ではないが、複数 Profile 運用で極めて有効

#### 4.2.4 Document（document/）

**役割**：プロジェクト全体のガイドラインとテンプレート

**内容**：
- Domain Profile Guidelines
- Core Profile Guidelines
- Project Management Guidelines
- 共通テンプレート

### 4.3 バージョンディレクトリの管理

#### 4.3.1 基本ルール

- **プロファイルごとにディレクトリを分け**、その下にバージョンを切る
- **バージョンディレクトリは削除しない**（過去バージョンも保持）
- **最新バージョンは明示的に示す**（README.md に記載）

#### 4.3.2 ディレクトリ命名規則

- バージョンディレクトリ：`v[MAJOR].[MINOR].[PATCH]`（例：`v1.0.0`）
- ドメイン名：小文字とハイフン（例：`group-lst`）

#### 4.3.3 ファイル命名規則

**Markdown ドキュメント**：
- `[domain]_profile.md`（例：`ebook_profile.md`）
- `core_profile.md`（Core の場合）

**JSON-LD 定義**：
- `profile.jsonld`（統一）

**その他**：
- `README.md`：プロファイル概要
- `CHANGELOG.md`：変更履歴

### 4.4 README.md の記載内容

各プロファイルディレクトリの README.md には以下を記載する：

```markdown
# [Profile Name] Profile

## 概要
[プロファイルの簡単な説明]

## 最新バージョン
v1.0.0（2026-04-01）

## バージョン一覧
- [v1.0.0](v1.0.0/) - 初版リリース
- [v1.0.1](v1.0.1/) - [変更内容]

## ドキュメント
- [Markdown ドキュメント](v1.0.0/[domain]_profile.md)
- [JSON-LD 定義](v1.0.0/profile.jsonld)

## 依存関係
- Core Profile v1.x

## 関連リンク
- [Domain Profile Guidelines](../document/document_rules/Domain_Profile_Guidelines.md)
```

---

## 5. Catalog による依存関係管理

### 5.1 Catalog の役割

Catalog は、複数のプロファイル間の関係を管理するためのメタデータファイルである。

### 5.2 Catalog の構造例

```json
{
  "@context": "https://w3id.org/xapi/profiles/context",
  "id": "https://w3id.org/japan-xapi/catalog/v1",
  "type": "ConceptScheme",
  "title": {
    "ja": "Japan xAPI Profile Catalog",
    "en": "Japan xAPI Profile Catalog"
  },
  "profiles": [
    {
      "id": "https://w3id.org/japan-xapi/profiles/core",
      "currentVersion": "v1.0.0",
      "versions": ["v1.0.0", "v1.0.1"]
    },
    {
      "id": "https://w3id.org/japan-xapi/profiles/ebook",
      "currentVersion": "v1.0.0",
      "versions": ["v1.0.0", "v1.1.0"],
      "dependencies": [
        {
          "profile": "https://w3id.org/japan-xapi/profiles/core",
          "versionRange": "v1.x"
        }
      ]
    },
    {
      "id": "https://w3id.org/japan-xapi/profiles/lms",
      "currentVersion": "v1.0.0",
      "versions": ["v1.0.0"],
      "dependencies": [
        {
          "profile": "https://w3id.org/japan-xapi/profiles/core",
          "versionRange": "v1.x"
        }
      ]
    }
  ]
}
```

### 5.3 Catalog の利用

- **依存関係の確認**：実装時に必要な Profile のバージョンを確認
- **互換性の検証**：Profile の組み合わせの互換性を検証
- **廃止情報の管理**：deprecated な語彙や Profile の情報を管理

---

## 6. 運用フロー

### 6.1 新規 Profile 作成フロー

1. **企画・提案**
   - TF での議論
   - ユースケースの整理

2. **ドキュメント作成**
   - Markdown ドキュメントの作成（テンプレート使用）
   - Guidelines に従った記述

3. **JSON-LD 作成**
   - Profile の JSON-LD 定義
   - 語彙の定義（Core または既存標準参照）

4. **レビューと承認**
   - TF 内レビュー
   - SWG 全体レビュー

5. **公開**
   - リポジトリへの追加
   - Catalog への登録
   - README.md の更新

### 6.2 既存 Profile 更新フロー

1. **更新の検討**
   - 更新の必要性を確認
   - Major / Minor / Patch の判定

2. **影響範囲の分析**
   - 既存データへの影響
   - 依存 Profile への影響

3. **ドキュメント更新**
   - Markdown ドキュメントの更新
   - JSON-LD の更新
   - CHANGELOG.md の更新

4. **バージョン番号の更新**
   - セマンティックバージョニングに従う
   - メタ情報の更新

5. **レビューと承認**
   - TF または SWG でのレビュー
   - Major の場合は必ず SWG 全体で承認

6. **公開**
   - 新バージョンディレクトリの作成
   - Catalog の更新
   - README.md の更新

### 6.3 語彙追加フロー（Core Profile）

1. **必要性の確認**
   - 既存標準の調査
   - 複数 Domain での共通性の確認

2. **Core Profile への提案**
   - TF から Core TF への提案
   - 提案書の作成

3. **SWG での議論**
   - 全体での議論
   - 合意形成

4. **Core Profile への追加**
   - JSON-LD への追加
   - ドキュメントへの追加

5. **Domain Profile での採用**
   - 各 Domain Profile での利用
   - Template での参照

---

## 7. 品質管理

### 7.1 チェックリスト

#### 7.1.1 IRI 設計チェック

- [ ] 既存標準の調査を実施したか
- [ ] IRI が命名規則に従っているか
- [ ] Concept IRI はバージョンを含まないか
- [ ] Profile IRI はバージョンを含むか
- [ ] 小文字とハイフンのみを使用しているか

#### 7.1.2 バージョン管理チェック

- [ ] セマンティックバージョニングに従っているか
- [ ] Major / Minor / Patch の判定は適切か
- [ ] CHANGELOG.md を更新したか
- [ ] versions セクションを更新したか
- [ ] 依存 Profile への影響を確認したか

#### 7.1.3 ディレクトリ構造チェック

- [ ] バージョンディレクトリを正しく作成したか
- [ ] 必須ファイルがすべて存在するか
- [ ] ファイル命名規則に従っているか
- [ ] README.md を更新したか
- [ ] Catalog を更新したか

### 7.2 レビュープロセス

#### 7.2.1 TF レビュー

- Patch 更新：TF 内で完結
- Minor 更新：TF 内で承認後、SWG に報告
- Major 更新：TF で検討後、SWG で議論

#### 7.2.2 SWG レビュー

- Core Profile の変更：必須
- Major 更新：必須
- Minor 更新：報告（承認は不要）
- Patch 更新：報告不要

---

## 8. 附則

### 8.1 更新履歴

| 日付 | バージョン | 変更内容 |
|---|---|---|
| 2026-02-11 | v1.0.0 | 初版作成（IRI設計、バージョン管理、ディレクトリ構造を統合） |

### 8.2 参考資料

- [xAPI Profile Specification](https://github.com/adlnet/xapi-profiles)
- [Semantic Versioning](https://semver.org/)
- [W3C Permanent Identifier (w3id.org)](https://w3id.org/)
- Domain Profile Guidelines
- Core Profile Guidelines

### 8.3 統合元ドキュメント

本ガイドラインは、以下の3つのドキュメントを統合したものである：

1. **IRI設計.md**：IRI 設計規則（第2章に統合）
2. **バージョン管理の考え方.md**：バージョン管理規則（第3章に統合）
3. **全体のディレクトリ構造.md**：ディレクトリ構造規則（第4章に統合）

---
