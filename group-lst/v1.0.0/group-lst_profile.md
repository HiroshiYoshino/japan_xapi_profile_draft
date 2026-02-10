# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるグループ学習支援ツールTFにおける学習ログを対象として取りまとめた **Japan xAPI Group Learning Support Tool Profile** 標準仕様である。  
　本仕様は、グループ学習支援ツール分野に記載されている特性を踏まえ、グループ学習における個人の操作や協働的な学習活動（議論、共同編集等）に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、グループ学習支援ツールにおける学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、グループ学習支援ツールプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateで使用される語彙（Verb、ActivityType、Extension等）は以下のいずれかに整理される。(1) SWG独自に定義した語彙を使用する場合、Core Profile内のConceptsに定義されている。(2) ADLや他の標準で定義済みの語彙を使用する場合、それらを直接参照し、Domain Profileで再定義しない。Domain Profile（本プロファイルはDomain Profileの1つ）としてGroup Learning Support Tool Profileは Statement Templateおよび Rules の定義に集中し、語彙定義はCore Profileに委譲する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、グループ学習支援ツールにおける学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

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

　本ドキュメントは、Japan xAPI Group Learning Support Tool Profileを構成する要素のうち、メタ情報、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、グループ学習活動が非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本ドキュメントの構成について

　本紙は、xAPIプロファイル仕様に基づき、グループ学習支援ツール学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                     | 説明                                   | 値                                                                   |
| :----------------------- | :------------------------------------- | :------------------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/group-lst`                     |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                            |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                                 |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI Group Learning Support Tool Profile                       |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                               |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                              |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                           |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                               |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育におけるグループ学習支援ツールログ標準プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                           |

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

# 3. グループ学習に関するユースケース

「グループ学習」とは、個人ないし集団が行う学習活動を指す。グループ学習でありつつ、個人の学習活動も範囲とする理由として、個人の考えを作成した後にグループで交流し、また、グループで交流したことを踏まえて個人の考えを編集するといった往還が見られるためであり、厳密に弁別できないためである。

主な学習活動の例：

- 自分や自分たちの考えをテキストやオブジェクト等で表現すること
- 友達の考えに対して「いいね」を送るなど、反応すること
- 友達の考えに対してコメントしたりフィードバックしたりすること

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、グループ学習支援ツールプロファイルにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

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

### 4.3.1　ツールの起動

#### 4.3.1.1　基本仕様

- グループ学習支援ツールがシステムとして起動されたことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/group-lst/tool-launched |
| :-------- | :--------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0           |
| prefLabel | ツールの起動                                              |

- 判定条件

| verb               | https://w3id.org/xapi/adl/verbs/launched               |
| :----------------- | :------------------------------------------------------ |
| objectActivityType | https://w3id.org/japan-xapi/activity-types/group-lst/tool |

#### 4.3.1.2　記述規則（Rules）

なし。共通記述規則に準拠する。

#### 4.3.1.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                     | Location (JSONPath) | Presence |
| :----------------------------------------------------- | :------------------ | :------- |
| **ツールID**<br>起動したツールを識別するIRIまたはURL。 | `$.object.id`       | included |

### 4.3.2　ツール内でのコンテンツ利用開始

#### 4.3.2.1　基本仕様

- ツール内の特定コンテンツ（スライド等）の利用を開始したことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/group-lst/content-launched |
| :-------- | :--------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0            |
| prefLabel | ツール内でのコンテンツ利用開始                               |

- 判定条件

| verb               | https://w3id.org/xapi/adl/verbs/launched   |
| :----------------- | :----------------------------------------- |
| objectActivityType | http://id.tincanapi.com/activitytype/slide |

#### 4.3.2.2　記述規則（Rules）

なし。共通記述規則に準拠する。

#### 4.3.2.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                   | Location (JSONPath) | Presence |
| :------------------------------------------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)**<br>launched                                   | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ**<br>Slide等のコンテンツ           | `$.object.objectType` | included |
| **オブジェクトID**<br>コンテンツを一意に識別するID                    | `$.object.id` | included |

### 4.3.3　オブジェクトの作成

#### 4.3.3.1　基本仕様

- コンテンツ内でテキストや図形を作成したことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/group-lst/object-created |
| :-------- | :-------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0          |
| prefLabel | オブジェクトの作成                                         |

- 判定条件

| verb               | https://w3id.org/xapi/scrapbook/verbs/created |
| :----------------- | :-------------------------------------------- |
| objectActivityType | http://id.tincanapi.com/activitytype/slide    |

#### 4.3.3.2　記述規則（Rules）

1. $.object.definition.extensions['https://w3id.org/japan-xapi/extensions/scrapbook-item-type']
   1. recommended
   2. 作成されたオブジェクトの種類（text, shape等） (Core Profile参照)

#### 4.3.3.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                      | Location (JSONPath)                                                                            | Presence    |
| :---------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------- | :---------- |
| **オブジェクト種類**<br>作成されたオブジェクトの種類（text, shape等）。 | `$.object.definition.extensions['https://w3id.org/japan-xapi/extensions/scrapbook-item-type']` | recommended |

### 4.3.4　議論スレッドの作成

#### 4.3.4.1　基本仕様

- 議論のためのスレッドを作成したことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/group-lst/discussion-created |
| :-------- | :-------------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0              |
| prefLabel | 議論スレッドの作成                                             |

- 判定条件

| verb               | http://activitystrea.ms/create                  |
| :----------------- | :---------------------------------------------- |
| objectActivityType | http://id.tincanapi.com/activitytype/discussion |

#### 4.3.4.2　記述規則（Rules）

なし。共通記述規則に準拠する。

#### 4.3.4.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                   | Location (JSONPath) | Presence |
| :------------------------------------------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)**<br>created                                    | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ**<br>Discussion等のスレッド        | `$.object.objectType` | included |
| **オブジェクトID**<br>スレッドを一意に識別するID                      | `$.object.id` | included |

### 4.3.5　スレッドへの書き込み

#### 4.3.5.1　基本仕様

- スレッドに対してコメント・返信を行ったことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/group-lst/discussion-replied |
| :-------- | :------------------------------------------------------------------ |
| inScheme  | https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0              |
| prefLabel | スレッドへの書き込み                                           |

- 判定条件

| verb               | http://id.tincanapi.com/verb/replied            |
| :----------------- | :---------------------------------------------- |
| objectActivityType | http://id.tincanapi.com/activitytype/discussion |

#### 4.3.5.2　記述規則（Rules）

なし。共通記述規則に準拠する。

#### 4.3.5.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                   | Location (JSONPath) | Presence |
| :------------------------------------------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)**<br>replied                                    | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ**<br>Discussion等のスレッド        | `$.object.objectType` | included |
| **オブジェクトID**<br>スレッドを一意に識別するID                      | `$.object.id` | included |

### 4.3.6　スタンプ送信

#### 4.3.6.1　基本仕様

- 「いいね」等のスタンプを送信したことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/group-lst/stamp-voted |
| :-------- | :--------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/group-lst/v1.0.0       |
| prefLabel | スタンプ送信                                            |

- 判定条件

| verb               | http://id.tincanapi.com/verb/voted-up       |
| :----------------- | :----------------------------------------- |
| objectActivityType | http://id.tincanapi.com/activitytype/comment |

#### 4.3.6.2　記述規則（Rules）

なし。共通記述規則に準拠する。

#### 4.3.6.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                                   | Location (JSONPath) | Presence |
| :------------------------------------------------------------------- | :------------------ | :------- |
| **動詞の表示名(英語)**<br>voted-up                                   | `$.verb.display.en` | included |
| **オブジェクトのオブジェクトタイプ**<br>Comment等のコンテンツ         | `$.object.objectType` | included |
| **オブジェクトID**<br>コンテンツを一意に識別するID                    | `$.object.id` | included |
