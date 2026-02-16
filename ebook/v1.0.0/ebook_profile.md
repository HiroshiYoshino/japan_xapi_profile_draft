# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである電子書籍（ebook）における学習ログを対象として取りまとめたebook xAPIプロファイル標準仕様（案）である。  
　本仕様は、文部科学省が令和5年3月に策定した「デジタル教科書標準仕様書」に記載されている「別紙3 プラットフォーム機能一覧」を踏まえ、電子書籍プラットフォーム上で発生する操作、読書行動、注釈および表示設定の変更等に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、電子書籍（ebook）における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、ebook xAPIプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateで使用される語彙（Verb、ActivityType、Extension等）は以下のいずれかに整理される。(1) SWG独自に定義した語彙を使用する場合、Core Profile内のConceptsに定義されている。(2) ADLや他の標準で定義済みの語彙を使用する場合、それらを直接参照し、Domain Profileで再定義しない。Domain Profile（本プロファイルはDomain Profileの1つ）としてeBook Profileは Statement Templateおよび Rules の定義に集中し、語彙定義はCore Profileに委譲する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、電子書籍（ebook）における学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

* idに期待されるURI    
  * 省略理由：idはStatementTemplateをグローバルに一意に識別するためのURI を指定する項目であり、プロファイルの公開形態、管理主体、バージョニング方針が確定した段階で設計されるべきものである。本ドキュメントは標準仕様（案）としての整理および合意形成を目的としているため、現時点では具体的なURIの定義は行わない。  
* typeに期待される固定値StatementTemplate    
  * 省略理由：typeに指定される固定値StatementTemplateは、JSON-LD形式における機械可読性を担保するための項目である。本ドキュメントでは、読み手による理解を前提とした仕様書として、StatementTemplateの構造および位置づけを章構成および見出しによって明示しているため、当該項目は省略する。
* inSchemeに期待されるURI   
  * 省略理由：inSchemeは、当該StatementTemplateが属するプロファイルおよびバージョンをURIにより示すための項目である。本ドキュメントでは、プロファイルの名称およびバージョン管理を文書構成および章立てにより管理していることから、inSchemeによる明示的な指定は行わない  
* prefLabel    
  * 省略理由：prefLabelはStatementTemplateに対する人可読な名称を付与するための項目である。本ドキュメントでは、各ユースケースを章・節の見出し（項目名）として明示しており、これをもって当該StatementTemplateを識別可能とするため、prefLabel の記載は省略する。  

　なお、これらの項目については、将来的にプロファイルの登録や機械可読な形式での提供が必要となる場合に、改めて検討することとする。

## 1.4　定義範囲

　本ドキュメントは、Japan xAPI eBook Profileを構成する要素のうち、メタ情報、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、電子書籍（ebook）の閲覧行動が非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本ドキュメントの構成について

　本紙は、xAPIプロファイル仕様に基づき、eBook学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

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
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/ebook`          |
| **type**                 | オブジェクトタイプ                     | `Profile`                                             |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                  |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI eBook Profile                              |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                               |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                            |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育における電子書籍学習ログのプロファイル |
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

# 3.　電子書籍（ebook）における読書行動

　本章では、電子書籍（ebook）における読書活動の特性を述べ、本プロファイルで定義するStatementTemplateの背景にある考え方を示す。

## 3.1　電子書籍プラットフォームの特性

　電子書籍プラットフォームは、デジタル教科書環境において学習者の読書行動をきめ細かく記録する環境を提供する。本プロファイルは、以下の操作行動および読書行為を記録対象とする。

**プラットフォーム関連操作：**
- 起動・終了

**コンテンツ表示関連操作：**
- コンテンツの利用開始・終了、表示・非表示

**読書行為：**
- ページ移動、読書（滞在）、目次操作

**表示形式・設定操作：**
- 画面向き、レイアウト、ズーム、色設定の変更

**注釈機能：**
- しおり、ハイライト、ペン・線分書き込み、削除操作

## 3.2　学習ログ記録の目的

　電子書籍プラットフォームにおいて記録される学習ログは、以下の目的で活用される。

- **学習行動の可視化**：学習者がどのように教材を利用したかを把握
- **学習支援**：学習者の読書パターンに基づいた個別指導
- **教育効果の測定**：電子書籍機能の利用と学習成果の関連性分析
- **プラットフォーム改善**：利用状況に基づいたUI/UX改善

## 3.3　本プロジェクトの成果と今後の課題

**本プロジェクトの成果**

- 本プロファイルでは、電子書籍プラットフォーム上で発生するプラットフォーム関連操作（起動・終了）、コンテンツ表示関連操作（ページ移動、目次移動）、読書行為（読書時間の記録）、注釈機能（しおり、ハイライト等）を体系的に記録するStatementTemplateを定義した。これにより、学習者の読書行動をきめ細かく追跡し、学習支援やプラットフォーム改善に活用することが可能になる。一方で、電子書籍の閲覧行動は極めて非線形であり、特定の「正解ルート」が存在しないため、行動パターンの定義（xAPI Patterns）は今回対象外とした。

**今後の課題（作業中）**

- **生体情報との連携**：視線追跡やアイトラッキングなど、学習者の生理的反応を含めた読書行動分析への対応。
- **注釈情報の構造化**：ハイライトやしおり、書き込みなどの注釈データについて、意味的な関連性を分析するための構造化。
- **複合学習シーンの対応**：オンライン学習時のビデオ再生や外部リソースへのアクセスなど、電子書籍以外の学習活動との統合記録。
- **読む能力の診断**：読書速度や停止時間などから、読む能力の発達段階を診断するメタデータの標準化。

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、eBook Profileにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

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

### 4.3.1　プラットフォームの起動

#### 4.3.1.1　基本仕様

* 電子書籍プラットフォームがシステムとして起動されたことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/viewer-launched |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | プラットフォームの起動                       |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/launched               |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/viewer     |

#### 4.3.1.2　記述規則（Rules）

| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **プラットフォームID** |      | `$.object.id` | included |
| **起動理由** |      | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/launchReason']` | recommended |

### 4.3.2　プラットフォームの終了

#### 4.3.2.1　基本仕様

* 電子書籍プラットフォームの利用が終了したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/viewer-terminated |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | プラットフォームの終了                       |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/terminated             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/viewer     |

#### 4.3.2.2　記述規則（Rules）

| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **プラットフォームID** |      | `$.object.id` | included |
| **終了理由** |      | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/terminationReason']` | recommended |

### 4.3.3　コンテンツの利用開始

#### 4.3.3.1　基本仕様

* 電子書籍コンテンツを利用開始したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/content-opened |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | コンテンツの利用開始                         |

| 項目              | 値                                        |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/open   |
| objectActivityType | http://activitystrea.ms/schema/1.0/book   |

#### 4.3.3.2　記述規則（Rules）

| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** |      | `$.object.id` | included |

### 4.3.4　コンテンツの利用終了

#### 4.3.4.1　基本仕様

* 電子書籍コンテンツの表示を終了したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/content-closed |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | コンテンツの利用終了                         |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/close   |
| objectActivityType | http://activitystrea.ms/schema/1.0/book    |

#### 4.3.4.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 表示終了したコンテンツのIDまたはURL | `$.object.id` | included |
| **経過時間** | 表示開始から終了までの総経過時間（ISO 8601） | `$.result.duration` | included |
| **終了位置** | 終了時のページ番号または位置情報 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/endPosition']` | recommended |

### 4.3.5　コンテンツの表示

#### 4.3.5.1　基本仕様

* 電子書籍コンテンツが画面上に表示可能になったことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/content-rendered |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | コンテンツの表示                             |

#### 4.3.5.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 表示されたコンテンツのIDまたはURL | `$.object.id` | included |

### 4.3.6　コンテンツの非表示

#### 4.3.6.1　基本仕様

* 表示されていたコンテンツが非表示になったことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/content-hidden |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | コンテンツの非表示                           |

#### 4.3.6.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 非表示になったコンテンツのIDまたはURL | `$.object.id` | included |

### 4.3.7　読書行動

#### 4.3.7.1　基本仕様

* 学習者がコンテンツ内の特定箇所で意識的な読み取りを行ったことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/reading-paged |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 読書行動                                     |

| 項目              | 値                                        |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/read   |
| objectActivityType | http://activitystrea.ms/schema/1.0/book   |

#### 4.3.7.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 読書対象のコンテンツID | `$.object.id` | included |
| **滞在時間** | 滞在時間（ISO 8601 Duration） | `$.result.duration` | included |
| **開始位置** | 読書開始時点のページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/startPosition']` | recommended |
| **終了位置** | 読書終了時点のページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/endPosition']` | recommended |

### 4.3.8　ページ移動

#### 4.3.8.1　基本仕様

* 学習者がページ移動したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/progressed-page |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | ページ移動                                   |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/progressed  |
| objectActivityType | http://activitystrea.ms/schema/1.0/page    |

#### 4.3.8.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | ページ移動が行われたコンテンツID | `$.object.id` | included |
| **移動元位置** | ページ移動の起点となったページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/startPosition']` | recommended |
| **移動先位置** | ページ移動の到達点となったページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/endPosition']` | included |
| **ナビゲーション方法** | ページ移動の操作方法（"flick"、"button"、"toc" など） | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/navigationMethod']` | recommended |

### 4.3.9　目次移動

#### 4.3.9.1　基本仕様

* 目次を使用して特定位置へ移動したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/navigation-toc |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 目次移動                                     |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/progressed  |
| objectActivityType | http://activitystrea.ms/schema/1.0/page    |

#### 4.3.9.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 目次選択により移動したコンテンツID | `$.object.id` | included |
| **移動先位置** | 移動先のページ番号または位置情報 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/endPosition']` | included |

### 4.3.10　縦ローリング

#### 4.3.10.1　基本仕様

* 表示レイアウトを縦置き1ページ表示へ変更したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/layout-portrait |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 縦ローリング                                 |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.10.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **プラットフォームID** | プラットフォームを識別するIRIまたはURL | `$.object.id` | included |
| **画面向き** | 画面向き："portrait" | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/displayOrientation']` | included |

### 4.3.11　横ローリング

#### 4.3.11.1　基本仕様

* 表示レイアウトを横置き見開き表示へ変更したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/layout-landscape |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 横ローリング                                 |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.11.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **プラットフォームID** | プラットフォームを識別するIRIまたはURL | `$.object.id` | included |
| **画面向き** | 画面向き："landscape" | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/displayOrientation']` | included |

### 4.3.12　リフロー遷移

#### 4.3.12.1　基本仕様

* リフロー画面（テキスト折り返し表示）を使用したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/reflow-engaged |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | リフロー遷移                                 |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.12.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **プラットフォーム/コンテンツID** | プラットフォームまたはコンテンツページのID | `$.object.id` | included |
| **文字サイズ** | リフロー表示での文字サイズ | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/fontSize']` | recommended |
| **行間** | リフロー表示での行間 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/lineSpacing']` | recommended |

### 4.3.13　しおり追加

#### 4.3.13.1　基本仕様

* 特定箇所にしおりを追加したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/bookmark-added |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | しおり追加                                   |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | https://w3id.org/xapi/adb/verbs/bookmarked |
| objectActivityType | http://activitystrea.ms/schema/1.0/bookmark |

#### 4.3.13.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | ブックマーク対象のコンテンツID | `$.object.id` | included |
| **ページ番号** | ブックマークを追加したページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **ブックマークID** | ブックマークをアプリ内で一意に識別するID | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/bookmarkId']` | recommended |

### 4.3.14　しおり削除

#### 4.3.14.1　基本仕様

* 既存のしおりを削除したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/bookmark-removed |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | しおり削除                                   |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/delete  |
| objectActivityType | http://activitystrea.ms/schema/1.0/bookmark |

#### 4.3.14.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 削除対象のブックマークが紐づくコンテンツID | `$.object.id` | included |
| **ブックマークID** | 削除対象のブックマークID | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/bookmarkId']` | included |
| **ページ番号** | しおりが紐づいていたページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | recommended |

### 4.3.15　ペン書き込み

#### 4.3.15.1　基本仕様

* ペン機能で手書き線・文字を書き込んだことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/pen-annotation |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | ペン書き込み                                 |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | https://w3id.org/xapi/adb/verbs/noted      |
| objectActivityType | http://activitystrea.ms/schema/1.0/note   |

#### 4.3.15.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | ペン書き込みが行われたコンテンツID | `$.object.id` | included |
| **ツール種別** | 使用されたツール種別 ("pen" など) | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/annotationTool']` | included |
| **ページ番号** | 書き込みが行われたページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **位置情報** | ページ内の書き込み位置情報 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/targetLocation']` | recommended |

### 4.3.16　ペン書き込み削除

#### 4.3.16.1　基本仕様

* ペン書き込みを削除したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/pen-annotation-removed |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | ペン書き込み削除                             |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/delete  |
| objectActivityType | http://activitystrea.ms/schema/1.0/note    |

#### 4.3.16.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 削除対象の書き込みが紐づくコンテンツID | `$.object.id` | included |
| **ツール種別** | 削除対象のツール種別 ("pen" など) | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/annotationTool']` | included |
| **ページ番号** | 削除対象の書き込みがあったページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | recommended |
| **位置情報** | 削除対象の書き込み位置情報 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/targetLocation']` | recommended |

### 4.3.17　線分書き込み

#### 4.3.17.1　基本仕様

* 線分書き込み機能で線を書き込んだことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/line-annotation |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 線分書き込み                                 |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | https://w3id.org/xapi/adb/verbs/noted      |
| objectActivityType | http://activitystrea.ms/schema/1.0/note    |

#### 4.3.17.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 書き込みが行われたコンテンツID | `$.object.id` | included |
| **ツール種別** | 使用されたツール種別 ("line" など) | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/annotationTool']` | included |
| **ページ番号** | 線分が描画されたページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **位置情報** | 線分の描画位置情報（始点・終点座標など） | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/targetLocation']` | recommended |

### 4.3.18　線分書き込み削除

#### 4.3.18.1　基本仕様

* 線分書き込みを削除したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/line-annotation-removed |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 線分書き込み削除                             |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/delete  |
| objectActivityType | http://activitystrea.ms/schema/1.0/note    |

#### 4.3.18.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 削除対象の書き込みが紐づくコンテンツID | `$.object.id` | included |
| **ツール種別** | 削除対象のツール種別 ("line" など) | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/annotationTool']` | included |
| **ページ番号** | 削除対象があったページ番号 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **位置情報** | 削除対象の描画位置情報 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/targetLocation']` | recommended |

### 4.3.19　一括削除

#### 4.3.19.1　基本仕様

* 全ての書き込みを一括削除したことを記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/all-annotations-cleared |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 一括削除                                     |

| 項目              | 値                                         |
| :---------------- | :----------------------------------------- |
| verb              | http://activitystrea.ms/schema/1.0/delete  |
| objectActivityType | http://activitystrea.ms/schema/1.0/note    |

#### 4.3.19.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 一括削除対象となったコンテンツID | `$.object.id` | included |
| **ページ番号** | 削除対象があったページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |

### 4.3.20　拡大

#### 4.3.20.1　基本仕様

* 表示倍率の拡大を記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/zoom-in |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 拡大                                         |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.20.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 操作が行われたコンテンツID | `$.object.id` | included |
| **ページ番号** | 拡大操作時の表示ページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **ズームレベル** | 拡大後のズームレベル | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/zoomLevel']` | included |

### 4.3.21　縮小

#### 4.3.21.1　基本仕様

* 表示倍率の縮小を記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/zoom-out |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 縮小                                         |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.21.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 操作が行われたコンテンツID | `$.object.id` | included |
| **ページ番号** | 縮小操作時の表示ページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **ズームレベル** | 縮小後のズームレベル | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/zoomLevel']` | included |

### 4.3.22　背景色の変更

#### 4.3.22.1　基本仕様

* 背景色変更を記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/background-color-changed |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 背景色の変更                                 |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.22.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 変更が行われたコンテンツID | `$.object.id` | included |
| **ページ番号** | 変更時の表示ページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **背景色** | 変更後の背景色 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/backgroundColor']` | included |

### 4.3.23　文字色の変更

#### 4.3.23.1　基本仕様

* 文字色変更を記録するためのテンプレート。

| 項目     | 値                                             |
| :------- | :--------------------------------------------- |
| id       | https://w3id.org/xapi/ebook/templates/font-color-changed |
| inScheme | https://w3id.org/xapi/ebook/v1                 |
| prefLabel | 文字色の変更                                 |

| 項目              | 値                                                      |
| :---------------- | :---------------------------------------------------- |
| verb              | http://adlnet.gov/expapi/verbs/interacted             |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/settings   |

#### 4.3.23.2　記述規則（Rules）
| 項目     | 説明 | Location | Presence |
| :------- | :--- | :--- | :--- |
| **コンテンツID** | 変更が行われたコンテンツID | `$.object.id` | included |
| **ページ番号** | 変更時の表示ページ番号 | `$.context.extensions['https://w3id.org/xapi/ebook/extensions/pageNumber']` | included |
| **文字色** | 変更後の文字色 | `$.result.extensions['https://w3id.org/xapi/ebook/extensions/fontColor']` | included |
