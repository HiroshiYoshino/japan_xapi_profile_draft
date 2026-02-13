# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるLMS TFにおける学習ログを対象として取りまとめた **Japan xAPI LMS Profile** 標準仕様である。  
　本仕様は、学習管理システム（LMS）分野に記載されている特性を踏まえ、学習課題の配布、提出、評価などのプロセスに関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、LMSにおける学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、LMSプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateで使用される語彙（Verb、ActivityType、Extension等）は以下のいずれかに整理される。(1) SWG独自に定義した語彙を使用する場合、Core Profile内のConceptsに定義されている。(2) ADLや他の標準で定義済みの語彙を使用する場合、それらを直接参照し、Domain Profileで再定義しない。Domain Profile（本プロファイルはDomain Profileの1つ）としてLMS Profileは Statement Templateおよび Rules の定義に集中し、語彙定義はCore Profileに委譲する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、LMSにおける学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

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

　本ドキュメントは、Japan xAPI LMS Profileを構成する要素のうち、メタ情報、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、LMSにおける学習行動が非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本ドキュメントの構成について

　本紙は、xAPIプロファイル仕様に基づき、LMS学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                     | 説明                                   | 値                                                    |
| :----------------------- | :------------------------------------- | :---------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/lms`            |
| **type**                 | オブジェクトタイプ                     | `Profile`                                             |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                  |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI LMS Profile                                |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                               |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                            |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育におけるLMS学習ログのプロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                            |

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

# 3. 学習課題に関するユースケース

「学習課題」を次の通り定義する。
「学習課題」とは以下のいずれかのObjectである。
**① ”教職員”が”児童生徒”に対して行った学習活動の指示の内容を表すもの**
**② ”児童生徒”が”自身”に対して行った学習活動の指示の内容を表すもの**

ここでの学習活動とは、それが児童生徒の学びに資すると教職員または児童生徒が考えるものすべてを指す。

学習活動の例

- 授業動画を視聴すること
- ドリル問題に解答すること
- テストを受けること
- 新聞のニュースから興味のあるものを切り抜き、スクラップブックを作ること
- 学習計画を作ること

学習課題の例

- 授業動画A,B,CをX月X日までに視聴すること（親課題）
  - 授業動画Aを視聴すること（子課題A）
  - 授業動画Bを視聴すること（子課題B）
  - 授業動画Cを視聴すること（子課題C）
- ドリル問題A,B,Cに解答し、X月X日までに正答率100％となるよう繰り返し取り組むこと
- テストAをX月X日までに受けること
- 新聞のニュースから興味のあるものを切り抜き、スクラップブックをX月X日までに作ること
- 教科：aaa、単元：bbbの学習計画をX月X日までに作ること

学習課題は、学習活動要素と指示要素に分けられる。

学習活動要素：誰が、いつ、何を学ぶか。（＋その結果がどうであったか）
指示要素：いつまでに、どこからどこまでを、超えるべき基準値は何か。

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、LMSプロファイルにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

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

### 4.3.1　学習課題の作成

#### 4.3.1.1　基本仕様

- 学習課題を作成したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                          |
| :------- | :----------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-created |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0              |
| prefLabel | 学習課題の作成                                              |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | https://w3id.org/xapi/adl/verbs/created               |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.1.2　記述規則（Rules）

| 項目     | 説明                                       | Location (JSONPath)                                                                | Presence    |
| :------- | :----------------------------------------- | :--------------------------------------------------------------------------------- | :---------- |
| **単元名** | 学習課題が属する単元名。                  | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/unit']`    | recommended |
| **期限日** | 学習課題の実施期限日。ISO 8601形式。      | `$.context.extensions['https://w3id.org/japan-xapi/extensions/due-date']`          | recommended |
| **教科** | Core Profileで定義された教科Extensionを使用する。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/subject']` | recommended |
| **学年** | Core Profileで定義された学年Extensionを使用する。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/grade']`   | recommended |

### 4.3.2　学習課題の配布

#### 4.3.2.1　基本仕様

- 学習課題を児童生徒に配布したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                         |
| :------- | :---------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-shared |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0             |
| prefLabel | 学習課題の配布                                             |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/shared                 |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.2.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | shared                           | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |

### 4.3.3　学習課題の実施開始

#### 4.3.3.1　基本仕様

- 学習課題を開始したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                           |
| :------- | :------------------------------------------------------------ |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-launched |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0               |
| prefLabel | 学習課題の実施開始                                           |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/launched               |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.3.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | launched                         | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |

### 4.3.4　学習課題の完了

#### 4.3.4.1　基本仕様

- 学習課題を完了したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                            |
| :------- | :------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-completed |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0                |
| prefLabel | 学習課題の完了                                                |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/completed              |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.4.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | completed                        | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |

### 4.3.5　学習課題へのフィードバック

#### 4.3.5.1　基本仕様

- 教職員が児童生徒の学習課題成果にコメントなどのフィードバックを行ったことを表すステートメント。
- 識別情報

| 項目     | 値                                                            |
| :------- | :------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-responded |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0                |
| prefLabel | 学習課題へのフィードバック                                    |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/responded              |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.5.2　記述規則（Rules）

共通記述規則に準拠する。ただし、result.response および result.completion は、本仕様において任意（MAY）の項目であるため、本記述規則による制約を課さない。

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | responded                        | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |
| **フィードバック内容** | 後ろに続く結果オブジェクトに含められる。    | `$.result.response` | optional |
| **完了フラグ** | フィードバック後の完了状態                          | `$.result.completion` | optional |

### 4.3.6　学習課題を閲覧する

#### 4.3.6.1　基本仕様

- 児童生徒が学習課題を閲覧したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                         |
| :------- | :---------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-viewed |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0             |
| prefLabel | 学習課題を閲覧する                                         |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | http://id.tincanapi.com/verb/viewed                   |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.6.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | viewed                           | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |

### 4.3.7　学習課題を異常終了する

#### 4.3.7.1　基本仕様

- 児童生徒が学習課題を異常終了（放棄）したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                            |
| :------- | :------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-abandoned |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0                |
| prefLabel | 学習課題を異常終了する                                        |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | https://w3id.org/xapi/adl/verbs/abandoned             |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.7.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | abandoned                        | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |

### 4.3.8　学習課題の実施状況を初期化する

#### 4.3.8.1　基本仕様

- 学習課題の実施状況が初期化されたことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                              |
| :------- | :--------------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-initialized |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0                  |
| prefLabel | 学習課題の実施状況を初期化する                                  |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/initialized            |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.8.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | initialized                      | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |

### 4.3.9　学習課題を免除する

#### 4.3.9.1　基本仕様

- 教職員が児童生徒の学習課題を免除したことを記録するためのテンプレート。
- 識別情報

| 項目     | 値                                                         |
| :------- | :---------------------------------------------------------- |
| id       | https://w3id.org/japan-xapi/templates/lms/assessment-waived |
| inScheme | https://w3id.org/japan-xapi/profiles/lms/v1.0.0             |
| prefLabel | 学習課題を免除する                                         |

- 判定条件

| 項目              | 値                                                     |
| :---------------- | :---------------------------------------------------- |
| verb              | https://w3id.org/xapi/adl/verbs/waived                |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |

#### 4.3.9.2　記述規則（Rules）

| 項目     | 説明                               | Location (JSONPath) | Presence |
| :------- | :--------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)** | waived                           | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ** | Assignment等の学習課題        | `$.object.objectType` | included |
| **オブジェクトID** | 学習課題を一意に識別するID                      | `$.object.id` | included |
