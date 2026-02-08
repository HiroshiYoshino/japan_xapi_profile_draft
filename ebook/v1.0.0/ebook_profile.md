# 1.　本ドキュメントについて

## 1.1　位置づけ

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである電子書籍TFにおける学習ログを対象として取りまとめた **Japan xAPI eBook Profile** 標準仕様（案）である。  
　本仕様は、電子書籍分野に記載されている特性を踏まえ、電子書籍ビューア上で発生する閲覧操作や書き込み等に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的

　本ドキュメントは、電子書籍における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、eBookプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本ドキュメントに記載されるStatementTemplateのうち独自に定義したものについては、coreプロファイル内のconceptに記載している。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、電子書籍における学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

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

　本ドキュメントは、Japan xAPI eBook Profileを構成する要素のうち、メタ情報、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、電子書籍閲覧が非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本ドキュメントの構成について

　本紙は、xAPIプロファイル仕様に基づき、電子書籍学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                     | 説明                                   | 値                                                         |
| :----------------------- | :------------------------------------- | :--------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/japan-xapi/profiles/ebook`               |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                  |
| **conformsTo**           | 準拠するxAPI Profile仕様               | `https://w3id.org/xapi/profiles#1.0`                       |
| プロファイル名 prefLabel | プロファイルを識別する名称             | Japan xAPI eBook Profile                                   |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                     |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                    |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                 |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                     |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育における電子書籍学習ログ標準プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                 |

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

# 3. 電子書籍利用に関するユースケース

電子書籍（デジタル教科書・教材）における主なユースケースは、学習者がコンテンツを閲覧し、学習の過程で書き込みやしおり付けなどの操作を行うことである。

主な学習活動の例：

- **コンテンツの閲覧**: デジタル教科書や教材を開き、ページをめくりながら読み進める。
- **重要箇所の記録**: 重要な部分にマーカーを引いたり、メモを書き込んだりする。
- **学習の再開**: しおりを挟んだページから学習を再開する。
- **表示の調整**: 読みやすいように文字サイズを変更したり、拡大縮小を行ったりする。

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、eBookプロファイルにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

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

### 3.3.1　プラットフォームの起動

#### 4.3.1.1　基本仕様

- 電子書籍ビューアがシステムとして起動されたことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/ebook/viewer-launched |
| :-------- | :---------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/ebook/v1.0.0           |
| prefLabel | プラットフォームの起動                                      |

- 判定条件

| verb               | http://adlnet.gov/expapi/verbs/launched                 |
| :----------------- | :------------------------------------------------------ |
| objectActivityType | https://w3id.org/japan-xapi/activity-types/ebook/viewer |

#### 4.3.1.2　記述規則（Rules）

1. $.object.id
   1. included
   2. 開始されたビューアを識別するIRIまたはURLを設定
2. $.context.extensions['https://w3id.org/japan-xapi/extensions/ebook/launch-reason']
   1. recommended
   2. ビューアの起動のきっかけを記録する（user-launch, resume, system-launch等）

#### 4.3.1.3　Markdownテーブル

| 項目説明 (Description / ScopeNote)                           | Location (JSONPath)                                                                  | Presence    |
| :----------------------------------------------------------- | :----------------------------------------------------------------------------------- | :---------- |
| **ビューアID**<br>開始されたビューアを識別するIRIまたはURL。 | `$.object.id`                                                                        | included    |
| **起動理由**<br>例："user-launch", "resume", "system-launch" | `$.context.extensions['https://w3id.org/japan-xapi/extensions/ebook/launch-reason']` | recommended |

### 3.3.2　コンテンツの利用開始

#### 4.3.2.1　基本仕様

- 書籍を開いたことを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/ebook/content-opened |
| :-------- | :--------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/ebook/v1.0.0          |
| prefLabel | コンテンツの利用開始                                       |

- 判定条件

| verb               | http://activitystrea.ms/schema/1.0/open |
| :----------------- | :-------------------------------------- |
| objectActivityType | http://activitystrea.ms/schema/1.0/book |

### 3.3.3　ページ移動 (Progressed)

#### 4.3.3.1　基本仕様

- ページめくり等の移動を記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/ebook/page-progressed |
| :-------- | :---------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/ebook/v1.0.0           |
| prefLabel | ページ移動                                                  |

- 判定条件

| verb               | http://adlnet.gov/expapi/verbs/progressed |
| :----------------- | :---------------------------------------- |
| objectActivityType | http://activitystrea.ms/schema/1.0/page   |

### 3.3.4　設定変更 (Interacted)

#### 3.3.4.1　基本仕様

- 拡大縮小、文字サイズ変更などを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/ebook/settings-interacted |
| :-------- | :-------------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/ebook/v1.0.0               |
| prefLabel | 設定変更                                                        |

- 判定条件

| verb               | http://adlnet.gov/expapi/verbs/interacted                 |
| :----------------- | :-------------------------------------------------------- |
| objectActivityType | https://w3id.org/japan-xapi/activity-types/ebook/settings |

### 3.3.5　注釈・書き込み (Noted)

#### 3.3.5.1　基本仕様

- メモやペンの書き込みを記録するためのテンプレート。
- 識別情報

| id        | https://w3id.org/japan-xapi/templates/ebook/annotation-noted |
| :-------- | :----------------------------------------------------------- |
| inScheme  | https://w3id.org/japan-xapi/profiles/ebook/v1.0.0            |
| prefLabel | 注釈・書き込み                                               |

- 判定条件

| verb               | https://w3id.org/xapi/adb/verbs/noted   |
| :----------------- | :-------------------------------------- |
| objectActivityType | http://activitystrea.ms/schema/1.0/note |
