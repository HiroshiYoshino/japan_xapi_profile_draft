# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるJapan xAPI Core Profile TFにおける学習ログを対象として取りまとめた **Japan xAPI Core Profile** 標準仕様である。  
　本仕様は、全体アーキテクチャに記載されている **Core Concept Profile（語彙の核）** としての役割を踏まえ、各ドメイン（CBT, eBook, LMS等）上で発生する学習ログ記録において共通利用される語彙（Concepts）を体系的に定義するための仕様である。

## 1.2　目的

　本ドキュメントは、日本の初等中等教育における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、共通語彙（Verb, ActivityType, Extension）の定義および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各Concept定義は、xAPIプロファイル仕様で定義されているConceptsの構造および考え方に準拠して記載する。  
　本プロファイルは **Concept（概念定義）** を主とし、Statement Template は原則として定義しない（Templateは各ドメインプロファイルで定義する）。  
　本ドキュメントは、学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

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

　本ドキュメントは、Japan xAPI Core Profileを構成する要素のうち、メタ情報、およびドメイン横断的に利用されるConcepts（Verbs, Extensions等）を定義することを目的とする。

## 1.5　本ドキュメントの構成について

　本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- Concepts：本プロファイルで定義する共通語彙（Verb, Extension等）

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                                        | 説明                                   | 値                                                                 |
| :------------------------------------------ | :------------------------------------- | :----------------------------------------------------------------- |
| **id**                                      | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/core`                        |
| **type**                                    | オブジェクトタイプ                     | `Profile`                                                          |
| **conformsTo**                              | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                               |
| プロファイル名 prefLabel                    | プロファイルを識別する名称             | Japan xAPI Core Profile                                            |
| バージョン version                          | プロファイルの改訂番号やリリース状態   | v1.0.0                                                             |
| 作成者/管理者 author                        | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                            |
| 作成日/更新日 versions                      | 文書化日または改訂日                   | 2026-04-01                                                         |
| 言語 languages                              | メタ情報およびプロファイルの記載言語   | 日本語                                                             |
| 目的/説明 $.object.definition.name['ja-JP'] | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育を主対象とする学習ログの共通語彙定義プロファイル |
| ドキュメントバージョン                      | 文書版数                               | 2026年度版                                                         |

# 3.　Concepts (概念定義)

## 3.1　本章の位置づけ

　本章では、Japan xAPI Core Profileにおける共通語彙（Verbs, Extensions）を定義する。

## 3.2　Verbs (動詞)

### 3.2.1　本プロファイルで定義する Verb

#### highlighted

- **IRI**: `https://w3id.org/xapi/adb/verbs/highlighted`
- **Display**: `highlighted` (en), `ハイライトした` (ja)
- **Definition**: テキストや画像の一部を強調表示する行為。
- **Scope Note**: 重要な箇所へのマーキング等に使用する。

#### attempted

- **IRI**: `http://adlnet.gov/expapi/verbs/attempted`
- **Display**: `attempted` (en), `開始した` (ja)
- **Definition**: アセスメントの提供開始を示す。
- **Scope Note**: 受験開始操作やページ表示時に使用する。

#### answered

- **IRI**: `http://adlnet.gov/expapi/verbs/answered`
- **Display**: `answered` (en), `回答した` (ja)
- **Definition**: 学習者がAssessment内の設問に応答したことを示す。
- **Scope Note**: 個別の質問に対する回答時に使用する。

#### completed

- **IRI**: `http://adlnet.gov/expapi/verbs/completed`
- **Display**: `completed` (en), `終了した` (ja)
- **Definition**: Assessmentが終了したことを示す。
- **Scope Note**: 学習者が明示的に終了したかどうかは result.completed で示す。

#### viewed

- **IRI**: `http://id.tincanapi.com/verb/viewed`
- **Display**: `viewed` (en), `閲覧した` (ja)
- **Definition**: 学習コンテンツやアイテムページの閲覧を示す。
- **Scope Note**: eBook、ヒント、解説などのコンテンツ参照時に使用する。

## 3.2.2　ActivityTypes (活動の種類)

### 3.2.2.1　本プロファイルで定義する ActivityType

#### assessment

- **IRI**: `http://adlnet.gov/expapi/activities/assessment`
- **Definition**: アセスメント全体を識別するアクティビティタイプ。
- **Scope Note**: attempted/completed ステートメントで使用する。

#### page

- **IRI**: `http://activitystrea.ms/schema/1.0/page`
- **Definition**: Webコンテンツやアプリにおけるページを表す。
- **Scope Note**: viewed ステートメントで使用する。

## 3.3　Extensions (拡張)

ドメイン横断的に利用されるコンテキスト拡張およびアクティビティ拡張。

### 3.3.1　本プロファイルで定義する Extension

#### difficulty (難易度)

- **IRI**: `https://w3id.org/japan-xapi/extensions/difficulty`
- **Type**: `ContextExtension`
- **Definition**: 学習コンテンツの難易度を示す。
- **Schema**:
  ```json
  { "type": "string" }
  ```

#### subject (教科)

- **IRI**: `https://w3id.org/japan-xapi/extensions/subject`
- **Type**: `ActivityExtension` / `ContextExtension`
- **Definition**: 学習対象の教科名。
- **Scope Note**: 学習指導要領コードまたは教育データ標準の教科名コード表に準拠することを推奨する。
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### grade (学年)

- **IRI**: `https://w3id.org/japan-xapi/extensions/grade`
- **Type**: `ActivityExtension` / `ContextExtension`
- **Definition**: 対象学年。
- **Scope Note**: 文部科学省教育データ標準（主体情報）上の「学年」項目の要素名を推奨する。
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### course_of_study_code (学習指導要領コード)

- **IRI**: `https://w3id.org/japan-xapi/extensions/course-of-study-code`
- **Type**: `ActivityExtension` / `ContextExtension`
- **Definition**: 学習指導要領コード。
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### unit (単元名)

- **IRI**: `https://w3id.org/japan-xapi/extensions/unit`
- **Type**: `ActivityExtension` / `ContextExtension`
- **Definition**: 学習課題やコンテンツが属する単元名。
- **Schema**:
  ```json
  { "type": "string" }
  ```



#### unit (単元名)

- **IRI**: `https://w3id.org/japan-xapi/extensions/unit`
- **Type**: `ActivityExtension` / `ContextExtension`
- **Definition**: 学習課題やコンテンツが属する単元名。
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```


#### due-date (期限日)

- **IRI**: `https://w3id.org/japan-xapi/extensions/due-date`
- **Type**: `ContextExtension`
- **Definition**: 課題等の実施期限日。
- **Schema**:
  ```json
  { "type": "string", "format": "date-time" }
  ```

#### scrapbook_item_type (スクラップブックアイテムタイプ)

- **IRI**: `https://w3id.org/japan-xapi/extensions/scrapbook-item-type`
- **Type**: `ActivityExtension`
- **Definition**: スクラップブック等で作成されるオブジェクトの種類（text, shape, image等）。
- **Schema**:
  ```json
  { "type": "string" }
  ```

#### purpose-of-question (問題の趣旨)

- **IRI**: `https://w3id.org/japan-xapi/extensions/purpose-of-question`
- **Type**: `ActivityExtension`
- **Definition**: 問題の趣旨を表す値。学習指導要領コードよりも細かいレベルで問題の目的を示す。
- **Scope Note**: 例えば「真分数の乗法の計算」など、より細粒度の学習目標を記録できる。複数レベルの趣旨を設定可能。
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### question-order (問題の出題順序)

- **IRI**: `https://w3id.org/japan-xapi/extensions/question-order`
- **Type**: `ActivityExtension`
- **Definition**: デジタルドリルやCBTにおける問題の出題順序を表す値。
- **Scope Note**: アダプティブに出題順序が変化する場合、実際に出題された順序を記録する。
- **Schema**:
  ```json
  { "type": "integer" }
  ```

#### content-type (コンテンツの種類)

- **IRI**: `https://w3id.org/japan-xapi/extensions/content-type`
- **Type**: `ActivityExtension`
- **Definition**: 学習者が参照したものが、問題解答中のヒント、解答後の結果、解答後の解説などのどれであるかを示す。
- **Scope Note**: hint（回答中のヒント）、result（得点、正誤等の結果）、explanation（問題の解説）などの値を持つ。
- **Schema**:
  ```json
  {
    "type": "array",
    "enum": ["hint", "result", "explanation"]
  }
  ```

#### assessment-type (評価のタイプ)

- **IRI**: `https://w3id.org/japan-xapi/extensions/assessment-type`
- **Type**: `ContextExtension`
- **Definition**: 評価のタイプを表す値。
- **Scope Note**: diagnostic（診断的）、formative（形成的）、summative（総括的）のいずれか。
- **Schema**:
  ```json
  {
    "type": "array",
    "enum": ["diagnostic", "formative", "summative"]
  }
  ```

# 4.　Statement Templates (ステートメントテンプレート)

_本プロファイル（Core Profile）では、Statement Template は定義しない。各ドメインプロファイルにて定義される。_
