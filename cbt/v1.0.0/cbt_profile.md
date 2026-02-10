# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるデジタルドリル/CBT TFにおける学習ログを対象として取りまとめた **Japan xAPI CBT Profile** 標準仕様（案）である。  
　本仕様は、デジタルドリル/CBT分野に記載されている特性を踏まえ、CBTシステム上で発生するアセスメント実施や解答に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、CBT/デジタルドリルにおける学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、CBTプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateで使用される語彙（Verb、ActivityType、Extension等）については、Core Profile内のConceptsに定義されている。Domain Profile（本プロファイルはDomain Profileの1つ）としてCBT Profileは Statement Templateおよび Rules の定義に集中し、語彙定義はCore Profileに委譲する。  
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

| 項目                     | 説明                                   | 値                                                       |
| :----------------------- | :------------------------------------- | :------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/cbt`               |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                     |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI CBT Profile                                   |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                   |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                  |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                               |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                   |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本のCBT/デジタルドリルにおける学習ログ標準プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                               |

## 2.3　共通記述規則

　本プロファイルで定義するすべてのStatementTemplateに対して、以下のRulesを適用する。

| 項目説明 (Description / ScopeNote)   | Location (JSONPath)                        | Presence    |
| :----------------------------------- | :----------------------------------------- | :---------- |
| **ステートメントID**                 | `$.id`                                     | included    |
| **タイムスタンプ**                   | `$.timestamp`                              | included    |
| **アクター**                         | `$.actor`                                  | included    |
| **アクターのオブジェクトタイプ**     | `$.actor.objectType`                       | included    |
| **アクターのアカウントホームページ** | `$.actor.account.homePage`                 | included    |
| **アクターのアカウント名**           | `$.actor.account.name`                     | included    |
| **動詞の表示名(英語)**               | `$.verb.display.en`                        | included    |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType`                      | included    |
| **オブジェクトID**                   | `$.object.id`                              | included    |
| **オブジェクト定義のタイプ**         | `$.object.definition.type`                 | included    |
| **オブジェクト定義の名称(日本語)**   | `$.object.definition.name['ja-JP']`        | recommended |
| **オブジェクト定義の説明(日本語)**   | `$.object.definition.description['ja-JP']` | recommended |
| **コンテキスト**                     | `$.context`                                | included    |
| **コンテキストの言語**               | `$.context.language`                       | included    |
| **コンテキストのプラットフォーム**   | `$.context.platform`                       | included    |
| **プロファイルバージョン**           | `$.version`                                | included    |

# 3. CBT/デジタルドリルに関するユースケース

CBT/デジタルドリルにおける主なユースケースは、学習者がドリルやテストなどのアセスメントに取り組み、その結果を記録することである。

主な学習活動の例：

- **アセスメントの実施**: 学習者がドリルやテストを開始し、一連の問題に取り組む。
- **問題への回答**: 個々の問題に対して解答を行い、正誤や得点を確認する。
- **解説やヒントの参照**: 問題に取り組む中で、ヒントを見たり、解答後に解説を読んだりする。
- **結果の確認**: アセスメント全体の正答率や合否などの結果を確認する。

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

| id        | https://w3id.org/japan-xapi/templates/cbt/attempted |
| :-------- | :------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/cbt/v1.0.0                |
| prefLabel | Assessmentの開始                                               |

- 判定条件

| verb               | http://adlnet.gov/expapi/verbs/attempted       |
| :----------------- | :--------------------------------------------- |

#### 4.3.1.2　記述規則（Rules）

1. $.object.definition.name.ja-JP
   1. recommended
   2. Assessmentの日本語表示名
2. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Activity拡張 (Core Profile参照)
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年・Activity拡張 (Core Profile参照)
4. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
   1. recommended
   2. 学習指導要領コード・Activity拡張 (Core Profile参照)
5. $.context.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Context拡張 (Core Profile参照)
6. $.context.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年・Context拡張 (Core Profile参照)
7. $.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
   1. recommended
   2. 学習指導要領コード・Context拡張 (Core Profile参照)
8. $.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']
   1. recommended
   2. 評価タイプ（診断的/形成的/総括的）(Core Profile参照)
9. $.context.contextActivities.grouping[*].id
   1. recommended
   2. ある一回のAssessmentの取り組みに対して同一のIRIを記述する

#### 4.3.1.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                                           | Location (JSONPath)                                                                          | Presence    |
| :------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- | :---------- |
| **Assessmentの日本語表示名**                                                                 | `$.object.definition.name.ja-JP`                                                             | recommended |
| **教科（Activity拡張）**<br>Core Profileで定義された教科Extensionを使用する。                | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']`           | recommended |
| **学年（Activity拡張）**<br>Core Profileで定義された学年Extensionを使用する。                | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']`             | recommended |
| **学習指導要領コード（Activity拡張）**<br>Core Profileで定義された学習指導要領コード拡張。  | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']` | recommended |
| **教科（Context拡張）**<br>Core Profileで定義された教科Extensionを使用する。                | `$.context.extensions['https://w3id.org/japan-xapi/extensions/subject']`                     | recommended |
| **学年（Context拡張）**<br>Core Profileで定義された学年Extensionを使用する。                | `$.context.extensions['https://w3id.org/japan-xapi/extensions/grade']`                       | recommended |
| **学習指導要領コード（Context拡張）**<br>Core Profileで定義された学習指導要領コード拡張。  | `$.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']`       | recommended |
| **評価タイプ**<br>診断的(diagnostic)、形成的(formative)、総括的(summative)のいずれかを指定。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']`             | recommended |
| **Assessment実施グループID**<br>ある一回のAssessmentの取り組みに対して同一のIRIを記述。     | `$.context.contextActivities.grouping[*].id`                                                 | recommended |
| **活動発生日時**                                                                             | `$.timestamp`                                                                                | included    |

### 4.3.2　問題への回答

#### 4.3.2.1　基本仕様

- 学習者が得点・正誤判定単位の設問に回答したことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/cbt/answered |
| :-------- | :---------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/cbt/v1.0.0             |
| prefLabel | 問題への回答                                                |

- 判定条件

| verb | http://adlnet.gov/expapi/verbs/answered |
| :--- | :-------------------------------------- |

#### 4.3.2.2　記述規則（Rules）

1. $.object.definition.name.ja-JP
   1. recommended
   2. 問題の日本語表示名
2. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Activity拡張 (Core Profile参照)
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年・Activity拡張 (Core Profile参照)
4. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
   1. recommended
   2. 学習指導要領コード・Activity拡張 (Core Profile参照)
5. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/purpose-of-question']
   1. recommended
   2. 問題の趣旨 (Core Profile参照)
6. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/question-order']
   1. recommended
   2. 出題順序 (Core Profile参照)
7. $.result.score.scaled
   1. included
   2. 得点率 (0.0 - 1.0)
8. $.result.score.raw
   1. included
   2. 素点
9. $.result.score.max
   1. included
   2. 最大点
10. $.result.score.min
   1. optional
   2. 最小点   
11. $.result.response
    1. recommended
    2. 回答値
12. $.result.duration
    1. recommended
    2. 回答所要時間
13. $.context.extensions['https://w3id.org/japan-xapi/extensions/subject']
    1. recommended
    2. 教科・Context拡張 (Core Profile参照)
14. $.context.extensions['https://w3id.org/japan-xapi/extensions/grade']
    1. recommended
    2. 学年・Context拡張 (Core Profile参照)
15. $.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
    1. recommended
    2. 学習指導要領コード・Context拡張 (Core Profile参照)
16. $.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']
    1. recommended
    2. 評価タイプ (Core Profile参照)
17. $.context.contextActivities.grouping[*].id
    1. recommended
    2. ある一回のAssessmentの取り組みに対して同一のIRIを記述する

#### 4.3.2.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                                          | Location (JSONPath)                                                                          | Presence    |
| :------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- | :---------- |
| **問題の日本語表示名**                                                                      | `$.object.definition.name.ja-JP`                                                             | recommended |
| **教科（Activity拡張）**<br>Core Profileで定義された教科Extensionを使用する。               | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']`           | recommended |
| **学年（Activity拡張）**<br>Core Profileで定義された学年Extensionを使用する。               | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']`             | recommended |
| **学習指導要領コード（Activity拡張）**<br>Core Profileで定義された学習指導要領コード拡張。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']` | recommended |
| **問題の趣旨**<br>学習指導要領より細粒度の学習目標を記録。                                  | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/purpose-of-question']` | recommended |
| **出題順序**<br>デジタルドリルやCBTにおける問題の出題順序。                                 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/question-order']`    | recommended |
| **得点率**<br>0.0から1.0の実数。                                                            | `$.result.score.scaled`                                                                      | included    |
| **素点**                                                                                    | `$.result.score.raw`                                                                         | included    |
| **最大点**                                                                                  | `$.result.score.max`                                                                         | included    |
| **回答値**                                                                                  | `$.result.response`                                                                          | recommended |
| **回答所要時間**                                                                            | `$.result.duration`                                                                          | recommended |
| **教科（Context拡張）**<br>Core Profileで定義された教科Extensionを使用する。               | `$.context.extensions['https://w3id.org/japan-xapi/extensions/subject']`                     | recommended |
| **学年（Context拡張）**<br>Core Profileで定義された学年Extensionを使用する。               | `$.context.extensions['https://w3id.org/japan-xapi/extensions/grade']`                       | recommended |
| **学習指導要領コード（Context拡張）**<br>Core Profileで定義された学習指導要領コード拡張。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']`       | recommended |
| **評価タイプ**<br>診断的(diagnostic)、形成的(formative)、総括的(summative)のいずれか。      | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']`             | recommended |
| **Assessment実施グループID**<br>ある一回のAssessmentの取り組みに対して同一のIRIを記述。   | `$.context.contextActivities.grouping[*].id`                                                 | recommended |
| **活動発生日時**                                                                            | `$.timestamp`                                                                                | included    |

#### 4.3.2.4 補記
- 問題に得点や部分点がある場合は、その得点情報を$.result.scoreに記録する。
  - 例1:一つの問題に回答欄が一つあり問題の配点が5点の場合、maxを5、rawを5(正答)または0(誤答)、scaledを1(正答)または0(誤答)とする。
  - 例2:一つの問題に回答欄が二つあり、それぞれで得点が設定されている場合、例えば回答欄一つ目が3点、二つ目が2点の場合、maxを5、rawを5(両方正答)または3(回答欄一つ目を正答)または2(回答欄二つ目を正答)または0(両方誤答)、scaledを1(両方正答)または0.6(回答欄一つ目を正答)または0.4(回答欄二つ目を正答)または0(両方誤答)とする。
- 正誤情報のみあり得点情報がない場合は、正誤の判定箇所の数をそのまま得点として$.result.scoreに記録する。
  - 例1:一つの問題に回答欄が一つある場合、maxを1、rawを1(正答)または0(誤答)、scaledを1(正答)または0(誤答)とする。
  - 例2:一つの問題に回答欄が二つあり、それぞれで正誤の判定ができる場合、maxを2、rawを2(回答欄二つともに正答)または1(回答欄の一つを正答)または0(回答欄の両方を誤答)、scaledを1(回答欄二つともに正答)または0.5(回答欄の一つを正答)または0(回答欄の両方を誤答)とする。
- $.result.score.scaledは、(raw-min)/(max-min) の計算結果とする。
  - minは省略可能とするが、minが0でない場合は必ず含めることを求める。minを省略した場合は0とみなす。
  - 小数点の桁数についてはSCORM プロファイル仕様を参考に、最大で小数点以下については7桁まで・8桁目を四捨五入とする。
    - 例:0.3333333、0.6666667など
- 採点が自動以外で採点が未実施の場合はresult.scoreが出力できない。このため採点が未実施の段階のstatementではcontext.contextActivities.category[*]で本プロファイルのIRIを参照しない。採点終了後にresult.scoreを出力した際に本プロファイルの参照を行うこととする。
- 一回のデジタルドリル/CBTの取り組みを通じて、同じ問題を複数回回答する場合がある。その場合、同じ問題に対する各回答をそれぞれ別の問題解答のステートメントで記録することとする。
- Determining PropertiesにおいてobjectActivityTypeは指定せず、任意のobjectActivityTypeに対して本テンプレートのルールを適用可能とすることで、MEXCBTの「タイプ1」「タイプ2」双方に対応可能とする。


### 4.3.3　学習コンテンツやページの参照

#### 4.3.3.1　基本仕様

- 学習コンテンツやページの閲覧を記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/cbt/viewed |
| :-------- | :------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/cbt/v1.0.0          |
| prefLabel | 学習コンテンツやページの参照                             |

- 判定条件

| verb               | http://id.tincanapi.com/verb/viewed     |
| :----------------- | :-------------------------------------- |

#### 4.3.3.2　記述規則（Rules）

1. $.object.definition.name.ja-JP
   1. recommended
   2. コンテンツの日本語表示名
2. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Activity拡張 (Core Profile参照)
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年・Activity拡張 (Core Profile参照)
4. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
   1. recommended
   2. 学習指導要領コード・Activity拡張 (Core Profile参照)
5. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/content-type']
   1. recommended
   2. コンテンツの種類 (hint/result/explanation) (Core Profile参照)
6. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/purpose-of-question']
   1. recommended
   2. 問題の趣旨 (Core Profile参照)
7. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/question-order']
   1. recommended
   2. 出題順序 (Core Profile参照)
8. $.context.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Context拡張 (Core Profile参照)
9. $.context.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年・Context拡張 (Core Profile参照)
10. $.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
    1. recommended
    2. 学習指導要領コード・Context拡張 (Core Profile参照)
11. $.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']
    1. recommended
    2. 評価タイプ (Core Profile参照)
12. $.context.contextActivities.grouping[*].id
    1. recommended
    2. ある一回のAssessmentの取り組みに対して同一のIRIを記述する
13. $.context.contextActivities.parent[*].id
    1. recommended
    2. ヒントや解説の対象となるAssessmentまたはQuestionのID

#### 4.3.3.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                                          | Location (JSONPath)                                                                          | Presence    |
| :------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------- | :---------- |
| **コンテンツの日本語表示名**                                                                | `$.object.definition.name.ja-JP`                                                             | recommended |
| **教科（Activity拡張）**<br>Core Profileで定義された教科Extensionを使用する。               | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']`           | recommended |
| **学年（Activity拡張）**<br>Core Profileで定義された学年Extensionを使用する。               | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']`             | recommended |
| **学習指導要領コード（Activity拡張）**<br>Core Profileで定義された学習指導要領コード拡張。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']` | recommended |
| **コンテンツの種類**<br>hint(ヒント), result(結果), explanation(解説) 等                    | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/content-type']`      | recommended |
| **問題の趣旨**<br>学習指導要領より細粒度の学習目標を記録。                                  | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/purpose-of-question']` | recommended |
| **出題順序**<br>デジタルドリルやCBTにおける問題の出題順序。                                 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/question-order']`    | recommended |
| **教科（Context拡張）**<br>Core Profileで定義された教科Extensionを使用する。               | `$.context.extensions['https://w3id.org/japan-xapi/extensions/subject']`                     | recommended |
| **学年（Context拡張）**<br>Core Profileで定義された学年Extensionを使用する。               | `$.context.extensions['https://w3id.org/japan-xapi/extensions/grade']`                       | recommended |
| **学習指導要領コード（Context拡張）**<br>Core Profileで定義された学習指導要領コード拡張。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']`       | recommended |
| **評価タイプ**<br>診断的(diagnostic)、形成的(formative)、総括的(summative)のいずれか。      | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']`             | recommended |
| **Assessment実施グループID**<br>ある一回のAssessmentの取り組みに対して同一のIRIを記述。   | `$.context.contextActivities.grouping[*].id`                                                 | recommended |
| **親アクティビティID**<br>関連する問題や評価のID                                            | `$.context.contextActivities.parent[*].id`                                                   | recommended |
| **活動発生日時**                                                                            | `$.timestamp`                                                                                | included    |

### 4.3.4　Assessmentの終了

#### 4.3.4.1　基本仕様

- Assessmentの終了を記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/cbt/completed |
| :-------- | :------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/cbt/v1.0.0                |
| prefLabel | Assessmentの終了                                               |

- 判定条件

| verb               | http://adlnet.gov/expapi/verbs/completed       |
| :----------------- | :--------------------------------------------- |

#### 4.3.4.2　記述規則（Rules）

1. $.object.definition.name.ja-JP
   1. recommended
   2. Assessmentの日本語表示名
2. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']
   1. recommended
   2. 教科・Activity拡張 (Core Profile参照)
3. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']
   1. recommended
   2. 学年・Activity拡張 (Core Profile参照)
4. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
   1. recommended
   2. 学習指導要領コード・Activity拡張 (Core Profile参照)
5. $.result.score.scaled
   1. included
   2. 得点率 (0.0 - 1.0)
6. $.result.score.raw
   1. included
   2. 素点
7. $.result.score.max
   1. included
   2. 最大点
8. $.result.score.min
   1. optional
   2. 最小点
9. $.result.success
   1. recommended
   2. 完了フラグ (true/false)
10. $.result.duration
   1. recommended
   2. 所要時間 (ISO 8601 duration)
11. $.context.extensions['https://w3id.org/japan-xapi/extensions/subject']
    1. recommended
    2. 教科・Context拡張 (Core Profile参照)
12. $.context.extensions['https://w3id.org/japan-xapi/extensions/grade']
    1. recommended
    2. 学年・Context拡張 (Core Profile参照)
13. $.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']
    1. recommended
    2. 学習指導要領コード・Context拡張 (Core Profile参照)
14. $.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']
    1. recommended
    2. 評価タイプ (Core Profile参照)
15. $.context.contextActivities.grouping[*].id
    1. recommended
    2. ある一回のAssessmentの取り組みに対して同一のIRIを記述する

#### 4.3.4.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                            | Location (JSONPath)                                                                          | Presence    |
| :------------------------------------------------------------ | :------------------------------------------------------------------------------------------- | :---------- |
| **Assessment名**                                              | `$.object.definition.name.ja-JP`                                                             | recommended |
| **教科（Activity拡張）**<br>Core Profileで定義された教科Extension。    | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']`           | recommended |
| **学年（Activity拡張）**<br>Core Profileで定義された学年Extension。    | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']`             | recommended |
| **学習指導要領コード（Activity拡張）**<br>Core Profileで定義。        | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']` | recommended |
| **得点率**<br>0.0から1.0の実数。                              | `$.result.score.scaled`                                                                      | included    |
| **素点**                                                      | `$.result.score.raw`                                                                         | included    |
| **最大点**                                                    | `$.result.score.max`                                                                         | included    |
| **完了フラグ**<br>最後まで完了した場合はtrue、途中終了はfalse | `$.result.success`                                                                           | recommended |
| **所要時間**<br>ISO 8601期間形式 (例: PT1H30M)                | `$.result.duration`                                                                          | recommended |
| **教科（Context拡張）**<br>Core Profileで定義された教科Extension。    | `$.context.extensions['https://w3id.org/japan-xapi/extensions/subject']`                     | recommended |
| **学年（Context拡張）**<br>Core Profileで定義された学年Extension。    | `$.context.extensions['https://w3id.org/japan-xapi/extensions/grade']`                       | recommended |
| **学習指導要領コード（Context拡張）**<br>Core Profileで定義。        | `$.context.extensions['https://w3id.org/japan-xapi/extensions/course-of-study-code']`       | recommended |
| **評価タイプ**<br>診断的(diagnostic)、形成的(formative)、総括的(summative)。 | `$.context.extensions['https://w3id.org/japan-xapi/extensions/assessment-type']`             | recommended |
| **Assessment実施グループID**<br>ある一回のAssessmentの取り組みに対して同一のIO。 | `$.context.contextActivities.grouping[*].id`                                                 | recommended |
| **活動発生日時**                                              | `$.timestamp`                                                                                | included    |

#### 4.3.4.4 補記
- $.result.score.scaledは、(raw-min)/(max-min) の計算結果とする。
  - minは省略可能とするが、minが0でない場合は必ず含めることを求める。minを省略した場合は0とみなす。
  - 小数点の桁数についてはSCORM プロファイル仕様を参考に、最大で小数点以下については7桁まで・8桁目を四捨五入とする。
    - 例:0.3333333、0.6666667など
- 採点が自動以外で採点が未実施の場合はresult.scoreが出力できない。このため採点が未実施の段階のstatementでは本プロファイルの参照を行わないこととする。すべての採点終了後にresult.scoreを出力した際に本プロファイルの参照を行うこととする。
- 一回のデジタルドリル/CBTの取り組みを通じて、同じ問題を複数回回答する場合がある。その場合、$.result.scoreには各問題に対して一番最後に解答した結果を集計した得点を最終的な達成点として記録することを想定する。過程については個別の問題解答のステートメントで記録することとする。
