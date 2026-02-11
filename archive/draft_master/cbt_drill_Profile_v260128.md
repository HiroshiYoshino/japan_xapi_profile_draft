
デジタルドリル/CBTに関する
xAPIプロファイル標準仕様（案）

2026年1月28日版

---

# 1. 本ドキュメントについて

本ドキュメントは、デジタルドリル/CBT分野における学習ログを対象として取りまとめたdigital drills and CBT xAPI Profile仕様（案）である。  
本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21 技術ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるデジタルドリル/CBTタスクフォースが作成した。  
本ドキュメントの仕様は、日本国内で広く利用されている文部科学省CBTシステム(以下MEXCBT)のxAPI仕様を参照しつつ、特に学習者の到達状況把握につながる得点情報を記録できることを重視して策定した。他の情報については、デジタルドリル/CBTの結果情報の活用にあたり記録できることが望ましい要素を取り上げたが、xAPI Profileの採用の容易性を考慮し推奨事項とした。    

---

# 2.　本ドキュメントの構成について

TBD  

- 本ドキュメントが記述するxAPI Profileの識別情報は以下とする。

## xAPI Profileの構成
- IRI: `https://w3id.org/jpXXX/assessment/v1.0`
- definition: アンケート向けxAPI Profile

---

# 3.　本ドキュメントが含むxAPIの概念(Concept)
**本章では、xAPI Profileの「Concept」に相当する本Profile固有の概念の記述に加えて、本Profileが参照する既存の概念についても記述している**

## 3.1 Verbs (動詞)
### 3.1.1 attempted
- アセスメントの提供開始（受験開始操作やページ表示）を示す。
#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | http://adlnet.gov/expapi/verbs/attempted | - |
| prefLabel.en | attempted | - |

### 3.1.2 answered
- 学習者がAssessment内の設問に応答したことを示す。
#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | http://adlnet.gov/expapi/verbs/answered | - |
| prefLabel.en | answered | - |

### 3.1.3 completed
- Assessmentが終了したことを示す。
- 学習者が明示的に終了したかどうかはresult.completedで示す。
#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | http://adlnet.gov/expapi/verbs/completed | - |
| prefLabel.en | completed | - |

### 3.1.4 viewed
- 学習コンテンツやアイテムページの閲覧を示す。
#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | http://id.tincanapi.com/verb/viewed | - |
| prefLabel.en | viewed | - |

### 3.1.5 補記 verbの選定経緯

- MEXCBTの既存のverbのコンセプトは、令和2年度(2020年度)のMEXCBTのプロトタイプ稼働時点構想時点で公開されていた[Tin Can APIのAssessment Profile](https://registry.tincanapi.com/#profile/27)に由来している。その一方で、xAPI Profileの新規公開サイトは2019年9月に公開されたxAPI Profile Serverに移り、SCORM xAPI Profile、cmi5、Navi xAPI Profileといった新たなxAPI Profileが公開された。2025/12現在、ADLが公開するxAPI Profileのリポジトリ[xapi-wuthored-profile](https://github.com/adlnet/xapi-authored-profiles)において、Tin Can APIのAssessment Profile相当のProfileは公開されていない。また、本プロファイルの検討においては、京都大学緒方研究室からMEXCBTとは異なる語彙の採用や、ツール間で共通の語彙の採用も提案されている。このため上記プロファイルでは、国際的に比較的主流の方式と見取れるコンセプトを改めて参照し語彙選定を検討した。具体的には以下の語彙を選定候補とした。

| 概念 | 説明 | IRI |
| :--- | :--- | :--- |
| initialized | Assessmentの提供開始を示す。 | http://adlnet.gov/expapi/verbs/initialized |
| responded | 学習者がAssessment内の設問に応答したことを示す。 | http://adlnet.gov/expapi/verbs/responded |
| terminated | Assessmentが終了したことを示す。学習者が明示的に終了したかどうかはresult.completedで示す。 | http://adlnet.gov/expapi/verbs/terminated |
| passed | 学習者が個々の問題を正答したことを示す。 | http://adlnet.gov/expapi/verbs/passed or https://w3id.org/xapi/adb/verbs/passed |
| failed | 学習者が個々の問題を誤答したことを示す。 | http://adlnet.gov/expapi/verbs/failed or https://w3id.org/xapi/adb/verbs/failed |
| read | 学習コンテンツやアイテムページの閲覧を示す。 | http://activitystrea.ms/schema/read または https://w3id.org/xapi/adb/verbs/read|

- TF_CBT内ではMEXCBTとの互換性確保が重要という認識が強く、上記の語彙の採用は見送りとした。


## 3.2 ActivityType (活動の種類)
### 3.2.1 assessment
- アセスメント全体を識別するアクティビティタイプ。initialized/terminatedステートメントで使用する。  
#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | http://adlnet.gov/expapi/activities/assessment | - |
| prefLabel.en | assessment | - |

### 3.2.2 page
- Webコンテンツやアプリにおけるページを表す。readステートメントで使用する。
#### 識別子プロパティ  

| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | http://activitystrea.ms/schema/1.0/page | - |
| prefLabel.en | page | - |

### 3.2.3 補記 ActivityTypeの選定経緯
- MEXCBTの既存のActivityTypeは以下の要素を含んでいる。  

| 概念 | 説明 | IRI |
| :--- | :--- | :--- |
| question | アセスメント内の採点や正誤の判定単位での活動を識別し、その結果を出力する際に用いるアクティビティタイプ。respondedステートメントで使用。 | http://adlnet.gov/expapi/activities/question |
| cmi.interaction | アセスメント内のインタラクション単位の活動を識別するアクティビティタイプ。特に、cmi.interactionの活動タイプに当てはまるrespondedステートメントで使用。 | http://adlnet.gov/expapi/activities/cmi.interaction |

- MEXCBTでは、問題の構造の違いに応じて、同じverb・ActivityTypeの組み合わせに対して異なるログ出力の規則を採用している。
  - ログ出力のタイプとして「タイプ 1 」と「タイプ 2」が存在する。
  - 「タイプ 1 」はverb=answered、ActivityType=cmi.interactionの組み合わせでログを出力する。
  - 「タイプ 2 」はverb=answered、ActivityType=questionの組み合わせのログと、verb=answered、ActivityType=cmi.interactionの組み合わせでログの計2種を出力する。
  - 「タイプ 1 」と「タイプ 2 」で共通するverb=answered、ActivityType=cmi.interactionの組み合わせに対して、resultの出力内容は異なっている。

| 項目 | タイプ1 アイテム | タイプ2 アイテム | タイプ2 インタラクション |
| :--- | :--- | :--- | :--- |
| verb | answered | answered | answered |
| obbject.id | アイテムID | アイテムID | アイテムID+インタラクション識別子 |
| object.activityType | cmi.interaction | question | cmi.interaction |
| result.score | 含む | 含む | 含まない |
| result.duration | 含む | 含む | 含まない |

- xAPI Profileの仕様上、特定のverb・特定のActivityType・またはそれらの特定の組み合わせに対して、共通の出力ルールを設定する必要がある。このためMEXCBTの出力規則をそのままxAPI Profileに反映することは困難であった。
- また、ログの出力規則が多数に分かれることは、xAPI Profileの仕様が複雑化し利用を困難にするとも考えられた。
- また、MEXCBTが出力するような個々の設問の形式情報についてアプリケーション間で共通の仕様を定めることは困難とも考えられた。
- これらの事項を考慮し、本プロファイルでは得点情報の出力に重点を置き、ActivityTypeを問わずverb=answeredのステートメントに対して共通の出力ルールを設定することとした。  
  
## 3.3 Extensions (拡張)
- xAPI Profileの仕様の都合から、同一の語彙をActivityとContextでそれぞれ使いたい場合、同等の内容で別の拡張として定義した。  

### 3.3.1 subject (教科・Activity拡張用)
- 教科名を表す文字列。
- 教材等のobjectのメタ情報として教科名を設定する際に利用する。
- 教科名の出典として学習指導要領コードと教育データ標準の2種が選択肢となる。学習指導要領コードのほうが包含する教科名が広いため、学習指導要領コードに準じる
- 今後の用途の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/subject-activity | - |
| type | ActivityExtension | - |
| perfLabel.en | subject | - |

#### inlineSchema
- type=array
- enum: 学習指導要領コード上の教科名を列挙する
- xAPI Profile記述概要
```json
{
  "type": "array",
  "items": {
    "type": "string",
    "enum": ["国語", "算数", "…"]　//学習指導要領コード上の教科名を列挙する
  }
}
```

### 3.3.2 subject (教科・Context拡張用)
- 教科名を表す文字列。
- 授業の教科等contextのメタ情報として教科名を設定する際に利用する。
- 教科名の出典として学習指導要領コードと教育データ標準の2種が選択肢となる。学習指導要領コードのほうが包含する教科名が広いため、学習指導要領コードに準じる。
- 今後の用途の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/subject-context | - |
| type | ContextExtension | - |
| perfLabel.en | subject | - |

#### inlineSchema
- type=array
- enum: 学習指導要領コード上の教科名を列挙する

### 3.3.3 grade (学年・Activity拡張用)
- 学年を表す文字列。
- 教材等のobjectのメタ情報として学年を設定する際に利用する。
- 学年の出典として学習指導要領コードと教育データ標準の2種が選択肢となる。教育データ標準は学年の語彙がリスト化されているのに対して、学習指導要領コードはリストがなく小・中・高等の区分による語彙の使い分けも明確ではないため、教育データ標準に準じる。
- 今後の用途の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/grade-activity | - |
| type | ActivityExtension | - |
| perfLabel.en | grade | - |
#### inlineSchema
- type=array
- enum: 文部科学省教育データ標準（主体情報）上の「学年」項目の要素名を列挙する

### 3.3.4 grade (学年・Context拡張用)
- 学年を表す文字列。
- 授業の学年等contextのメタ情報として学年を設定する際に利用する。
- 学年の出典として学習指導要領コードと教育データ標準の2種が選択肢となる。教育データ標準は学年の語彙がリスト化されているのに対して、学習指導要領コードはリストがなく小・中・高等の区分による語彙の使い分けも明確ではないため、教育データ標準に準じる。
- 今後の用途の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/grade-context | - |
| type | ContextExtension | - |
| perfLabel.en | grade | - |

#### inlineSchema
- type=array
- enum: 文部科学省教育データ標準（主体情報）上の「学年」項目の要素名を列挙する

### 3.3.5 Courses of Study Code (学習指導要領コード・Activity拡張用)
- 学習指導要領コードを表す文字列。
- 教材等のobjectのメタ情報として学習指導要領コードを設定する際に利用する。
- 今後の用途の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/cscode-activity | - |
| type | ActivityExtension | - |
| perfLabel.en | Courses of Study Code | - |


### 3.3.6 Courses of Study Code (学習指導要領コード・Context拡張用)
- 学習指導要領コードを表す文字列。
- 授業の内容等contextのメタ情報として学習指導要領コードを設定する際に利用する。
- 今後の用途の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/cscode-context | - |
| type | ContextExtension | - |
| perfLabel.en | Courses of Study Code | - |

### 3.3.7 purpose of question (問題の趣旨)
- 問題の趣旨を表す値
- 学習指導要領コードよりも細かいレベルで問題の目的を示すために利用する。
  - 例えば、学習指導要領コード「8250263111200000」((ｲ) 分数の乗法及び除法の計算ができること。)については、「小学校学習指導要領（平成 29 年告示）解説」において「真分数や仮分数の計算」や「帯分数を含む計算」といったより細かな内容に分解されている。このようなより細かいレベルでの問題の趣旨を示し、学習者や指導者が問題・結果の活用を行いやすくすることを目的とする。
  - 学習指導要領コードの細分化された共通語彙は存在しないため、本プロファイルの定義上は自由記述とする。
- 本プロファイルがアンケートの回答も対象とした場合、質問の趣旨を示すためにも利用する。
  - 例えば、全国学力・学習状況調査の質問調査においては、個別の調査項目の質問に対して「挑戦心、達成感、規範意識、自己有用感、幸福感等」といった設問の観点の分類が設定されている。このような質問の分類や、分類で用いられる端的な質問の趣旨を示し、学習者や指導者が質問・結果の活用を行いやすくすることを目的とする。
    - 複数のレベルの趣旨を設定する可能性も想定する。
    - 例：「自分には、よいところがあると思いますか」という設問に対して、["自己有用感","挑戦心、達成感、規範意識、自己有用感、幸福感等"]といった複数の趣旨を設定する。
  - 質問調査の目的に対する細分化された共通語彙は存在しないため、この用途においても本プロファイルの定義上は自由記述とする。
- 先行するContextExtension「http://id.tincanapi.com/extension/purpose」と類似した意味を持つが、以下の観点から本Profile固有のExtensionとして定義する。
  - 問題自体のメタ情報としてActivityExtensionでの用途を想定する。
  - 今後の用途の可能性を考慮し配列型データ型を指定する。

### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/purpose-of-question | - |
| type | ActivityExtension | - |
| perfLabel.en | purpose of question | - |

#### inlineSchema
- type=array
- items:type=string

### 3.3.8 question order (問題の出題順序)
- デジタルドリルやCBTにおける問題の出題順序を表す値
- デジタルドリルやCBTが問題を提示する順序を示し、学習者や指導者が取り組みの結果の参照・活用を行いやすくすることを目的とする。
- 問題の出題がアダプティブに変化する場合、同一の問題であっても学習者ごとに出題順序が異なる可能性がある。この場合学習者毎に実際に出題された順序を記録する。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/question-order | - |
| type | ActivityExtension | - |
| perfLabel.en | question order | - |
#### inlineSchema
- type=integer

### 3.3.9 content type (解説やヒントといったコンテンツの種類)
- 学習者が参照したものが、問題解答中のヒントなのか、解答後の結果なのか、解答後の解説なのかの区分を記載する。
- 今後の語彙・用途の拡張の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/content-type | - |
| type | Activityxtension | - |
| perfLabel.en | content type | - |

#### inlineSchema
- type=array
- enum: hint(回答中のヒント) / result(得点、正誤等の結果) / explanation(問題の解説)

### 3.3.10 assessment type (評価のタイプ)
- 評価のタイプを表す値
- 先行するExtension「http://id.tincanapi.com/extension/assessment-type」と類似した意味を持つが、データ型と語彙を指定するため本Profile固有のExtensionとして定義する。
- 今後の語彙・用途の拡張の可能性を考慮し配列型とする。

#### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/extensions/assessment-type | - |
| type | ContextExtension | - |
| perfLabel.en | assessment type | - |

#### inlineSchema
- type=array
- enum: diagnostic(診断的)/formative(形成的)/summative(総括的)


---

# 4. ステートメントテンプレート
## 4.1 Assessmentの開始
- **id**: `https://w3id.org/jpXXX/assessment/template/attempted-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: Assessmentの提供開始（受験開始操作やページ表示）を記録する。LRPは開始したAssessmentを識別する情報を含める。

### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/attempted` | - |
| Object | `objectActivityType` | `http://adlnet.gov/expapi/activities/assessment` | - |

### Rules（追加の必須/禁止/許容値）
#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | Assessmentの日本語表示名をLRPが任意に設定 | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |

### 補記
- 

### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "b2d52f2c-cc4d-42d0-bd9e-78329b1ee00f",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/attempted",
            "display": {
                "en": "attempted"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890",
            "definition": {
                "type": "http://adlnet.gov/expapi/activities/assessment"
            }
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    }
                ]
            }
        },
        "timestamp": "2022-03-03T04:45:03.051+00:00"
}

```

### Example (recommendedをすべて含めた場合)

```json
{
    "version": "1.0.0",
    "id": "b2d52f2c-cc4d-42d0-bd9e-78329b1ee00f",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/attempted",
            "display": {
                "en": "attempted"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890",
            "definition": {
                "name": {
                    "ja-jp": "分数のかけ算1"
                },
                "type": "http://adlnet.gov/expapi/activities/assessment",
                "extensions": {
                    "https://w3id.org/jpXXX/assessment/subject-activity": ["算数"],
                    "https://w3id.org/jpXXX/assessment/grade-activity": ["小学校第6学年"],
                    "https://w3id.org/jpXXX/assessment/cscode-activity": ["8250263111200000"]
                }
            }
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    }
                ],
                "grouping": [
                    {
                        "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                    }
                ]
            },
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-context": ["算数"],
                "https://w3id.org/jpXXX/assessment/grade-context": ["小学校第6学年"],
                "https://w3id.org/jpXXX/assessment/cscode-context": ["8250263111200000"],                
                "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
            }
        },
        "timestamp": "2022-03-03T04:45:03.051+00:00"
}
```


## 4.2 問題への回答(得点・正誤情報を含む)

- **id**: `https://w3id.org/jpXXX/assessment/template/answered-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: 学習者が得点・正誤判定単位の設問に回答したことを記録する。得点や正誤の結果情報を含む。

### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/answered` | - |

### Rules（追加の必須/禁止/許容値）
#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 問題の名前をLRPが任意に設定 | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/purpose-of-question']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/question-order']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

#### `$.result.duration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答所要時間 | - |

#### `$.result.score.scaled`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 得点率 | - |

#### `$.result.score.max`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 最大点 | - |

#### `$.result.score.raw`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 素点 | - |

#### `$.result.response`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答値 | - |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |


### 補記
- result.scoreは、採点・正誤判定単位の設問に対して必ず含めることを求める。
- 正誤情報のみあり得点情報がない場合はmaxを1、rawを1(正答)または0(誤答)、scaledを1.0(正答)または0.0(誤答)とする。
- 採点が自動以外で採点が未実施の場合はresult.scoreが出力できない。このため採点が未実施の段階のstatementではcontext.contextActivities.category[*]で本プロファイルのIRIを参照しない。採点終了後にresult.scoreを出力した際に本プロファイルの参照を行うこととする。
- Determining PropertiesにおいてobjectActivityTypeは指定せず、任意のobjectActivityTypeに対して本テンプレートのルールを適用可能とすることで、MEXCBTの「タイプ1」「タイプ2」双方に対応可能とする。
- 将来的に、アンケート回答結果の記録のために回答値を必ず含むステートメントテンプレートが必要になる可能性がある。その場合、本ステートメントテンプレートとは異なるDetermining Propertiesを持つステートメントテンプレートが必要になることから、回答値を必ず含むステートメントテンプレートのために別種のxAPI Profileを定義するか、本プロファイルのDetermining Propertiesを追加し、回答値を必ず含むステートテンプレートと区別にする可能性がある。


### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
    "actor": {
        "objectType": "Agent",
        "account": {
            "homePage": "https://example.platform.jp",
            "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/answered",
        "display": {
            "en": "answered"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://example.platform.jp/assessment/1234567890/question/0001",
    },
    "context": {
        "contextActivities": {
            "category": [
                {
                    "id": "https://w3id.org/jpXXX/assessment/v1.0"
                }
            ]
        }
    },
    "result": {
        "duration": "PT30S",
        "score": {
            "scaled": 0.5,
            "raw": 1,
            "max": 2
        }
    },
    "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

### Example (recommendedをすべて含めた場合)

```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
            "definition": {
                "name": {
                    "ja-jp": "次の計算をしなさい： 3/4 * 1/2"
                },
                "extensions": {
                    "https://w3id.org/jpXXX/assessment/subject-activity": ["算数"],
                    "https://w3id.org/jpXXX/assessment/grade-activity": ["小学校第6学年"],
                    "https://w3id.org/jpXXX/assessment/cscode-activity": ["8250263111200000"],
                    "https://w3id.org/jpXXX/assessment/purpose-of-question": ["真分数の乗法の計算"],
                    "https://w3id.org/jpXXX/assessment/question-order": 1
                }
            }
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    }
                ],
                "grouping": [
                    {
                        "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                    }
                ]
            },
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-context": ["算数"],
                "https://w3id.org/jpXXX/assessment/grade-context": ["小学校第6学年"],
                "https://w3id.org/jpXXX/assessment/cscode-context": ["8250263111200000"],                
                "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
            },        
        },
        "result": {
            "duration": "PT30S",
            "score": {
                "scaled": 0.5,
                "raw": 1,
                "max": 2
            }
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```


### 4.3 学習コンテンツやページの参照

- **id**: `https://w3id.org/jpXXX/assessment/template/content-viewed-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: 学習コンテンツやページの閲覧を記録する。

### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://id.tincanapi.com/verb/viewed` | - |
| Object | `objectActivityType` | `http://activitystrea.ms/schema/1.0/page` | - |


### Rules（追加の必須/禁止/許容値）

#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | コンテンツの名前をLRPが任意に設定 | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/extensions/content-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []hint/result/explanation | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/purpose-of-question']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/question-order']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.parent[*]`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ヒントや結果、解説の対象となるassessmentまたはquestionのobject.id | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |

### 補記
- 

### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "e5f6a7b8-c9d0-1e2f-3a4b-5c6d7e8f9012",
    "actor": {
        "objectType": "Agent",
        "account": {
            "homePage": "https://example.platform.jp",
            "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
        }
    },
    "verb": {
        "id": "http://id.tincanapi.com/verb/viewed",
        "display": {
            "en": "viewed"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://example.platform.jp/assessment/1234567890/content/hint1",
        "definition": {
            "type": "http://activitystrea.ms/schema/1.0/page"
        }        
    },
    "context": {
        "contextActivities": {
            "parent": [
                {
                    "id": "http://example.platform.jp/assessment/1234567890/question/0001"
                }
            ],
            "category": [
                {
                    "id": "https://w3id.org/jpXXX/assessment/v1.0"
                }
            ]
        }
    },
    "timestamp": "2022-03-03T05:00:03.051+00:00"
}
```


### Example (recommendedをすべて含めた場合)
```json
{
    "version": "1.0.0",
    "id": "e5f6a7b8-c9d0-1e2f-3a4b-5c6d7e8f9012",
    "actor": {
        "objectType": "Agent",
        "account": {
            "homePage": "https://example.platform.jp",
            "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
        }
    },
    "verb": {
        "id": "http://id.tincanapi.com/verb/viewed",
        "display": {
            "en": "viewed"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://example.platform.jp/assessment/1234567890/content/hint1",
        "definition": {
            "name": {
                "ja-jp": "ヒント：分数のかけ算の考え方"
            },
            "type": "http://activitystrea.ms/schema/1.0/page",
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-activity": [
                    "算数"
                ],
                "https://w3id.org/jpXXX/assessment/grade-activity": [
                    "小学校第6学年"
                ],
                "https://w3id.org/jpXXX/assessment/cscode-activity": [
                    "8250263111200000"
                ],
                "https://w3id.org/jpXXX/assessment/extensions/content-type": [
                     "hint"
                ],
                "https://w3id.org/jpXXX/assessment/purpose-of-question": [
                    "真分数の乗法の計算"
                ],
                "https://w3id.org/jpXXX/assessment/question-order": 1
            }
        }
    },
    "context": {
        "contextActivities": {
            "parent": [
                {
                    "id": "http://example.platform.jp/assessment/1234567890/question/0001"
                }
            ],
            "category": [
                {
                    "id": "https://w3id.org/jpXXX/assessment/v1.0"
                }
            ],
            "grouping": [
                {
                    "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                }
            ],
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-context": [
                    "算数"
                ],
                "https://w3id.org/jpXXX/assessment/grade-context": [
                    "小学校第6学年"
                ],
                "https://w3id.org/jpXXX/assessment/cscode-context": [
                    "8250263111200000"
                ],
                "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
            }
        }
    },
    "timestamp": "2022-03-03T05:00:03.051+00:00"
}
```

### 4.5 Assessmentの終了

- **id**: `https://w3id.org/jpXXX/assessment/template/completed-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: Assessmentの終了を記録する。完了フラグやスコアを含む。

### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/completed` | - |
| Object | `objectActivityType` | `http://adlnet.gov/expapi/activities/assessment` | - |

### Rules（追加の必須/禁止/許容値）

#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | Assessmentの日本語表示名をLRPが任意に設定 | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/extensions/content-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []hint/result/explanation | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.parent[*]`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ヒントや結果、解説の対象となるassessmentまたはquestionのobject.id | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

#### `$.result.duration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答所要時間 | - |

#### `$.result.score.scaled`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 得点率 | - |

#### `$.result.score.max`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 最大点 | - |

#### `$.result.score.raw`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 素点 | - |

#### `$.result.success`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | true / false | - |
| 4 | none | - | - |
| 5 | scopeNote | - | 学習者が最後まで完了操作した場合はtrue、途中で操作を終えており、システムや採点者等が終了判定した場合はfalse |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |

### 補記
- 採点が自動以外で採点が未実施の場合はresult.scoreが出力できない。このため採点が未実施の段階のstatementでは本プロファイルの参照を行わないこととする。すべての採点終了後にresult.scoreを出力した際に本プロファイルの参照を行うこととする。


### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "f6a7b8c9-d0e1-2f3a-4b5c-6d7e8f901234",
    "actor": {
        "objectType": "Agent",
        "account": {
            "homePage": "https://example.platform.jp",
            "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/completed",
        "display": {
            "en": "completed"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://example.platform.jp/assessment/1234567890",
        "definition": {
            "type": "http://adlnet.gov/expapi/activities/assessment"
        }
    },
    "context": {
        "contextActivities": {
            "category": [
                {
                    "id": "https://w3id.org/jpXXX/assessment/v1.0"
                }
            ],
        }
    },
    "result": {
        "duration": "PT15M30S",
        "score": {
            "scaled": 0.85,
            "raw": 85,
            "max": 100
        }
    },
    "timestamp": "2022-03-03T05:00:03.051+00:00"
}
```

### Example (recommendedをすべて含めた場合)

```json
{
    "version": "1.0.0",
    "id": "f6a7b8c9-d0e1-2f3a-4b5c-6d7e8f901234",
    "actor": {
        "objectType": "Agent",
        "account": {
            "homePage": "https://example.platform.jp",
            "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/completed",
        "display": {
            "en": "completed"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://example.platform.jp/assessment/1234567890",
        "definition": {
            "name": {
                "ja-jp": "分数のかけ算1"
            },
            "type": "http://adlnet.gov/expapi/activities/assessment",
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-activity": [
                    "算数"
                ],
                "https://w3id.org/jpXXX/assessment/grade-activity": [
                    "小学校第6学年"
                ],
                "https://w3id.org/jpXXX/assessment/cscode-activity": [
                    "8250263111200000"
                ]
            }
        }
    },
    "context": {
        "contextActivities": {
            "category": [
                {
                    "id": "https://w3id.org/jpXXX/assessment/v1.0"
                }
            ],
            "grouping": [
                {
                    "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                }
            ]
        },
        "extensions": {
            "https://w3id.org/jpXXX/assessment/subject-context": [
                "算数"
            ],
            "https://w3id.org/jpXXX/assessment/grade-context": [
                "小学校第6学年"
            ],
            "https://w3id.org/jpXXX/assessment/cscode-context": [
                "8250263111200000"
            ],
            "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
        }
    },
    "result": {
        "duration": "PT15M30S",
        "score": {
            "scaled": 0.85,
            "raw": 85,
            "max": 100
        },
        "success": true
    },
    "timestamp": "2022-03-03T05:00:03.051+00:00"
}
```

---
# 5 アンケート向けに回答値を必ず含むステートメントテンプレートを定義する可能性の検討
- 本ドキュメントが定義した「問題への回答」ステートメントテンプレートは、得点・正誤情報を必ず含むことを前提としている。また一方で、回答値を含むことは必須としていない。
- これは、現行のMEXCBTや既存のデジタルドリルのアプリケーションにおいて、必ず回答値を含むことが困難な場合があるためである。
  - 例えば、画像を使った複雑な問題やファイルのアップロードが必要な問題に対して回答値を含むことができない場合や、もともとのアプリケーションの連携データの仕様が回答値を含んでいない場合がある。
  - MEXCBTにおいては、「タイプ２アイテムステートメント」の仕様において、回答値を含まないこととされている。
- 一方で、アンケートのように問題に対する回答値を含まなければ記録の分析が行えないケースも存在する。
- この章では、アンケート用途の問題に対して回答値を必ず含むxAPI Profileをどう整備するかについての検討を行う。

## 5.1 アンケート用のxAPI Profileを新設する可能性
- 実現方式の一つ目として、本ドキュメント記載のxAPI Profileとは別にアンケート向けにxAPI Profileを新設し、回答値を必ず含むステートメントテンプレートを定義するという方式が考えられる。
- デジタルドリル/CBTがアンケートの回答値を含むステートメントを出力する際には、アンケート向けのxAPI Profileを参照すればよい。

### 5.1.1 実現イメージ
#### xAPI Profileの構成例
- IRI: `https://w3id.org/jpXXX/survey/v1.0`
- definition: アンケート向けxAPI Profile

#### ステートメントテンプレートの構成例
- アンケートへの回答 (回答値を必ず含む)

- **id**: `https://w3id.org/jpXXX/survey/template/questionaire-answered-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/survey/v1.0`
- **目的 / 用途（definition要約）**: 学習者のアンケートの回答内容を記録する。

#### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/answered` | - |

#### Rules（追加の必須/禁止/許容値）

##### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 問題の名前をLRPが任意に設定 | - |

##### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

##### `$.result.duration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答所要時間 | - |

##### `$.result.response`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

##### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |

#### 補記
- 回答値としてresult.responseを必ず含むことを求める。
- 以下の要素もメタデータとして定義する可能性があるが、ここでは回答値を含むことについての記載例にとどめる。
  - 教科、学年、学習指導要領コード等の学習に関するメタデータ
  - アンケートの設問集計に必要な設問のカテゴリ情報に関するメタデータ
  - アンケートの回答値の統計における尺度の違い
  - アンケートの回答が数値の場合の数値の大小に対するネガポジの扱い
  - アンケートの設問の種類(単一選択/複数選択/リッカート等)および選択肢の値(あてはまる/あてはまらない等)

#### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/survey/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/survey/v1.0"
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S",
            "response": "あてはまる"
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

#### Example (メタデータを増やし、選択式の設問情報まで含めた場合の例)
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/survey/1234567890/question/0001",
            "definition": {
                "name": {
                    "ja-jp": "あなたはこの学習コンテンツを理解しましたか？"
                },
                "type": "http://adlnet.gov/expapi/activities/cmi.interaction",
                "interactionType": "choice",
                "choices": [
                    {
                        "id": "choice_1",
                        "description": {
                            "ja": "あてはまる"
                        }
                    },
                    {
                        "id": "choice_2",
                        "description": {
                            "ja": "どちらかといえばあてはまる"
                        }
                    },
                    {
                        "id": "choice_3",
                        "description": {
                            "ja": "どちらともいえない"
                        }
                    },
                    {
                        "id": "choice_4",
                        "description": {
                            "ja": "どちらかといえばあてはまらない"
                        }
                    },
                    {
                        "id": "choice_5",
                        "description": {
                            "ja": "あてはまらない"
                        }
                    }
                ],                
                "extensions": {
                    "https://w3id.org/jpXXX/survey/extensions/subject-activity": [
                        "算数"
                    ],
                    "https://w3id.org/jpXXX/survey/extensions/grade-activity": [
                        "小学校第6学年"
                    ],
                    "https://w3id.org/jpXXX/survey/extensions/cscode-activity": [
                        "8250263111200000"
                    ],
                    "https://w3id.org/jpXXX/survey/extensions/purpose-of-question": [
                        "理解度の把握",
                        "真分数の乗法の計算"
                    ],
                    "https://w3id.org/jpXXX/survey/extensions/question-order": 1
                }
            }            
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/survey/v1.0"
                    }
                ],
                "grouping": [
                    {
                        "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                    }
                ]
            },
        },
        "result": {
            "duration": "PT30S",
            "response": "choice_2"
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```


### 5.1.2 利点・課題
- 利点
  - アンケート用途に特化したxAPI Profileを定義することで、回答値を必ず含むステートメントテンプレートを柔軟に設計できる。
  - デジタルドリル/CBTがアンケートの回答値を含むステートメントを出力する際に、既存のxAPI Profileと混在しないため、運用上の混乱を避けられる。    
  - MEXCBTとの互換性を考慮した場合、MEXCBTの既存のステートメントに対してxAPI Profileの参照を追加するだけで上記の最小限の例を形式上実現できる。
    - ただし、実際のアンケートの分析のしやすさを考慮すると、より多くのメタデータを含むことが望ましく、単純なxAPI Profileの参照追加で十分とは言い切れない。

- 課題
  - xAPI Profileの参照先が増え、実装者の負担が増える可能性がある。

## 5.2 本プロファイルにアンケート回答用のステートメントテンプレートを追加する可能性
- 実現方式の二つ目として、本ドキュメントが定義するxAPI Profile内に、回答値を必ず含むステートメントテンプレートを追加する方式が考えられる。
- この場合、アンケート向けの回答値を必ず含むステートメントと、回答の得点・正誤情報を必ず含むステートメントを、ステートメントテンプレートのDetermining Propertiesで区別可能とする必要がある。
- より具体的には、xAPI Profileの仕様上、ステートメントの以下の要素の組み合わせで区別可能とする必要がある。

| 項目 | 備考 |
|---|---|
| $.verb.id | 本要素のみで区別する場合、問題解答に対するverbを使い分けることとなり扱いにくい |
| $.object.definition.type | 本要素のみで区別する場合、xAPIの定義上問題解答時に推奨されているcmi.interactionをアンケート向け回答と得点・正誤付き回答のいずれかでしか使えないこととなり扱いにくい |
| $.context.contextActivities.grouping[*].definition.type | 本項目以降のcontextActivitiesとverbの組み合わせで区別する場合、問題解答に対するverbとobject.definition.typeはアンケート向け回答と得点・正誤付き回答で同一のものを使えるため、比較的扱いやすい |
| $.context.contextActivities.parent[*].definition.type | 同上 |
| $.context.contextActivities.other[*].definition.type | 同上 |
| $.context.contextActivities.category[*].definition.type | 同上 |

- 上記整理の判断から、ここでは$.context.contextActivities.~を使ったステートメントの区別について案を示す。
- より具体的には、個々の設問の回答ステートメントにおいて、$.context.contextActivities.category[*].definition.typeを使ってアンケート向け回答と得点・正誤付き回答を区別する案を示す。
  - categoryは消去法で選択している。parentやgroupingを使う場合、設問の親となるActivityや問題群となるActivityのタイプに従って区別することになり、設問単位での区別に利用するには不適切と考えられた。また、otherを使う場合、otherの利用目的が明確でないため、設問単位での区別に利用するには不適切と考えられた。
  - 個々の設問の回答に対して区別を設け、異なるルールが適用可能となるため、以下の例ではアンケート向け回答への対応に加えて、手動採点の未採点状態を表すためのルールも併記している。

### 5.2.1 実現イメージ
#### ステートメント判定用のActivityTypeおよびActivityの定義
- xAPI Profileの仕様上、特定のverb・特定のActivityType・またはそれらの特定の組み合わせに対して、共通の出力ルールを設定する必要がある。
- 未採点の回答記録は得点の出力を必須にできないため、未採点の回答記録と採点済みの回答記録を区別可能とするために、以下のActivityTypeとActivityを定義する。
- アンケートの回答記録についても、得点・正誤情報を持たず回答値そのものを記録するために区別可能とするために、以下のActivityTypeとActivityを定義する。

#### 得点・正誤情報を持たず、アンケートとして回答値そのものを記録するための回答記録用ActivityType
##### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/activity-types/survey-answer | - |
| prefLabel.en | survey answer | - |

#### 得点・正誤情報を持たず、アンケートとして回答値そのものを記録するための回答記録用Activity
##### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/activities/survey-answer | - |
| type | https://w3id.org/jpXXX/assessment/activity-types/survey-answer | - |

#### 利用例
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/survey-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/survey-answer"
                        }
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S"
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

#### 採点済の回答記録用ActivityType
##### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/activity-types/graded-answer | - |
| prefLabel.en | graded answer | - |

#### 採点済の回答記録用Activity
##### 識別子プロパティ
| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/activities/graded-answer | - |
| type | https://w3id.org/jpXXX/assessment/activity-types/graded-answer | - |


#### 採点済の回答記録利用例
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/graded-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/graded-answer"
                        }
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S",
            "score": {
                "scaled": 0.5,
                "raw": 1,
                "max": 2
            }
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

#### 未採点の回答記録用ActivityType
##### 識別子プロパティ

| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/activity-types/ungraded-answer | - |
| prefLabel.en | ungraded answer | - |

#### 未採点の回答記録用Activity
##### 識別子プロパティ

| 項目 | 値 | 備考 |
| :--- | :--- | :--- |
| id | https://w3id.org/jpXXX/assessment/activities/ungraded-answer | - |
| type | https://w3id.org/jpXXX/assessment/activity-types/ungraded-answer | - |

#### 未採点の回答記録利用例
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/ungraded-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/ungraded-answer"
                        }
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S"
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

#### アンケートへの回答(回答値を含む回答)用のステートメントテンプレートの定義

- **id**: `https://w3id.org/jpXXX/assessment/template/answered-survey-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: 学習者がアンケートの設問に回答したことを記録する。回答値を含む。

### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/answered` | - |
| Object | `object.definition.type` | `http://adlnet.gov/expapi/activities/cmi.interaction` | - |
| Context | `context.contextActivities.category[*].definition.type` | `https://w3id.org/jpXXX/assessment/activity-types/survey-answer` | - |


### Rules（追加の必須/禁止/許容値）

#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 問題の名前をLRPが任意に設定 | - |

#### `$.object.definition.interactionType`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | xAPI Specに基づいたinteractionType | - |

#### `$.object.definition.choices`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | xAPI Specに基づいたchoices | - |

#### `$.object.definition.likert`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | xAPI Specに基づいたlikert | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/purpose-of-question']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/question-order']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

#### `$.result.duration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答所要時間 | - |

#### `$.result.score.scaled`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 得点率 | - |

#### `$.result.score.max`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 最大点 | - |

#### `$.result.score.min`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 最小点 | - |

#### `$.result.score.raw`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 素点 | - |

#### `$.result.response`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答値 | - |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |


### 補記
- アンケート設問のinteractionTypeには、xAPI Specで定義されている「choice」「likert」「fill-in」「long-fill-in」「matching」「performance」「sequencing」「numeric」「other」のうち、比較的シンプルなアンケートで用いられるであろう「choice」「likert」「fill-in」「long-fill-in」のいずれかを指定することを推奨する。
  - アンケート設問のinteractionTypeが「choice」の場合には、object.definition.choicesを含めることを推奨する。
  - アンケート設問のinteractionTypeが「likert」の場合には、object.definition.likertを含めることを推奨する。
- アンケートの設問が間隔尺度・比例尺度の場合にはresult.scoreの各子要素を含めることを推奨する。
  - 例えば、設問が5段階評価の場合、minを1、maxを5、rawを学習者の回答に対応する数値(例えば「とても満足」なら5)とする。

### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/survey-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/survey-answer"
                        }
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S",
            "response": "とても満足"
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

### Example (recommendedをすべて含めた場合)

```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
            "definition": {
                "name": {
                    "ja-jp": "次の設問に答えなさい： この学習コンテンツについてどの程度満足していますか？"
                },
                "interactionType": "likert",
                "likert": [
                    {
                        "id": "1",
                        "description": {
                            "ja-jp": "とても不満"
                        }
                    },
                    {
                        "id": "2",
                        "description": {
                            "ja-jp": "やや不満"
                        }
                    },
                    {
                        "id": "3",
                        "description": {
                            "ja-jp": "普通"
                        }
                    },
                    {
                        "id": "4",
                        "description": {
                            "ja-jp": "やや満足"
                        }
                    },
                    {
                        "id": "5",
                        "description": {
                            "ja-jp": "とても満足"
                        }
                    }
                ],
                "extensions": {
                    "https://w3id.org/jpXXX/assessment/subject-activity": ["算数"],
                    "https://w3id.org/jpXXX/assessment/grade-activity": ["小学校第6学年"],
                    "https://w3id.org/jpXXX/assessment/cscode-activity": ["8250263111200000"],
                    "https://w3id.org/jpXXX/assessment/purpose-of-question": [
                        "理解度の把握",
                        "真分数の乗法の計算"
                    ],
                    "https://w3id.org/jpXXX/assessment/question-order": 1
                }
            }
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/survey-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/survey-answer"
                        }
                    }
                ],
                "grouping": [
                    {
                        "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                    }
                ]
            },
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-context": ["算数"],
                "https://w3id.org/jpXXX/assessment/grade-context": ["小学校第6学年"],
                "https://w3id.org/jpXXX/assessment/cscode-context": ["8250263111200000"],                
                "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
            },        
        },
        "result": {
            "duration": "PT30S",
            "response": "5",
            "score": {
                "scaled": 1,
                "raw": 5,
                "max": 5,
                "min": 1
            }
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```


#### 問題への回答(得点・正誤情報を含む)用のステートメントテンプレートの定義

- **id**: `https://w3id.org/jpXXX/assessment/template/answered-graded-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: 学習者が得点・正誤判定単位の設問に回答したことを記録する。得点や正誤の結果情報を含む。

### テンプレートの合致条件(Determining Properties)
| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/answered` | - |
| Context | `context.contextActivities.category[*].definition.type` | `https://w3id.org/jpXXX/assessment/activity-types/graded-answer` | - |

### Rules（追加の必須/禁止/許容値）

#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 問題の名前をLRPが任意に設定 | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/purpose-of-question']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/question-order']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.contextActivities.grouping[*].id`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | ある一回のAssessmentの取り組みに対して同一のIRIを記述する | - |

#### `$.result.duration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答所要時間 | - |

#### `$.result.score.scaled`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 得点率 | - |

#### `$.result.score.max`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 最大点 | - |

#### `$.result.score.raw`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 素点 | - |

#### `$.result.response`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答値 | - |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |


### 補記
- result.scoreは、採点・正誤判定単位の設問に対して必ず含めることを求める。
- 正誤情報のみあり得点情報がない場合はmaxを1、rawを1(正答)または0(誤答)、scaledを1.0(正答)または0.0(誤答)とする。
- Determining PropertiesにおいてobjectActivityTypeは指定せず、任意のobjectActivityTypeに対して本テンプレートのルールを適用可能とすることで、MEXCBTの「タイプ1」「タイプ2」双方に対応可能とする。


### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/graded-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/graded-answer"
                        }
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S",
            "score": {
                "scaled": 0.5,
                "raw": 1,
                "max": 2
            }
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

### Example (recommendedをすべて含めた場合)

```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
            "definition": {
                "name": {
                    "ja-jp": "次の計算をしなさい： 3/4 * 1/2"
                },
                "extensions": {
                    "https://w3id.org/jpXXX/assessment/subject-activity": ["算数"],
                    "https://w3id.org/jpXXX/assessment/grade-activity": ["小学校第6学年"],
                    "https://w3id.org/jpXXX/assessment/cscode-activity": ["8250263111200000"],
                    "https://w3id.org/jpXXX/assessment/purpose-of-question": [
                        "真分数の乗法の計算"
                    ],
                    "https://w3id.org/jpXXX/assessment/question-order": 1
                }
            }
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/graded-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/graded-answer"
                        }
                    }
                ],
                "grouping": [
                    {
                        "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                    }
                ]
            },
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-context": ["算数"],
                "https://w3id.org/jpXXX/assessment/grade-context": ["小学校第6学年"],
                "https://w3id.org/jpXXX/assessment/cscode-context": ["8250263111200000"],
                "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
            },        
        },
        "result": {
            "duration": "PT30S",
            "score": {
                "scaled": 0.5,
                "raw": 1,
                "max": 2
            }
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```
#### 問題への回答(未採点で得点・正誤情報を含まない)用のステートメントテンプレートの定義

- **id**: `https://w3id.org/jpXXX/assessment/template/answered-ungraded-v1`
- **inScheme (Profile version)**: `https://w3id.org/jpXXX/assessment/v1.0`
- **目的 / 用途（definition要約）**: 学習者が得点・正誤判定単位の設問に回答したことを記録する。未採点のため得点や正誤の結果情報を含まない。

### テンプレートの合致条件(Determining Properties)

| 種別 | フィールド | 値(IRI) | 説明/補足 |
|---|---|---|---|
| Verb | `verb` | `http://adlnet.gov/expapi/verbs/answered` | - |
| Context | `context.contextActivities.category[*].definition.type` | `https://w3id.org/jpXXX/assessment/activity-types/ungraded-answer` | - |


### Rules（追加の必須/禁止/許容値）

#### `$.object.definition.name.ja-jp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 問題の名前をLRPが任意に設定 | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/subject-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/grade-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/cscode-activity']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/subject-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []教科 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/grade-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学年 | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/cscode-context']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | []学習指導要領コード | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/purpose-of-question']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.object.definition.extensions['https://w3id.org/jpXXX/assessment/question-order']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.extensions['https://w3id.org/jpXXX/assessment/extension/assessment-type']`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | diagnostic/formative/summative | - |
| 4 | none | - | - |
| 5 | scopeNote | - | - |

#### `$.context.registration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 一連のAssessmentの取り組みに対して同一のGUIDを指定する | - |

#### `$.result.duration`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答所要時間 | - |

#### `$.result.response`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | recommended(含むことを推奨) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 回答値 | - |

#### `$.timestamp`

| # | 項目 | 値 | 備考 |
|---:|---|---|---|
| 1 | presence | included(必ず含む) | - |
| 2 | any | - | - |
| 3 | all | - | - |
| 4 | none | - | - |
| 5 | scopeNote | 活動の発生日時 | - |


### 補記
- 正誤情報のみあり得点情報がない場合はmaxを1とする。

### Example (最小限の場合)
```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
        "actor": {
            "objectType": "Agent",
            "account": {
                "homePage": "https://example.platform.jp",
                "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
            }
        },
        "verb": {
            "id": "http://adlnet.gov/expapi/verbs/answered",
            "display": {
                "en": "answered"
            }
        },
        "object": {
            "objectType": "Activity",
            "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        },
        "context": {
            "contextActivities": {
                "category": [
                    {
                        "id": "https://w3id.org/jpXXX/assessment/v1.0"
                    },
                    {
                        "id": "https://w3id.org/jpXXX/assessment/activities/ungraded-answer",
                        "definition": {
                            "type": "https://w3id.org/jpXXX/assessment/activity-types/ungraded-answer"
                        }
                    }
                ]
            }
        },
        "result": {
            "duration": "PT30S"
        },
        "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

### Example (recommendedをすべて含めた場合)

```json
{
    "version": "1.0.0",
    "id": "a3c9b7d1-9f4e-4b2a-8f2b-0f1a2b3c4d5e",
    "actor": {
        "objectType": "Agent",
        "account": {
            "homePage": "https://example.platform.jp",
            "name": "1fcdd088-66fc-11ec-b362-ebfd340b9cee"
        }
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/answered",
        "display": {
            "en": "answered"
        }
    },
    "object": {
        "objectType": "Activity",
        "id": "http://example.platform.jp/assessment/1234567890/question/0001",
        "definition": {
            "name": {
                "ja-jp": "次の計算をしなさい： 3/4 * 1/2"
            },
            "extensions": {
                "https://w3id.org/jpXXX/assessment/subject-activity": ["算数"],
                "https://w3id.org/jpXXX/assessment/grade-activity": ["小学校第6学年"],
                "https://w3id.org/jpXXX/assessment/cscode-activity": ["8250263111200000"],
                "https://w3id.org/jpXXX/assessment/purpose-of-question": [
                    "真分数の乗法の計算"
                ],
                "https://w3id.org/jpXXX/assessment/question-order": 1
            }
        }
    },
    "context": {
        "contextActivities": {
            "category": [
                {
                    "id": "https://w3id.org/jpXXX/assessment/v1.0"
                },
                {
                    "id": "https://w3id.org/jpXXX/assessment/activities/ungraded-answer",
                    "definition": {
                        "type": "https://w3id.org/jpXXX/assessment/activity-types/ungraded-answer"
                    }
                }
            ],
            "grouping": [
                {
                    "id": "https://example.platform.jp/b7a1f4e0-3d2e-4c5b-8f4a-2e5d6c7b8a9f"
                }
            ]
        },
        "extensions": {
            "https://w3id.org/jpXXX/assessment/subject-context": ["算数"],
            "https://w3id.org/jpXXX/assessment/grade-context": ["小学校第6学年"],
            "https://w3id.org/jpXXX/assessment/cscode-context": ["8250263111200000"],                
            "https://w3id.org/jpXXX/assessment/extension/assessment-type": "formative"
        },        
    },
    "result": {
        "duration": "PT30S"
    },
    "timestamp": "2022-03-03T04:50:03.051+00:00"
}
```

### 5.2.2 利点・課題
- 利点
  - xAPI Profileの参照先が増えない分、実装者にとって見落としが起きにくい。

- 課題
  - ログの出力制御が複雑になる分実装が重くなる。
  - 本プロファイルの公開後にこの仕様を追加する場合、本プロファイル全体のバージョンアップや実装の改修が必要となる。

---
