# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるJapan xAPI Core Profile TFにおける学習ログを対象として取りまとめた **Japan xAPI Core Profile** 標準仕様（案）である。  
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

| 項目                    | 説明                                   | 値                                                                 |
| :---------------------- | :------------------------------------- | :----------------------------------------------------------------- |
| プロファイル名 name     | プロファイルを識別する名称             | Japan xAPI Core Profile                                            |
| バージョン version      | プロファイルの改訂番号やリリース状態   | v1.0.0                                                             |
| 作成者/管理者 publisher | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                            |
| 作成日/更新日 created   | 文書化日または改訂日                   | 2026年4月1日                                                       |
| 言語 languages          | メタ情報およびプロファイルの記載言語   | 日本語                                                             |
| 目的/説明 description   | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育を主対象とする学習ログの共通語彙定義プロファイル |
| ドキュメントバージョン  | 文書版数                               | 2026年度版                                                         |

# 3.　Concepts (概念定義)

## 3.1　本章の位置づけ

　本章では、Japan xAPI Core Profileにおける共通語彙（Verbs, Extensions）を定義する。

## 3.2　Verbs (動詞)

### 3.2.1　本プロファイルで定義する Verb

#### highlighted

- **IRI**: `https://w3id.org/japan-xapi/verbs/highlighted`
- **Display**: `highlighted` (en), `ハイライトした` (ja)
- **Definition**: テキストや画像の一部を強調表示する行為。
- **Scope Note**: 重要な箇所へのマーキング等に使用する。

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

# 4.　Statement Templates (ステートメントテンプレート)

_本プロファイル（Core Profile）では、Statement Template は定義しない。各ドメインプロファイルにて定義される。_
