# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるデジタルドリル/CBT TFにおける学習ログを対象として取りまとめた **Japan xAPI CBT Profile** 標準仕様（案）である。  
　本仕様は、デジタルドリル/CBT分野に記載されている特性を踏まえ、CBTシステム上で発生するアセスメント実施や解答に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、CBT/デジタルドリルにおける学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、CBTプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateのうち独自に定義したものについては、coreプロファイル内のconceptに記載している。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、CBT/デジタルドリルにおける学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

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

　本ドキュメントは、Japan xAPI CBT Profileを構成する要素のうち、メタ情報、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、CBT/デジタルドリルが非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本ドキュメントの構成について

　本紙は、xAPIプロファイル仕様に基づき、CBT/デジタルドリル学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                    | 説明                                   | 値                                                       |
| :---------------------- | :------------------------------------- | :------------------------------------------------------- |
| プロファイル名 name     | プロファイルを識別する名称             | Japan xAPI CBT Profile                                   |
| バージョン version      | プロファイルの改訂番号やリリース状態   | v1.0.0                                                   |
| 作成者/管理者 publisher | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                  |
| 作成日/更新日 created   | 文書化日または改訂日                   | 2026年4月1日                                             |
| 言語 languages          | メタ情報およびプロファイルの記載言語   | 日本語                                                   |
| 目的/説明 description   | プロファイルが対象とする学習ログや用途 | 日本のCBT/デジタルドリルにおける学習ログ標準プロファイル |
| ドキュメントバージョン  | 文書版数                               | 2026年度版                                               |

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、CBTプロファイルにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

## 4.2　前提条件

- 基本仕様
  - 冒頭にdifinitionの位置づけとして、Templateの目的やどのような操作を記録するためのものかを定義する。
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

### 4.3.1　Assessmentの開始

#### 4.3.1.1　基本仕様

- Assessmentの提供開始（受験開始操作やページ表示）を記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/cbt/assessment-attempted |
| :-------- | :------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/cbt/v1.0.0                |
| prefLabel | Assessmentの開始                                               |

- 判定条件

| verb               | http://adlnet.gov/expapi/verbs/attempted       |
| :----------------- | :--------------------------------------------- |
| objectActivityType | http://adlnet.gov/expapi/activities/assessment |

#### 4.3.1.2　記述規則（Rules）

1. $.object.definition.name.ja-jp
   1. recommended
   2. Assessmentの日本語表示名
2. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科 (Core Profile参照)
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年 (Core Profile参照)
4. $.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']
   1. recommended
   2. 評価タイプ（診断的/形成的/総括的）

#### 4.3.1.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                                           | Location (JSONPath)                                                                | Presence    |
| :------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------- | :---------- |
| **Assessmentの日本語表示名**                                                                 | `$.object.definition.name.ja-jp`                                                   | recommended |
| **教科**<br>Core Profileで定義された教科Extensionを使用する。                                | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
| **学年**<br>Core Profileで定義された学年Extensionを使用する。                                | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']`   | recommended |
| **評価タイプ**<br>診断的(diagnostic)、形成的(formative)、総括的(summative)のいずれかを指定。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']`   | recommended |
| **活動発生日時**                                                                             | `$.timestamp`                                                                      | included    |

### 4.3.2　問題への回答

#### 4.3.2.1　基本仕様

- 学習者が得点・正誤判定単位の設問に回答したことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/cbt/question-answered |
| :-------- | :---------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/cbt/v1.0.0             |
| prefLabel | 問題への回答                                                |

- 判定条件

| verb | http://adlnet.gov/expapi/verbs/answered |
| :--- | :-------------------------------------- |

#### 4.3.2.2　記述規則（Rules）

1. $.result.score.scaled
   1. included
   2. 得点率 (0.0 - 1.0)
2. $.result.score.raw
   1. included
   2. 素点
3. $.result.score.max
   1. included
   2. 最大点
4. $.result.response
   1. recommended
   2. 回答値
5. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/question-order']
   1. recommended
   2. 出題順序

#### 4.3.2.3　Markdownテーブル

| 項目説明 (Description / ScopeNote) | Location (JSONPath)                                                                       | Presence    |
| :--------------------------------- | :---------------------------------------------------------------------------------------- | :---------- |
| **得点率**<br>0.0から1.0の実数。   | `$.result.score.scaled`                                                                   | included    |
| **素点**                           | `$.result.score.raw`                                                                      | included    |
| **最大点**                         | `$.result.score.max`                                                                      | included    |
| **回答値**                         | `$.result.response`                                                                       | recommended |
| **回答所要時間**                   | `$.result.duration`                                                                       | recommended |
| **出題順序**                       | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/question-order']` | recommended |
