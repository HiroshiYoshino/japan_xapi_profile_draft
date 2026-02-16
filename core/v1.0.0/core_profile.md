# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるJapan xAPI Core Profile TFにおける学習ログを対象として取りまとめた **Japan xAPI Core Profile** 標準仕様である。  
　本仕様は、全体アーキテクチャに記載されている **Core Concept Profile** としての役割を踏まえ、各ドメイン（Assessment, eBook, LMS等）上で発生する学習ログ記録において共通利用されるConceptsを体系的に定義するための仕様である。

## 1.2　目的

　本ドキュメントは、日本の初等中等教育における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、共通語彙の定義および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各Concept定義は、xAPIプロファイル仕様で定義されているConceptsの構造および考え方に準拠して記載する。  
　本プロファイルは **Concept（概念定義）** を主とし、Statement Template は原則として定義しない（Templateは各ドメインプロファイルで定義する）。  

## 1.4　定義範囲

　本ドキュメントは、Japan xAPI Core Profileを構成する要素のうち、メタ情報、およびドメイン横断的に利用されるConceptsを定義することを目的とする。

## 1.5　本ドキュメントの構成について

　本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- Concepts：本プロファイルで定義する共通語彙

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
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                             |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                            |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                         |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                             |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育を主対象とする学習ログの共通語彙定義プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                         |

# 3.　Concepts (概念定義)

## 3.1　本章の位置づけ

　本章では、Japan xAPI Core Profileにおける共通語彙を定義する。

## 3.3　Extensions (拡張)

ドメイン横断的に利用されるコンテキスト拡張およびアクティビティ拡張。

### 3.3.1　本プロファイルで定義する Extension

#### grade (学年)

- **IRI**: `https://w3id.org/japan-xapi/extensions/grade`
- **Type**: `ActivityExtension`, `ContextExtension`
- **Definition**: 対象学年。
- **Scope Note**: 
  - ActivityExtensionとして使用する場合: オブジェクト（コンテンツや課題）が対象とする学年を示す
  - ContextExtensionとして使用する場合: 学習活動が行われた学年のコンテキストを示す
  - 文部科学省教育データ標準（主体情報）上の「学年」項目の要素名を推奨する
  - 単一の学年の場合は要素数1の配列とする
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### subject (教科)

- **IRI**: `https://w3id.org/japan-xapi/extensions/subject`
- **Type**: `ActivityExtension`, `ContextExtension`
- **Definition**: 学習対象の教科名。
- **Scope Note**: 
  - ActivityExtensionとして使用する場合: オブジェクト（コンテンツや課題）が対象とする教科を示す
  - ContextExtensionとして使用する場合: 学習活動が行われた教科のコンテキストを示す
  - 文部科学省教育データ標準の教科名コード表に準拠することを推奨する
  - 単一の教科の場合は要素数1の配列とする
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### course-of-study-code (学習指導要領コード)

- **IRI**: `https://w3id.org/japan-xapi/extensions/course-of-study-code`
- **Type**: `ActivityExtension`, `ContextExtension`
- **Definition**: 文部科学省学習指導要領に基づく学習項目コード。
- **Scope Note**:
  - ActivityExtensionとして使用する場合: オブジェクト（コンテンツや課題）が対応する学習指導要領コードを示す
  - ContextExtensionとして使用する場合: 学習活動が行われた学習指導要領項目のコンテキストを示す
  - 単一のコードの場合は要素数1の配列とする
  - 複数の学習項目にまたがる場合は複数の要素を含む配列とする
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```

#### unit (単元名)

- **IRI**: `https://w3id.org/japan-xapi/extensions/unit`
- **Type**: `ActivityExtension`, `ContextExtension`
- **Definition**: 学習課題やコンテンツが属する単元名。
- **Scope Note**:
  - ActivityExtensionとして使用する場合: オブジェクト（コンテンツや課題）が対象とする単元を示す
  - ContextExtensionとして使用する場合: 学習活動が行われた単元のコンテキストを示す
  - 単一の単元の場合は要素数1の配列とする
  - 複数の単元にまたがる場合は複数の要素を含む配列とする
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
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

#### content-type (コンテンツの種類)

- **IRI**: `https://w3id.org/japan-xapi/extensions/content-type`
- **Type**: `ActivityExtension`
- **Definition**: 学習者が参照したものが、問題解答中のヒント、解答後の結果、解答後の解説などのどれであるかを示す。
- **Scope Note**: hint（回答中のヒント）、result（得点、正誤等の結果）、explanation（問題の解説）などの値を持つ。
- **Schema**:
  ```json
  {
    "type": "string",
    "enum": ["hint", "result", "explanation"]
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

#### difficulty (難易度)

- **IRI**: `https://w3id.org/japan-xapi/extensions/difficulty`
- **Type**: `ContextExtension`
- **Definition**: 学習コンテンツの難易度を示す。
- **Scope Note**: 学習活動が行われた状況における難易度レベルを示す。難易度の基準は実装に依存する。
- **Schema**:
  ```json
  { "type": "string" }
  ```

#### assessment-type (評価のタイプ)

- **IRI**: `https://w3id.org/japan-xapi/extensions/assessment-type`
- **Type**: `ContextExtension`
- **Definition**: 評価のタイプを表す値。
- **Scope Note**: diagnostic（診断的）、formative（形成的）、summative（総括的）のいずれか。
- **Schema**:
  ```json
  {
    "type": "string",
    "enum": ["diagnostic", "formative", "summative"]
  }
  ```

#### scrapbook-item-type (スクラップブックアイテムタイプ)

- **IRI**: `https://w3id.org/japan-xapi/extensions/scrapbook-item-type`
- **Type**: `ActivityExtension`
- **Definition**: スクラップブック等で作成されるオブジェクトの種類（text, shape, image等）。
- **Scope Note**: グループ学習支援ツールなどで作成されるコンテンツの種別を示す。
- **Schema**:
  ```json
  { "type": "string" }
  ```

#### due-date (期限日)

- **IRI**: `https://w3id.org/japan-xapi/extensions/due-date`
- **Type**: `ContextExtension`
- **Definition**: 課題等の実施期限日。
- **Scope Note**: ISO 8601形式の日時文字列を使用する（例: "2025-11-15T23:59:59Z"）。
- **Schema**:
  ```json
  { "type": "string", "format": "date-time" }
  ```

# 4.　Statement Templates (ステートメントテンプレート)

_本プロファイル（Core Profile）では、Statement Template は定義しない。各ドメインプロファイルにて定義される。_
