# 1.　本プロファイルについて

## 1.1　位置づけ

　本プロファイルは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである電子書籍型デジタル教材（ebook）における学習ログを対象として取りまとめた **xAPI Japan Profiles ebook Profile** 標準仕様である。  
　本仕様は、電子書籍型デジタル教材プラットフォーム上における各種操作や、機能利用の学習ログを体系的に記録するための仕様である。

### 1.1.1　共通方針

　xAPIプロファイルの思想自体は、データ提供者に対して特定の仕様を強制するものではなく、表現の共通化を支えるための枠組みである。本プロファイルにおいても同様のスタンスをとり、各コンテンツ事業者に対して本プロファイルの規定通りの出力を一律に強制するものではない。  
　そのため、本プロファイルは、出力方法の方向性を示す「表現のための資産」として位置づけ、あくまで「推奨」として扱う。  
　したがって、コンテンツの特性に応じて、一部項目を出力しない、あるいは満たさない運用も許容される。また、個別のユースケースにおいて本プロファイルとは著しく異なるデータ構造が必要とされる場合には、本規定に縛られることなく、別のプロファイルが提示・利用されることを拒絶するものではない。  
　なお、本プロファイルは xAPI 1.0.3 をベースとする。これは、現在の学習分析基盤における普及状況と相互運用性を考慮し、既存のLRS（Learning Record Store）等との円滑なデータ連携を確実にするための選定である。
　学習eポータルと連携する場合は、システム間の相互運用性を確保する観点から、「初等中等教育におけるシステム間連携のための相互運用標準モデル Version 5.00」も参照する。

## 1.2　目的

　本プロファイルは、電子書籍型デジタル教材（ebook）における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、ebook Profileとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本プロファイルにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造・考え方に準拠して記載する。  
　本仕様書の記述は、特定の製品仕様に制約されないデータ記述の標準化を目指し、「抽象化された学習ツール」を想定して策定している。特定の既存システムへの準拠ではなく、汎用的な標準仕様を定義することで、広範な学習ツールへの適用を可能にしている。実際のシステム実装において本仕様との差異が生じる際は、本仕様を共通の基点とした上で、各システム特有のスタディ・ログ仕様を補足するプロファイルが別途定義されることも考えらえる。
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

## 2.3　記述規則の記載方針

　本プロファイルでは、xAPI Profile Specification および xAPI-Specで規定されている内容と同一の項目は重複して記載しない。
　各StatementTemplateでは、ebook Profileとして個別に明示する必要がある項目のみを、当該Templateの記述規則（Rules）に記載する。

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
| startPosition | `https://w3id.org/xapi-japan-profiles/ebook/extensions/startPosition` | ContextExtension | `type: string` | 学習行動の起点となる位置情報を表す。 |
| endPosition | `https://w3id.org/xapi-japan-profiles/ebook/extensions/endPosition` | ResultExtension | `type: string` | 学習行動が終了した位置情報を表す。 |
| navigationMethod | `https://w3id.org/xapi-japan-profiles/ebook/extensions/navigationMethod` | ResultExtension | `type: string, enum: ["paging", "index"]` | ページ移動や目次遷移などの移動方法を表す。 |
| contentPosition | `https://w3id.org/xapi-japan-profiles/ebook/extensions/contentPosition` | ResultExtension | `type: string` | コンテンツ内の範囲情報を表す。 |
| annotationTool | `https://w3id.org/xapi-japan-profiles/ebook/extensions/annotationTool` | ContextExtension | `type: string, enum: ["freehand", "straightline", "textinput"]` | 注釈作成に用いたツール種別を表す。 |
| targetLocation | `https://w3id.org/xapi-japan-profiles/ebook/extensions/targetLocation` | ResultExtension | `type: string` | 学習行動対象の矩形座標を表す。 |

# 4.　電子書籍（ebook）における学習行動

## 4.1　本章の位置づけ

　本章では、電子書籍（ebook）における学習活動の特性を述べ、本プロファイルで定義するStatementTemplateの背景にある考え方を示す。

## 4.2　電子書籍型デジタル教材プラットフォームの特性と主な学習行動

　電子書籍型デジタル教材プラットフォームは、デジタル教材を通じ、学習者の学習行動をきめ細かく記録する環境を提供する。
　本プロファイルは、電子書籍の標準的なUIとして一般的に備わる機能を起点とし、実装間で比較的共通化しやすい操作に対象を限定して標準仕様を策定する。

主な学習活動の例：

- **プラットフォーム関連操作**：プラットフォームの起動、終了
- **紙面表示関連操作**：紙面の表示、非表示
- **ページ遷移操作**：ページ送り、戻り、特定ページへの遷移を含むページ移動
- **注釈機能**：しおり・ブックマーク作成、書き込み作成
- **削除操作**：注釈やしおり等の削除

## 4.3　本プロジェクトの成果と今後の課題

**本プロジェクトの成果**

- 本プロファイルでは、電子書籍型デジタル教材における標準的なUI操作を対象として、プラットフォームの起動・終了、紙面の表示・非表示、ページ移動、しおり・ブックマーク作成、書き込み作成、削除といった基本的な操作ログを記録するStatementTemplateを定義した。これにより、学習者が教材をどのように閲覧し、注釈機能をどのように利用したかを共通的に把握でき、学習行動の可視化、個別支援、教材改善等に活用できる。一方で、本版では標準的な閲覧UIにおいて広く見られる操作に対象を限定しており、学習体験の解釈に追加の合意を要する機能やVerbは対象外としている。

**今後の課題**

- **周辺機能の拡張**：検索機能、辞書連携、音声読み上げ、外部リンク遷移など、電子書籍型デジタル教材プラットフォームで実装差が大きい周辺機能について、実装実態を踏まえた上で順次スコープ化を検討する。
- **学習完了（completed）の定義**：電子書籍型デジタル教材における「完了」は、読本、ドリル、副読本等のコンテンツ特性によって判定基準が大きく異なるため、本バージョンではスコープ外とした。今後、各プラットフォームの実装事例を収集・分析し、共通定義と判定基準の策定を行う必要がある。
- **読書行動（read）の定義と標準化**：学習体験の本質的な把握に寄与するVerbとして `read` の採用を検討したが、現時点では共通定義および技術的整合性の確保には至らず、本バージョンでは定義対象外とした。今後は各事業者の判定ロジックを収集し、算出困難となる技術的・運用的なボトルネックを可視化した上で、準拠可能な共通判定ロジックを検討する。

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
    - presence：included（必須）、recommended（推奨）、optional（任意）とする。なお、xAPIのJSON-LD表現においては、presence: "optional" という値は公式にはサポートされていない。JSON-LD形式でプロファイルを記述する場合、presenceプロパティを省略した場合は「任意（optional）」として扱う。そのため、included（必須）およびrecommended（推奨）の場合のみ presence を明記し、optional（任意）の場合は presence プロパティを省略する運用とする。本プロファイルもこの方針に従う。
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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 開始した電子書籍型デジタル教材プラットフォームのURIを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | 電子書籍型デジタル教材プラットフォームが起動した日時を設定 |

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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 終了した電子書籍型デジタル教材プラットフォームのURIを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | 電子書籍型デジタル教材プラットフォームが終了した日時を設定 |

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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 表示された紙面のURIを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | 紙面が表示された日時を設定 |

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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 表示を終了した紙面のURIを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | 紙面が非表示された日時を設定 |

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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | ページ移動先の要素のURIを設定 |
| **移動開始位置** | `$.context.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/startPosition']` | recommended | ページ移動の起点となった位置情報を設定。目次からの移動の場合は、目次を開く直前の位置情報を設定 |
| **移動方法** | `$.result.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/navigationMethod']` | recommended | ページ移動の操作方法を設定。例：ボタン操作（button）、目次（toc） |
| **タイムスタンプ** | `$.timestamp` | recommended | ページ移動が行われた日時を設定 |

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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 作成されたしおり・ブックマーク自体のURIを設定 |
| **親アクティビティ** | `$.context.activities.parent` | included | しおり・ブックマークが設定された対象（ページ等）のURIを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | しおり・ブックマーク作成が行われた日時を設定 |

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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 作成された書き込みを一意に識別するURIを設定 |
| **親アクティビティ** | `$.context.activities.parent` | included | 書き込みが行われた対象要素（ページ等）のURIを設定 |
| **注釈ツール種別** | `$.context.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/annotationTool']` | included | 使用された注釈ツールの種別を設定 |
| **目標位置** | `$.result.extensions['https://w3id.org/xapi-japan-profiles/ebook/extensions/targetLocation']` | recommended | ページ内の具体的な書き込み座標や範囲情報などを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | 書き込み作成が行われた日時を設定 |

### 5.3.8　削除

#### 5.3.8.1　基本仕様

- 電子書籍型デジタル教材の表示ページにおいて、書き込み内容や図形、しおり・ブックマーク等の注釈を削除したことを記録するためのテンプレート。
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

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **オブジェクトID** | `$.object.id` | included | 削除対象の要素のURIを設定。object.idがページ等の範囲および注釈・描画・しおり・ブックマーク等の種別を示す場合は、対象範囲の指定された全てまたは個別の種別を対象とした一括削除となる。object.idが注釈・描画・しおり・ブックマーク等の個別の注釈を示す場合は、その対象物の削除となる |
| **親アクティビティ** | `$.context.activities.parent` | included | 削除が行われた対象要素（ページ等）のURIを設定 |
| **タイムスタンプ** | `$.timestamp` | recommended | 削除が行われた日時を設定 |
