# xAPI Japan Profiles Domain Profile テンプレート

> **注意**: このテンプレートは、新しいDomain Profileを作成する際の雛形です。  
> `[ドメイン名]`、`[domain]`、`[Domain]` 等のプレースホルダーを実際の値に置き換えて使用してください。

---

# 1.　本プロファイルについて

## 1.1　位置づけ

　本プロファイルは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである[ドメイン名]TFにおける学習ログを対象として取りまとめた **xAPI Japan Profiles [Domain] Profile** 標準仕様である。  
　本仕様は、[ドメイン名]分野に記載されている特性を踏まえ、[対象システム・環境]上で発生する[主な活動内容]に関する学習ログを体系的に記録するための仕様である。

### 1.1.1　共通方針

　本プロファイルは、各コンテンツ事業者に対して本規定どおりの出力を強制するものではない。  
　xAPIプロファイルの思想自体が、そのような強制力を持たせるものではなく、表現の共通化を支えるための枠組みである。  
　本プロファイルは、出力方法の方向性を示す「表現のための資産」として位置づけ、「推奨」として扱う。  
　したがって、本プロファイルに記載された全項目への一律の準拠を求めるものではない。コンテンツの特性に応じて、記載したログを出力しない場合や一部項目を満たさない場合も許容される。  
　なお、本プロファイルは xAPI 1.0.3 をベースとする。  
　学習eポータルと連携する場合は、システム間の相互運用性を確保する観点から、「初等中等教育におけるシステム間連携のための相互運用標準モデル Version 5.00」も参照する。

## 1.2　目的

　本プロファイルは、[ドメイン名]における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、[Domain] Profileとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件

　本プロファイルにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　本仕様書の記述は、特定製品を前提とせず、現実的な範囲の「架空ツール」を想定して行う。この前提により、既存システムとの部分的不一致や未確定要素に起因する議論停滞を回避する。  
　本プロファイルに記載される語彙（Verb、ActivityType、Extension等）は以下のいずれかに整理される。(1) 必要に応じて本プロファイル内のConceptsで定義する。(2) ADLや他の標準で定義済みの語彙を直接参照する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本プロファイルは、[ドメイン名]における学習ログの標準的な解釈および実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。省略理由は下記に示すとおりである。

- typeに期待される固定値StatementTemplate
  - 省略理由：typeに指定される固定値StatementTemplateは、JSON-LD形式における機械可読性を担保するための項目である。本プロファイルでは、読み手による理解を前提とした仕様書として、StatementTemplateの構造および位置づけを章構成および見出しによって明示しているため、当該項目は省略する。

　なお、この項目については、将来的にプロファイルの登録や機械可読な形式での提供が必要となる場合に、改めて検討することとする。

## 1.4　定義範囲

　本プロファイルは、xAPI Japan Profiles [Domain] Profileを構成する要素のうち、メタ情報、（必要に応じた）Concepts、各操作行動に対応するStatementTemplateおよびStatementのRulesを定義することを目的とする。ただし、[ドメイン名]における学習行動が非線形である特性を踏まえ、xAPIプロファイルにおけるPatternsは定義の対象外とする。  
　本プロファイルは、実装者がJSON形式のプロファイル（StatementTemplateを含む）を理解し、xAPI Statementを正しく生成するための実装補助資料である。定義された各ユースケースの構造やサンプルは、プロファイルビューアーにJSONファイルを読み込ませることで直接確認することができる。

## 1.5　本プロファイルの構成について

　本プロファイルは、xAPIプロファイル仕様に基づき、[ドメイン名]学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本プロファイルは、以下の要素を含む。

- メタ情報：プロファイル全体のメタ情報およびバージョン管理
- Concepts：必要に応じたVerb、ActivityType、Extensionsの定義
- StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素
- Rules：StatementTemplateの検証規則

# 2.　メタ情報

## 2.1　本章の位置づけ

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、プロファイル全体の情報として参照される項目である。

## 2.2　構成要素

　プロファイルのメタ情報を構成する要素を示す。

| 項目                     | 説明                                   | 値                                                           |
| :----------------------- | :------------------------------------- | :----------------------------------------------------------- |
| **id**                   | プロファイルIRI                        | `https://w3id.org/xapi-japan-profiles/[domain]/v1.0.0`      |
| **type**                 | オブジェクトタイプ                     | `Profile`                                                    |
| **conformsTo**           | 準拠するxAPIプロファイル仕様               | `https://w3id.org/xapi/profiles#1.0`                         |
| プロファイル名 prefLabel | プロファイルを識別する名称             | xAPI Japan Profiles [Domain] Profile                         |
| バージョン version       | プロファイルの改訂番号やリリース状態   | v1.0.0                                                       |
| 作成者/管理者 author     | プロファイルの作成者や責任者           | ICT CONNECT 21 xAPI SWG                                      |
| 作成日/更新日 versions   | 文書化日または改訂日                   | 2026-04-01                                                   |
| 言語 languages           | メタ情報およびプロファイルの記載言語   | 日本語                                                       |
| 目的/説明 definition     | プロファイルが対象とする学習ログや用途 | 日本の初等中等教育における[ドメイン名]学習ログ標準プロファイル |
| ドキュメントバージョン   | 文書版数                               | 2026年度版                                                   |

## 2.3　記述規則の記載方針

　本プロファイルでは、xAPI Profile Specification および xAPI-Specで規定されている内容と同一の項目は重複して記載しない。  
　各StatementTemplateでは、[Domain] Profileとして個別に明示する必要がある項目のみを、当該Templateの記述規則（Rules）に記載する。

# 3.　[ドメイン名]に関するユースケース

## 3.1　本章の位置づけ

　本章では、[ドメイン名]における学習活動の特性を述べ、本プロファイルで定義するStatementTemplateの背景にある考え方を示す。

## 3.2　[ドメイン名]の特性と主な活動

[ドメイン名]における主なユースケースは、[主要な学習活動の説明]である。

主な学習活動の例：

- **[活動1]**: [説明]
- **[活動2]**: [説明]
- **[活動3]**: [説明]

## 3.3　本プロジェクトの成果と今後の課題

**本プロジェクトの成果**

- 本プロファイルでは、[実装範囲]を記録するStatementTemplateを定義した。これにより、[実現される効果]が可能になる。一方で、[スコープ外の機能]は対象外としている。

**今後の課題**

- **[課題名1]**: [説明]
- **[課題名2]**: [説明]
- **[課題名3]**: [説明]

# 4.　StatementTemplate

## 4.1　本章の位置づけ

　本章では、[Domain] Profileにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。

## 4.2　前提条件

- 基本仕様
  - 冒頭にdefinitionの位置づけとして、Templateの目的やどのような操作を記録するためのものかを定義する。
  - 識別情報
    - Templateを管理上特定するための情報として3要素（id,inScheme,prefLabel）を含む。
  - 判定条件
    - 受信したStatementがどのTemplateに該当するかを自動判別するための固定値（verb, objectActivityType）を示す。
- 記述規則（Rules）
  - Statement内の各プロパティに対する制約を示す。以下の要素を含む。
    - データの所在（location）: JSONPath方式で記述されるデータの位置。
    - presence：included（必須）、recommended（推奨）、optional（任意）とする。
    - ScopeNoteの内容に基づいた値の定義や運用上の注意点。
- Rulesテーブルの構成
  - 各Templateの記述規則（Rules）は、以下の4列で記載する：
    - 項目
    - Location (JSONPath)
    - Presence
    - 説明(scopeNote)

## 4.3　StatementTemplate一覧

### 4.3.1　[操作名1]

#### 4.3.1.1　基本仕様

- [操作内容の説明]を記録するためのテンプレート。
- 識別情報

| 項目 | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/[domain]/templates/v1.0.0/[template-id] |
| inScheme | https://w3id.org/xapi-japan-profiles/[domain]/v1.0.0 |
| prefLabel | [操作名] |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | [Verb IRI] |
| objectActivityType | [ActivityType IRI] |

#### 4.3.1.2　記述規則（Rules）

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **[項目名]** | `$.object.id` | included | [説明：例：対象を識別するIRI/URLを設定] |
| **[項目名]** | `$.timestamp` | recommended | [説明：活動が行われた日時を設定] |
| **[項目名]（Activity拡張）** | `$.object.definition.extensions['https://w3id.org/xapi-japan-profiles/[domain]/extensions/[extension-id]']` | recommended | [説明] (Core Profile参照 / [Domain名] Domain固有) |

> [!NOTE]
> - 補足条件がある場合はここに記載する。

### 4.3.2　[操作名2]

#### 4.3.2.1　基本仕様

- [操作内容の説明]を記録するためのテンプレート。
- 識別情報

| 項目 | 値 |
| :--- | :--- |
| id | https://w3id.org/xapi-japan-profiles/[domain]/templates/v1.0.0/[template-id-2] |
| inScheme | https://w3id.org/xapi-japan-profiles/[domain]/v1.0.0 |
| prefLabel | [操作名2] |

- 判定条件

| 項目 | 値 |
| :--- | :--- |
| verb | [Verb IRI] |
| objectActivityType | [ActivityType IRI] |

#### 4.3.2.2　記述規則（Rules）

| 項目 | Location (JSONPath) | Presence | 説明(scopeNote) |
| :--- | :--- | :--- | :--- |
| **[項目名]** | `$.object.id` | included | [説明] |
| **[その他の項目]** | [JSONPath] | [Presence] | [説明] |

---

## 附則：テンプレート使用ガイド

### 1. プレースホルダーの置換

- `[ドメイン名]`: CBT、LMS、ebook、Group Learning Support Tool 等
- `[Domain]`: Assessment、LMS、ebook、Group-LST 等（表示名）
- `[domain]`: assessment、lms、ebook、group-lst 等（IRI用小文字）
- `[操作名]`: 具体的な操作名称
- `[template-id]`: テンプレートID
- `[Verb IRI]`: Core Profileまたは既存標準のVerb IRI
- `[ActivityType IRI]`: ActivityType IRI
- `[extension-id]`: 拡張項目ID

### 2. ドキュメント作成の流れ

1. メタ情報を記入する。
2. ユースケースを定義する。
3. StatementTemplate（基本仕様／記述規則）を記述する。
4. Core Profile参照とDomain固有語彙の区別を確認する。
5. ガイドラインのチェックリストで整合性を確認する。

### 3. 参考資料

- [Domain Profile Guidelines](./Domain_Profile_Guidelines.md)
- [Core Profile Guidelines](./Core_Profile_Guidelines.md)
- [assessment Profile](../../assessment/v1.0.0/assessment_profile.md)
- [LMS Profile](../../lms/v1.0.0/lms_profile.md)
- [ebook Profile](../../ebook/v1.0.0/ebook_profile.md)
- [Group-LST Profile](../../group-lst/v1.0.0/group-lst_profile.md)
