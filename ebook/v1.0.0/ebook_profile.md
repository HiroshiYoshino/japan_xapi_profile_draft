# 1.　本プロファイルについて

## 1.1　位置づけ

　本プロファイルは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである電子書籍型デジタル教材（ebook）における学習ログを対象として取りまとめた **xAPI Japan Profiles ebook Profile** 標準仕様である。  
　本仕様は、電子書籍型デジタル教材プラットフォーム上における各種操作や、機能利用の学習ログを体系的に記録するための仕様である。

### 1.1.1　共通方針

　本プロファイルは、各コンテンツ事業者に対して本規定どおりの出力を強制するものではない。  
　xAPIプロファイルの思想自体が、そのような強制力を持たせるものではなく、表現の共通化を支えるための枠組みである。  
　本プロファイルは、出力方法の方向性を示す「表現のための資産」として位置づけ、「推奨」として扱う。  
　したがって、本プロファイルに記載された全項目への一律の準拠を求めるものではない。コンテンツの特性に応じて、記載したログを出力しない場合や一部項目を満たさない場合も許容される。  
　なお、本プロファイルは xAPI 1.0.3 をベースとする。  
　学習eポータルと連携する場合は、システム間の相互運用性を確保する観点から、「初等中等教育におけるシステム間連携のための相互運用標準モデル Version 5.00」も参照する。

## 1.2　目的

　本プロファイルは、電子書籍型デジタル教材（ebook）における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、ebook Profileとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本プロファイルにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造・考え方に準拠して記載する。  
　本仕様書の記述は、特定製品を前提とせず、現実的な範囲の「架空ツール」を想定して行う。この前提により、既存システムとの部分的不一致や未確定要素に起因する議論停滞を回避する。  
　本プロファイルに記載される語彙（Verb、ActivityType、Extension等）は、(1) 本プロファイル内のConceptsで定義する語彙、または (2) ADLや他標準で定義済みの語彙を直接参照する語彙として整理する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別記載は行わないものとする。  
　本プロファイルは、電子書籍型デジタル教材（ebook）における学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録段階で主に必要となる項目については、本書の目的に照らし記載を省略する。省略理由は下記に示すとおりである。  

- typeに期待される固定値StatementTemplate    
  - 省略理由：typeに指定される固定値StatementTemplateは、JSON-LD形式における機械可読性を担保するための項目である。本プロファイルでは、読み手による理解を前提とした仕様書として、StatementTemplateの構造および位置づけを章構成および見出しによって明示しているため、当該項目は省略する。  

　なお、この項目については、将来的にプロファイルの登録や機械可読な形式での提供が必要となる場合に、改めて検討することとする。

## 1.4　定義範囲

　本プロファイルは、xAPI Japan Profiles ebook Profileを構成する要素のうち、メタ情報、Concepts、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、電子書籍型デジタル教材（ebook）の閲覧行動が非線形である特性を踏まえ、xAPIプロファイルにおけるPatternsは定義の対象外とする。  
　本プロファイルは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。

## 1.5　本プロファイルの構成について

　本プロファイルは、xAPIプロファイル仕様に基づき、電子書籍型デジタル教材（ebook）学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本プロファイルは、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- Concepts：ActivityType、Extensionsの定義
- 学習行動：電子書籍プラットフォームにおける学習行動の整理
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
| **id**                   | プロファイルIRI                        | `https://w3id.org/xapi-japan-profiles/ebook/v1.0.0`   |
| **type**                 | オブジェクトタイプ                     | `Profile`                                             |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                  |
| プロファイル名 prefLabel | プロファイルを識別する名称             | xAPI Japan Profiles ebook Profile                     |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                               |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                            |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育における電子書籍学習ログのプロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                           |

## 2.3　共通記述規則

　本プロファイルで定義するすべてのStatementTemplateに対して、xAPI Profile Specification および xAPI-Spec に基づき、以下のRulesを適用する。

| 項目                               | Location (JSONPath)                        | Presence    |
| :--------------------------------- | :----------------------------------------- | :---------- |
| **ステートメントID**               | `$.id`                                     | included    |
| **タイムスタンプ**                 | `$.timestamp`                              | recommended |
| **アクター**                       | `$.actor`                                  | included    |
| **アクターのオブジェクトタイプ**   | `$.actor.objectType`                       | included（accountを用いる場合） |
| **アクターのアカウントホームページ** | `$.actor.account.homePage`                 | included（accountを用いる場合） |
| **アクターのアカウント名**         | `$.actor.account.name`                     | included（accountを用いる場合） |
| **動詞の表示名(英語)**             | `$.verb.display.en`                        | included    |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType`                      | included    |
| **オブジェクトID**                 | `$.object.id`                              | included    |
| **オブジェクト定義のタイプ**       | `$.object.definition.type`                 | recommended    |
| **オブジェクト定義の名称(日本語)** | `$.object.definition.name.ja-JP`           | recommended |
| **オブジェクト定義の説明(日本語)** | `$.object.definition.description.ja-JP`    | recommended |
| **コンテキスト**                   | `$.context`                                | included    |

※ Presenceには included / excluded / recommended を用いる。本表には、全StatementTemplateに共通して指定する項目のみを記載する。表に記載していない項目は、各Templateで個別指定がない限り、共通記述規則としては未指定とする。

# 3.　Concepts

## 3.1　本章の位置づけ

　本章では、電子書籍型デジタル教材（ebook）向けxAPIプロファイルにおいて使用されるConceptsを定義する。Conceptsは、StatementTemplateから参照される共通定義であり、単体でxAPI Statementを構成するものではない。
　本プロファイルでは、ADLまたはxAPI Communityにより既に定義されている語彙については、意味的な齟齬がない限りそれらをそのまま利用する。電子書籍型デジタル教材（ebook）特有の対象種別や拡張情報についてのみ、本プロファイル独自の定義を記載する。

## 3.2　対象

　Conceptsの対象は、ActivityType、Extensionsの2項目とする。

## 3.3　ActivityType

### 3.3.1　ActivityTypeの定義

　ActivityTypeは、Statementにおいてobjectとして参照されるActivityが、どのような種類のリソースであるかを示す概念である。

### 3.3.2　電子書籍型デジタル教材（ebook）におけるActivityType一覧

| 名称 | id | 補足 |
| :--- | :--- | :--- |
| viewer | `https://w3id.org/xapi-japan-profiles/ebook/activitytypes/viewer` | プラットフォーム操作 |
| content | `https://w3id.org/xapi-japan-profiles/ebook/activitytypes/content` | 書籍全体または章節 |
| page | `https://w3id.org/xapi-japan-profiles/ebook/activitytypes/page` | 表示ページ単位 |

## 3.4　Extensions

### 3.4.1　Extensionsの定義

　Extensions（拡張）は、xAPI標準データモデルだけでは表現しきれない学習行動の文脈や詳細メタデータを付与するために利用される。

### 3.4.2　電子書籍型デジタル教材（ebook）におけるExtensions一覧

| 名称 | id | type | inlineSchema | 補足 |
| :--- | :--- | :--- | :--- | :--- |
| startPosition | `https://w3id.org/xapi-japan-profiles/ebook/extensions/startPosition` | ContextExtension | `type: string` | ページ移動前の開始位置を表す。 |
| endPosition | `https://w3id.org/xapi-japan-profiles/ebook/extensions/endPosition` | ResultExtension | `type: string` | 操作後の終了位置や読了位置を表す。 |
| navigationMethod | `https://w3id.org/xapi-japan-profiles/ebook/extensions/navigationMethod` | ResultExtension | `type: string, enum: ["paging", "index"]` | ページ移動の操作方法を表す。 |
| contentPosition | `https://w3id.org/xapi-japan-profiles/ebook/extensions/contentPosition` | ResultExtension | `type: string` | コンテンツ内の位置情報を表す。 |
| bookmarkId | `https://w3id.org/xapi-japan-profiles/ebook/extensions/bookmarkId` | ContextExtension | `type: string` | アプリ内で一意なブックマーク識別子を表す。 |
| annotationTool | `https://w3id.org/xapi-japan-profiles/ebook/extensions/annotationTool` | ContextExtension | `type: string, enum: ["freehand", "straightline", "textinput"]` | 注釈作成に用いたツール種別を表す。 |
| targetLocation | `https://w3id.org/xapi-japan-profiles/ebook/extensions/targetLocation` | ResultExtension | `type: string` | 書き込み対象の座標や範囲情報を表す。 |

# 4.　電子書籍（ebook）における読書行動

## 4.1　本章の位置づけ

　本章では、電子書籍（ebook）における読書活動の特性を述べ、本プロファイルで定義するStatementTemplateの背景にある考え方を示す。

## 4.2　電子書籍プラットフォームの特性と主な学習活動

　電子書籍プラットフォームは、デジタル教科書環境において学習者の読書行動をきめ細かく記録する環境を提供する。  
　本プロファイルは、電子書籍の標準的なUIとして一般的に備わる機能を起点とし、実装間で比較的共通化しやすい操作に対象を限定して標準仕様を策定する。

主な学習活動の例：

- **プラットフォーム関連操作**：プラットフォームの起動、終了
- **紙面表示関連操作**：紙面の表示、非表示
- **読書関連操作**：ページ送り、戻り、特定ページへの遷移を含むページ移動
- **注釈機能**：しおり・ブックマーク作成、書き込み作成
- **削除操作**：注釈やしおり等の削除

## 4.3　本プロジェクトの成果と今後の課題

**本プロジェクトの成果**

- 本プロファイルでは、電子書籍型デジタル教材における標準的なUI操作を対象として、プラットフォームの起動・終了、紙面の表示・非表示、ページ移動、しおり・ブックマーク作成、書き込み作成、削除といった基本的な操作ログを記録するStatementTemplateを定義した。これにより、学習者が教材をどのように閲覧し、注釈機能をどのように利用したかを共通的に把握でき、学習行動の可視化、個別支援、教材改善等に活用できる。一方で、本版では標準的な閲覧UIにおいて広く見られる操作に対象を限定しており、学習体験の解釈に追加の合意を要する機能やVerbは対象外としている。

**今後の課題**

- **周辺機能の拡張**：検索機能、辞書連携、音声読み上げ、外部リンク遷移など、電子書籍プラットフォームで実装差が大きい周辺機能について、実装実態を踏まえた上で順次スコープ化を検討する。
- **学習完了（completed）の定義**：電子書籍型デジタル教材における「完了」は、読本、ドリル、副読本等のコンテンツ特性によって判定基準が大きく異なるため、本バージョンではスコープ外とした。今後、各プラットフォームの実装事例を収集・分析し、共通定義と判定基準の策定を行う必要がある。
- **読書行動（read）の定義と標準化**：学習体験の本質的な把握に寄与するVerbとして `read` の採用を検討したが、現時点では共通定義および技術的整合性の確保には至らず、本バージョンでは定義対象外とした。今後は各事業者の判定ロジックを収集し、算出困難となる技術的・運用的なボトルネックを可視化した上で、準拠可能な共通判定ロジックを検討する。
- **コンテンツ特性を踏まえた判定ロジックの整理**：ページ移動や注釈操作の記録だけでは学習成立を十分に表せないケースがあるため、教材種別ごとにどの操作ログを学習解釈へどう結び付けるかについて、今後の拡張方針と合わせて整理する必要がある。

# 5.　StatementTemplate

## 5.1　本章の位置づけ

　本章では、ebook Profileにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

## 5.2　前提条件

- 基本仕様
  - 冒頭にdefinitionの位置づけとして、Templateの目的やどのような操作を記録するためのものかを定義する。
  - 識別情報
    - Templateを管理上特定するための情報として3要素（id,inScheme,prefLabel）を含む。
  - 判定条件
    - 受信したStatementがどのTemplateに該当するかを自動判別するための固定値（Verb,objectActivityType）を示す。
- 記述規則（Rules）
  - Statement内の各プロパティに対する制約を示す。以下の要素を含む。
    - データの所在（location）: JSONPath方式で記述されるデータの位置。
    - presence：included（必須）、recommended（推奨）、または未指定（任意）とする。
    - ScopeNoteの内容に基づいた値の定義や運用上の注意点。
- Markdownテーブルの構成
  - 各Templateの末尾には、システム設計・実装時に参照しやすいよう、記述規則（Rules）を一覧化したテーブルを配置する。

## 5.3　StatementTemplate一覧

### 5.3.1　プラットフォームの起動

#### 5.3.1.1　基本仕様

- 電子書籍型デジタル教材プラットフォームがシステムとして起動されたことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/launched |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | プラットフォームの起動 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | http://adlnet.gov/expapi/verbs/launched |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/viewer |

#### 5.3.1.2　記述規則（Rules）

共通記述規則に準拠する。

### 5.3.2　プラットフォームの終了

#### 5.3.2.1　基本仕様

- 電子書籍型デジタル教材プラットフォームの利用が終了したことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/terminated |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | プラットフォームの終了 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | http://adlnet.gov/expapi/verbs/terminated |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/viewer |

#### 5.3.2.2　記述規則（Rules）

共通記述規則に準拠する。

### 5.3.3　紙面の表示

#### 5.3.3.1　基本仕様

- 紙面が画面上に表示され、学習者が閲覧可能な状態になったことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/opened |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | 紙面の表示 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | http://activitystrea.ms/open |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/content |

#### 5.3.3.2　記述規則（Rules）

共通記述規則に準拠する。

### 5.3.4　紙面の非表示

#### 5.3.4.1　基本仕様

- 紙面の表示を終了・閉じたことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/closed |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | 紙面の非表示 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | http://activitystrea.ms/close |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/content |

#### 5.3.4.2　記述規則（Rules）

共通記述規則に準拠する。

### 5.3.5　ページ移動

#### 5.3.5.1　基本仕様

- 電子書籍型デジタル教材内でページ移動（遷移）を行い、新たな紙面を表示したことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/viewed |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | ページ移動 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | http://id.tincanapi.com/verb/viewed |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/page |

#### 5.3.5.2　記述規則（Rules）

| 項目 | 説明 | Location | Presence |
| :--- | :--- | :--- | :--- |
| **移動開始位置** | ページ移動の起点位置 | `$.context.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/startPosition']` | recommended |
| **移動方法** | ページ移動の操作方法（`paging`/`index`） | `$.result.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/navigationMethod']` | recommended |

### 5.3.6　しおり・ブックマーク作成

#### 5.3.6.1　基本仕様

- 電子書籍型デジタル教材内の特定箇所にしおり・ブックマークを作成したことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/bookmarked |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | しおり・ブックマーク作成 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | https://w3id.org/xapi/adb/verbs/bookmarked |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/page |

#### 5.3.6.2　記述規則（Rules）

| 項目 | 説明 | Location | Presence |
| :--- | :--- | :--- | :--- |
| **ブックマークID** | アプリ内で一意な識別ID | `$.context.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/bookmarkId']` | recommended |

### 5.3.7　書き込み作成

#### 5.3.7.1　基本仕様

- 電子書籍型デジタル教材紙面の座標情報に、線分・手書き線・文字情報を書き込む操作を記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/annotated |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | 書き込み作成 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | https://w3id.org/xapi/adb/verbs/annotated |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/page |

#### 5.3.7.2　記述規則（Rules）

| 項目 | 説明 | Location | Presence |
| :--- | :--- | :--- | :--- |
| **注釈ツール種別** | 使用した注釈ツール種別 | `$.context.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/annotationTool']` | included |
| **目標位置** | 書き込み座標や範囲情報 | `$.result.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/targetLocation']` | recommended |

### 5.3.8　削除

#### 5.3.8.1　基本仕様

- 電子書籍型デジタル教材の表示ページにおいて、書き込み内容や図形、しおり等を削除したことを記録するためのテンプレート。
- 識別情報

| 項目      | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/ebook/templates/v1.0.0/delete |
| inScheme | https://w3id.org/xapi-japan-profiles/ebook/v1.0.0 |
| prefLabel | 削除 |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | http://activitystrea.ms/delete |
| objectActivityType | https://w3id.org/xapi-japan-profiles/ebook/activitytypes/page |

#### 5.3.8.2　記述規則（Rules）

共通記述規則に準拠する。
