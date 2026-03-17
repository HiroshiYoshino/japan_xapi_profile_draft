# 1.　本プロファイルについて

## 1.1　位置づけ

　本プロファイルは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるLMS TFにおける学習ログを対象として取りまとめた **xAPI Japan Profiles LMS Profile** 標準仕様である。
　本仕様は、学習管理システム（LMS）分野に記載されている特性を踏まえ、学習課題の配布、提出、評価などのプロセスに関する学習ログを体系的に記録するための仕様である。

### 1.1.1　共通方針

　xAPIプロファイルの思想自体は、データ提供者に対して特定の仕様を強制するものではなく、表現の共通化を支えるための枠組みである。本プロファイルにおいても同様のスタンスをとり、各コンテンツ事業者に対して本プロファイルの規定通りの出力を一律に強制するものではない。
　そのため、本プロファイルは、出力方法の方向性を示す「表現のための資産」として位置づけ、あくまで「推奨」として扱う。
　したがって、コンテンツの特性に応じて、一部項目を出力しない、あるいは満たさない運用も許容される。また、個別のユースケースにおいて本プロファイルとは著しく異なるデータ構造が必要とされる場合には、本規定に縛られることなく、別のプロファイルが提示・利用されることを拒絶するものではない。
　なお、本プロファイルは xAPI 1.0.3 をベースとする。これは、現在の学習分析基盤における普及状況と相互運用性を考慮し、既存のLRS（Learning Record Store）等との円滑なデータ連携を確実にするための選定である。
　学習eポータルと連携する場合は、システム間の相互運用性を確保する観点から、「初等中等教育におけるシステム間連携のための相互運用標準モデル Version 5.00」も参照する。

## 1.2　目的

　本プロファイルは、LMSにおける学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、LMS Profileとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本プロファイルにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造・考え方に準拠して記載する。
　本仕様書の記述は、特定の製品仕様に制約されないデータ記述の標準化を目指し、「抽象化された学習ツール」を想定して策定している。特定の既存システムへの準拠ではなく、汎用的な標準仕様を定義することで、広範な学習ツールへの適用を可能にしている。実際のシステム実装において本仕様との差異が生じる際は、本仕様を共通の基点とした上で、各システム特有のスタディ・ログ仕様を補足するプロファイルが別途定義されることも考えらえる。
　本プロファイルに記載される語彙（Verb、ActivityType、Extension等）は、(1) 本プロファイル内のConceptsで定義する語彙、または (2) ADLや他の標準で定義済みの語彙を直接参照する語彙として整理する。
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。
　本プロファイルは、LMSにおける学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。省略理由は下記に示すとおりである。

- typeに期待される固定値StatementTemplate

  - 省略理由：typeに指定される固定値StatementTemplateは、JSON-LD形式における機械可読性を担保するための項目である。本プロファイルでは、読み手による理解を前提とした仕様書として、StatementTemplateの構造および位置づけを章構成および見出しによって明示しているため、当該項目は省略する。

　なお、この項目については、将来的にプロファイルの登録や機械可読な形式での提供が必要となる場合に、改めて検討することとする。

## 1.4　定義範囲

　本プロファイルは、xAPI Japan Profiles LMS Profileを構成する要素のうち、メタ情報、Concepts、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、LMSにおける学習行動が非線形である特性を踏まえ、xAPIプロファイルにおけるPatternsは定義の対象外とする。
　本プロファイルは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本プロファイルの構成について

　本プロファイルは、xAPIプロファイル仕様に基づき、LMS学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本プロファイルは、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- Concepts：ActivityType、Extensionsの定義
- 学習課題に関するユースケース：LMSにおける学習課題の特性整理
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                | 説明                  | 値                                                 |
| :---------------- | :------------------ | :------------------------------------------------ |
| **id**            | プロファイルIRI           | `https://w3id.org/xapi-japan-profiles/lms/v1.0.0` |
| **type**          | オブジェクトタイプ           | `Profile`                                         |
| **conformsTo**    | 準拠するxAPI Profile仕様  | `https://w3id.org/xapi/profiles#1.0`              |
| プロファイル名 prefLabel | プロファイルを識別する名称       | xAPI Japan Profiles LMS Profile                   |
| バージョン version     | プロファイルの改訂番号やリリース状態  | v1.0.0                                            |
| 作成者/管理者 author    | プロファイルの作成者や責任者      | ICT CONNECT 21 xAPI SWG                           |
| 作成日/更新日 versions  | 文書化日または改訂日          | 2026-04-01                                        |
| 言語 languages      | メタ情報およびプロファイルの記載言語  | 日本語                                               |
| 目的/説明 definition  | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育におけるLMS学習ログのプロファイル                       |
| ドキュメントバージョン       | 文書版数                | 2026年度版                                           |

## 2.3　記述規則の記載方針

　本プロファイルでは、xAPI Profile Specification および xAPI-Specで規定されている内容と同一の項目は重複して記載しない。
　各StatementTemplateでは、LMS Profileとして個別に明示する必要がある項目のみを、当該Templateの記述規則（Rules）に記載する。

# 3.　Concepts

## 3.1　本章の位置づけ

　本章では、LMS Profileにおいて使用する共通語彙（Concepts）を定義する。

## 3.2　対象

　Conceptsの対象は、ActivityType、Extensionsの2項目とする。

## 3.3　ActivityType

### 3.3.1　ActivityTypeの定義

　ActivityTypeは、Statementにおいてobjectとして参照されるActivityが、どのような種類のリソースであるかを示す概念である。また、StatementTemplateのobjectTypeがActivityに指定される際に参照される。

### 3.3.2　LMSにおけるActivityType一覧

| 名称                | id                                                       | 補足   |
| :---------------- | :------------------------------------------------------- | :--- |
| school-assignment | `http://id.tincanapi.com/activitytype/school-assignment` | 学習課題 |

## 3.4　Extensions

### 3.4.1　Extensionsの定義

　Extensions（拡張）は、xAPIの標準データモデルだけでは表現しきれない、学習行動に関する詳細な文脈や具体的なメタデータを付与するために利用される。

### 3.4.2　LMSにおけるExtensions一覧

| 名称       | id                                                             | type              | inlineSchema                                                                                                                                                                                                                                                                                | 補足                                                                                                 |
| :------- | :------------------------------------------------------------- | :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------- |
| modules  | `https://w3id.org/xapi-japan-profiles/lms/extensions/modules`  | ActivityExtension | `type: array, items: { type: object, properties: { id: { type: string, format: "uri" }, name: { type: object, properties: { "ja-JP": { type: string } } }, description: { type: object, properties: { "ja-JP": { type: string } } }, subject: { type: string }, unit: { type: string } } }` | 学習課題を構成する子課題のオブジェクト。各要素は `id`、`name`、`description`、`subject`、`unit` を含み得る。                         |
| due-date | `https://w3id.org/xapi-japan-profiles/lms/extensions/due-date` | ContextExtension  | `type: object, properties: { start: { type: string, format: "date-time" }, end: { type: string, format: "date-time" } }, required: ["start", "end"], additionalProperties: false`                                                                                                           | 配布期間を表すオブジェクト。`start` と `end` を必須とし、日付形式は ISO 8601 に従う。                                            |
| range    | `https://w3id.org/xapi-japan-profiles/lms/extensions/range`    | ContextExtension  | `type: array, items: { type: object, properties: { school: { type: array, items: { type: string } }, grade: { type: array, items: { type: string } }, class: { type: array, items: { type: string } }, student: { type: array, items: { type: string } } } }`                               | 配布対象を表すオブジェクト。`school`、`grade`、`class`、`student` を配列として含み得る。1要素内では `クラス ⊂ 学年` かつ `学年 ⊂ 学校` を満たすこと。 |

# 4.　学習課題に関するユースケース

## 4.1　本章の位置づけ

　本章では、LMSにおける学習課題に関する活動の特性を述べ、本プロファイルで定義するStatementTemplateの背景にある考え方を示す。

## 4.2　学習課題の特性と主な活動

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

## 4.3　本プロジェクトの成果と今後の課題

**本プロジェクトの成果**

- 本プロファイルでは、学習課題の作成、配布、提出、評価といったLMSの基本的なワークフロー、および個々の学習活動への取り組み状況を記録するStatementTemplateを定義した。これにより、教職員が児童生徒に指示した学習課題の実施状況を追跡することが可能になり、学習支援や学習履歴の蓄積に活用できる。一方で、コース学習のような長期間にわたる学習活動や、非線形な学習パス（個別最適な学習における自由進度学習など）の複雑なパターン定義は、今回のバージョンでは対象外としている。

**今後の課題**

- **複雑な学習パスへの対応**：自由進度学習やアダプティブ・ラーニングなど、学習者の進度に応じた個別最適な学習経路を記録・追跡するための拡張。
- **学習成果と学習活動の連動分析**：学習課題の実施状況と最終的な学習成果（テスト成績等）の因果関係を分析するための、メタデータの標準化。
- **協働学習への対応**：グループ学習支援ツールとの連動時に、個人の学習課題とグループ活動を統合的に記録・管理するための仕様。
- **長期にわたる学習データの集約**：複数のCo-Curricularプログラムやキャリア学習など、複数年度かつ複数領域にわたる学習課題の統合的な履歴管理。

# 5.　StatementTemplate

## 5.1　本章の位置づけ

　本章では、LMS Profileにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

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

### 5.3.1　学習課題の作成

#### 5.3.1.1　基本仕様

- 学習課題を作成したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                   |
| :-------- | :------------------------------------------------------------------ |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/created> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                   |
| prefLabel | 学習課題の作成                                                             |

- 判定条件

| 項目   | 値                                         |
| :--- | :---------------------------------------- |
| verb | <https://w3id.org/xapi/adl/verbs/created> |

#### 5.3.1.2　記述規則（Rules）

| 項目      | Location (JSONPath)                                                                    | Presence    | 説明(scopeNote) |
| :------ | :------------------------------------------------------------------------------------- | :---------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |
| **期限日** | `$.context.extensions['https://w3id.org/xapi-japan-profiles/lms/extensions/due-date']` | recommended | 学習課題の実施期限日。ISO 8601形式。 |

### 5.3.2　学習課題の配布

#### 5.3.2.1　基本仕様

- 学習課題を児童生徒に配布したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                  |
| :-------- | :----------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/shared> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                  |
| prefLabel | 学習課題の配布                                                            |

- 判定条件

| 項目   | 値                                       |
| :--- | :-------------------------------------- |
| verb | <http://adlnet.gov/expapi/verbs/shared> |

#### 5.3.2.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |

### 5.3.3　学習課題の実施開始

#### 5.3.3.1　基本仕様

- 学習課題を開始したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                    |
| :-------- | :------------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/launched> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                    |
| prefLabel | 学習課題の実施開始                                                            |

- 判定条件

| 項目   | 値                                         |
| :--- | :---------------------------------------- |
| verb | <http://adlnet.gov/expapi/verbs/launched> |

#### 5.3.3.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |

### 5.3.4　学習課題の完了

#### 5.3.4.1　基本仕様

- 学習課題を完了したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                     |
| :-------- | :-------------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/completed> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                     |
| prefLabel | 学習課題の完了                                                               |

- 判定条件

| 項目   | 値                                          |
| :--- | :----------------------------------------- |
| verb | <http://adlnet.gov/expapi/verbs/completed> |

#### 5.3.4.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |

### 5.3.5　学習課題へのフィードバック

#### 5.3.5.1　基本仕様

- 教職員が児童生徒の学習課題成果にコメントなどのフィードバックを行ったことを表すステートメント。
- 識別情報

| 項目        | 値                                                                     |
| :-------- | :-------------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/responded> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                     |
| prefLabel | 学習課題へのフィードバック                                                         |

- 判定条件

| 項目   | 値                                          |
| :--- | :----------------------------------------- |
| verb | <http://adlnet.gov/expapi/verbs/responded> |

#### 5.3.5.2　記述規則（Rules）

`result.response` および `result.completion` は、本仕様において任意（MAY）の項目であるため、本記述規則による制約を課さない。

| 項目            | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------ | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |
| **フィードバック内容** | `$.result.response`   | optional | 後ろに続く結果オブジェクトに含められる。 |
| **完了フラグ**     | `$.result.completion` | optional | フィードバック後の完了状態 |

### 5.3.6　学習課題を閲覧する

#### 5.3.6.1　基本仕様

- 児童生徒が学習課題を閲覧したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                  |
| :-------- | :----------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/viewed> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                  |
| prefLabel | 学習課題を閲覧する                                                          |

- 判定条件

| 項目   | 値                                     |
| :--- | :------------------------------------ |
| verb | <http://id.tincanapi.com/verb/viewed> |

#### 5.3.6.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |

### 5.3.7　学習課題を異常終了する

#### 5.3.7.1　基本仕様

- 児童生徒が学習課題を異常終了（放棄）したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                     |
| :-------- | :-------------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/abandoned> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                     |
| prefLabel | 学習課題を異常終了する                                                           |

- 判定条件

| 項目   | 値                                           |
| :--- | :------------------------------------------ |
| verb | <https://w3id.org/xapi/adl/verbs/abandoned> |

#### 5.3.7.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |

### 5.3.8　学習課題の実施状況を初期化する

#### 5.3.8.1　基本仕様

- 学習課題の実施状況が初期化されたことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                       |
| :-------- | :---------------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/initialized> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                       |
| prefLabel | 学習課題の実施状況を初期化する                                                         |

- 判定条件

| 項目   | 値                                            |
| :--- | :------------------------------------------- |
| verb | <http://adlnet.gov/expapi/verbs/initialized> |

#### 5.3.8.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |

### 5.3.9　学習課題を免除する

#### 5.3.9.1　基本仕様

- 教職員が児童生徒の学習課題を免除したことを記録するためのテンプレート。
- 識別情報

| 項目        | 値                                                                  |
| :-------- | :----------------------------------------------------------------- |
| id        | <https://w3id.org/xapi-japan-profiles/lms/templates/v1.0.0/waived> |
| inScheme  | <https://w3id.org/xapi-japan-profiles/lms/v1.0.0>                  |
| prefLabel | 学習課題を免除する                                                          |

- 判定条件

| 項目   | 値                                        |
| :--- | :--------------------------------------- |
| verb | <https://w3id.org/xapi/adl/verbs/waived> |

#### 5.3.9.2　記述規則（Rules）

| 項目                   | Location (JSONPath)   | Presence | 説明(scopeNote) |
| :------------------- | :-------------------- | :------- | :------------- |
| **オブジェクトのオブジェクトタイプ** | `$.object.objectType` | included | objectのオブジェクトタイプ。 |
