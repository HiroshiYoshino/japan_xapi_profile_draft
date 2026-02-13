# Japan xAPI Domain Profile テンプレート

> **注意**: このテンプレートは、新しいDomain Profileを作成する際の雛形です。  
> `[ドメイン名]`、`[domain]`、`[Domain]` 等のプレースホルダーを実際の値に置き換えて使用してください。

---

# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである[ドメイン名]TFにおける学習ログを対象として取りまとめた **Japan xAPI [Domain] Profile** 標準仕様である。  
　本仕様は、[ドメイン名]分野に記載されている特性を踏まえ、[対象システム・環境]上で発生する[主な活動内容]に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、[ドメイン名]における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、[Domain]プロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateで使用される語彙（Verb、ActivityType、Extension等）は以下のいずれかに整理される。(1) SWG独自に定義した語彙を使用する場合、Core Profile内のConceptsに定義されている。(2) ADLや他の標準で定義済みの語彙を使用する場合、それらを直接参照し、Domain Profileで再定義しない。Domain Profile（本プロファイルはDomain Profileの1つ）として[Domain] Profileは Statement Templateおよび Rules の定義に集中し、語彙定義はCore Profileに委譲する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、[ドメイン名]における学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

- idに期待されるURI
  - 省略理由：idはStatementTemplateをグローバルに一意に識別するためのURI を指定する項目であり、プロファイルの公開形態、管理主体、バージョニング方針が確定した段階で設計されるべきものである。本ドキュメントは標準仕様（案）としての整理および合意形成を目的としているため、現時点では具体的なURIの定義は行わない。
- typeに期待される固定値StatementTemplate
  - 省略理由：typeに指定される固定値StatementTemplateは、JSON-LD形式における機械可読性を担保するための項目である。本ドキュメントでは、読み手による理解を前提とした仕様書として、StatementTemplateの構造および位置づけを章構成および見出しによって明示しているため、当該項目は省略する。
- inSchemaに期待されるURI
  - 省略理由：inSchemaは、当該StatementTemplateが属するプロファイルおよびバージョンをURIにより示すための項目である。本ドキュメントでは、プロファイルの名称およびバージョン管理を文書構成および章立てにより管理していることから、inSchemaによる明示的な指定は行わない
- prefLabel
  - 省略理由：prefLabelはStatementTemplateに対する人可読な名称を付与するための項目である。本ドキュメントでは、各ユースケースを章・節の見出し（項目名）として明示しており、これをもって当該StatementTemplateを識別可能とするため、prefLabel の記載は省略する。

　なお、これらの項目については、将来的にプロファイルの登録や機械可読な形式での提供が必要となる場合に、改めて検討することとする。

## 1.4　定義範囲

　本ドキュメントは、Japan xAPI [Domain] Profileを構成する要素のうち、メタ情報、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、[ドメイン名]における学習行動が非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本ドキュメントの構成について

　本紙は、xAPIプロファイル仕様に基づき、[ドメイン名]学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                     | 説明                                   | 値                                                           |
| :----------------------- | :------------------------------------- | :----------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/[domain]`              |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                    |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                         |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI [Domain] Profile                                  |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                       |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                      |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                   |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                       |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育における[ドメイン名]学習ログ標準プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                   |

## 2.3　共通記述規則

　本プロファイルで定義するすべてのStatementTemplateに対して、以下のRulesを適用する。

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

# 3. [ドメイン名]に関するユースケース

> **記述ガイド**: 本章では、対象ドメインにおける学習活動の特性を記述し、主な学習活動の例を列挙する。

[ドメイン名]における主なユースケースは、[主要な学習活動の説明]である。

主な学習活動の例：

- **[活動1]**: [説明]
- **[活動2]**: [説明]
- **[活動3]**: [説明]

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、[Domain]プロファイルにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

## 4.2　前提条件

- 基本仕様
  - 冒頭にdefinitionの位置づけとして、Templateの目的やどのような操作を記録するためのものかを定義する。
  - 識別情報
    - Templateを管理上特定するための情報として3要素（id,inScheme,prefLabel）を含む。
  - 判定条件
    - 受信したStatementがどのTemplateに該当するかを自動判別するための固定値（Verb,objectActivityType）を示す。
- 記述規則（Rules）
  - Statement内の各プロパティに対する制約を示す。以下の要素を含む。
    - データの所在（location）: JSONPath方式で記述されるデータの位置。
    - presence：included（必須）、recommended（推奨）、optional（任意）のいずれか1つ。
    - ScopeNoteの内容に基づいた値の定義や運用上の注意点。
- Markdownテーブルの構成
  - 各Templateの末尾には、システム設計・実装時に参照しやすいよう、記述規則（Rules）を一覧化したテーブルを配置する。

## 4.3　StatementTemplate一覧

### 4.3.1　[操作名1]

#### 4.3.1.1　基本仕様

- [操作内容の説明]を記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                             |
| :------- | :--------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/[domain]/[template-id]   |
| inScheme | https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0            |
| prefLabel | [操作名]                                                      |

- 判定条件

| 項目              | 値                                                                 |
| :---------------- | :----------------------------------------------------------------- |
| verb              | [Verb IRI（例：http://adlnet.gov/expapi/verbs/launched）]           |
| objectActivityType | [ActivityType IRI（例：https://w3id.org/japan-xapi/activity-types/[domain]/xxx）] |

> **記述ガイド**: 
> - Verbは、Core Profileで定義されたもの、またはADL等の既存標準を参照する
> - objectActivityTypeも同様に、Core Profileまたは既存標準を参照する

#### 4.3.1.2　記述規則（Rules）

> **記述ガイド**: 
> - 各Ruleは番号付きリストで記述する
> - JSONPathは `$.` で始まり、Extensions は IRI をクォーテーションで囲む
> - Presenceは included / recommended / optional のいずれか
> - Core Profile参照の場合は「(Core Profile参照)」と明記
> - Domain固有の場合は「([Domain名] Domain固有)」と明記
> - 補足がある場合は [!NOTE] ブロックで記述する

1. $.object.id
   1. included
   2. [説明：例：開始された[ドメイン]を識別するIRIまたはURLを設定]
2. $.object.definition.name['ja-JP']
   1. recommended
   2. [説明：例：オブジェクトの日本語表示名]
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/[extension-id]']
   1. recommended
   2. [説明] (Activity拡張, Core Profile参照 / [Domain名] Domain固有)
      - [値の範囲や例を記述]
4. $.context.extensions['https://w3id.org/japan-xapi/extensions/[extension-id]']
   1. recommended
   2. [説明] (Context拡張, Core Profile参照 / [Domain名] Domain固有)
      - [値の範囲や例を記述]

#### 4.3.1.3　Markdownテーブル

| 項目     | 説明 | Location (JSONPath)                                      | Presence    |
| :------- | :--- | :------------------------------------------------------- | :---------- |
| **[項目名]** | [詳細説明]                                              | `$.object.id`                                                | included    |
| **[項目名]** | [詳細説明]                                              | `$.object.definition.name['ja-JP']`                          | recommended |
| **[項目名]（Activity拡張）** | [詳細説明]<br>Core Profile参照 / Domain固有 | `$.object.definition.extensions['https://w3id.org/...']`     | recommended |
| **[項目名]（Context拡張）** | [詳細説明]<br>Core Profile参照 / Domain固有  | `$.context.extensions['https://w3id.org/...']`               | recommended |

> [!NOTE]
> - [補足や条件がある場合に記載]

---

### 4.3.2　[操作名2]

#### 4.3.2.1　基本仕様

- [操作内容の説明]を記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                              |
| :------- | :--------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/[domain]/[template-id-2] |
| inScheme | https://w3id.org/japan-xapi/profiles/[domain]/v1.0.0            |
| prefLabel | [操作名2]                                                     |

- 判定条件

| 項目              | 値               |
| :---------------- | :--------------- |
| verb              | [Verb IRI]       |
| objectActivityType | [ActivityType IRI] |

#### 4.3.2.2　記述規則（Rules）

1. $.object.id
   1. included
   2. [説明]
2. [その他のRules...]

#### 4.3.2.3　Markdownテーブル

| 項目     | 説明 | Location (JSONPath) | Presence |
| :------- | :--- | :------------------ | :------- |
| [項目名] | [説明] | [JSONPath]          | [Presence] |

---

## 附則：テンプレート使用ガイド

### 1. プレースホルダーの置換

以下のプレースホルダーを実際の値に置き換えてください：

- `[ドメイン名]`: CBT、LMS、eBook、Group Learning Support Tool 等
- `[Domain]`: CBT、LMS、eBook、Group-LST 等（表示名）
- `[domain]`: cbt、lms、ebook、group-lst 等（IRI用小文字）
- `[操作名]`: 具体的な操作の名称（例：プラットフォームの起動、課題の作成）
- `[template-id]`: テンプレートのID（例：platform-launched、assignment-created）
- `[Verb IRI]`: 動詞のIRI（Core ProfileまたはADL等の既存標準を参照）
- `[ActivityType IRI]`: アクティビティタイプのIRI
- `[extension-id]`: 拡張フィールドのID

### 2. ドキュメント作成の流れ

1. **メタ情報の記入**
   - プロファイル名、作成日、説明を記入
   - 作成日は2026-04-01に統一（または最新版の日付）

2. **ユースケースの定義**
   - 対象ドメインの特性と主な学習活動を記述

3. **StatementTemplateの作成**
   - 各操作に対して、基本仕様・記述規則・Markdownテーブルを記述
   - Domain Profile Guidelinesに従って記述

4. **Core Profile参照の確認**
   - 使用する語彙がCore Profileに定義されているか確認
   - 未定義の場合は新規語彙検討フローに従う

5. **整合性チェック**
   - Domain Profile Guidelinesのチェックリストを使用

### 3. 各セクションの記述ポイント

#### 基本仕様
- Templateの目的を1文で簡潔に説明
- 識別情報（id, inScheme, prefLabel）を正確に記入
- 判定条件（Verb, objectActivityType）を明記

#### 記述規則（Rules）
- JSONPathを正確に記述（Extensionsはクォーテーション必須）
- Presenceを適切に選択（included / recommended / optional）
- Core Profile参照か Domain固有かを明記
- 値の範囲や例があれば記述

#### Markdownテーブル
- Rulesの内容を一覧表にまとめる
- 複数行の説明は `<br>` で改行
- 表のアライメントを統一（左揃え `:---`）

### 4. 参考資料

- [Domain Profile Guidelines](./Domain_Profile_Guidelines.md)
- [Core Profile Guidelines](./Core_Profile_Guidelines.md)
- 既存のDomain Profile
  - [CBT Profile](../../cbt/v1.0.0/cbt_profile.md)
  - [LMS Profile](../../lms/v1.0.0/lms_profile.md)
  - [eBook Profile](../../ebook/v1.0.0/ebook_profile.md)
  - [Group-LST Profile](../../group-lst/v1.0.0/group-lst_profile.md)

---
