内容  
[1\. 本ドキュメントについて	2](#1.-本ドキュメントについて)  
[1.1 本ドキュメントの構成について	3](#1.1-本ドキュメントの構成について)  
[1.2 既存のxAPIプロファイルおよび統制語彙の参照	3](#1.2-既存のxapiプロファイルおよび統制語彙の参照)  
[1.3 本仕様の記載ルールについて	3](#1.3-本仕様の記載ルールについて)  
[2\. 共通ルール	3](#heading)  
[2.1 一般項目	3](#2.1-一般項目)  
[2.2 学習課題の学習要素に関する記述	4](#2.2-学習課題の学習要素に関する記述)  
[2.2.1 学習課題の教科・科目の指定方法	4](#2.2.1-学習課題の教科・科目の指定方法)  
[2.2.2 学習課題の単元の指定方法	4](#2.2.2-学習課題の単元の指定方法)  
[2.2.3 学習課題の学年の指定方法	4](#2.2.3-学習課題の学年の指定方法)  
[2.2.4 学習課題の構成要素（子課題）の指定方法	5](#2.2.4-学習課題の構成要素（子課題）の指定方法)  
[2.3 学習課題の指示要素に関する記述方法	5](#2.3-学習課題の指示要素に関する記述方法)  
[2.3.1 学習課題の実施期限の指定方法	5](#2.3.1-学習課題の実施期限の指定方法)  
[2.3.2 学習課題の配布対象範囲の指定方法	5](#2.3.2-学習課題の配布対象範囲の指定方法)  
[2.3.3 学習課題の学習指導要領コードの指定方法	6](#2.3.3-学習課題の学習指導要領コードの指定方法)  
[3\. 学習課題に関するユースケース	7](#3.-学習課題に関するユースケース)  
[3.1 学習課題を作成する	7](#3.1-学習課題を作成する)  
[3.2 学習課題を配布する	8](#3.2-学習課題を配布する)  
[3.3 学習課題を起動する	9](#heading-1)  
[3.4 学習課題を閲覧する	10](#heading-2)  
[3.5 学習課題を異常終了する	10](#heading-3)  
[3.6 学習課題を完了する	11](#heading-4)  
[3.7 学習課題の実施状況を初期化する	12](#heading-5)  
[3.8 学習課題を免除する	13](#heading-6)  
[3.9 学習課題成果にフィードバックする	13](#heading-7)

# **1\. 本ドキュメントについて** {#1.-本ドキュメントについて}

## 1.1 本ドキュメントの構成について {#1.1-本ドキュメントの構成について}

TBD

## 1.2 既存のxAPIプロファイルおよび統制語彙の参照 {#1.2-既存のxapiプロファイルおよび統制語彙の参照}

TBD

## 1.3 本仕様の記載ルールについて {#1.3-本仕様の記載ルールについて}

TBD  
1.4 本ドキュメントの読み方  
TBD

# **2\. 共通ルール**

## 2.1 一般項目 {#2.1-一般項目}

| type | StatementTemplate |
| ----- | :---- |
| definition | 本プロファイルに準拠するすべてのステートメントに共通する必須項目 |
| rules |  |
| location | $.id |
| presence | included |
| location | $.timestamp |
| presence | included |
| location | $.actor |
| presence | included |
| location | $.actor.objectType |
| presence | included |
| location | $.actor.account.homePage |
| presence | included |
| location | $.actor.account.name |
| presence | included |
| location | $.context |
| presence | included |
| location | $.context.language |
| presence | included |
| location | $.context.platform |
| presence | included |
| location | $.version |
| presence | included |

## 2.2 学習課題の学習要素に関する記述 {#2.2-学習課題の学習要素に関する記述}

### 2.2.1 学習課題の教科・科目の指定方法 {#2.2.1-学習課題の教科・科目の指定方法}

| type | ActivityExtension |
| :---- | :---- |
| inScheme | 学習指導要領コードor教育データ標準に準じる |
| definition | 学習課題の教科・科目名を表す文字列。 例: 国語, 算数, 理科。 |
| recommendedActivityTypes | http://adlnet.gov/expapi/activities/school-assessment |

### 2.2.2 学習課題の単元の指定方法 {#2.2.2-学習課題の単元の指定方法}

| type | ActivityExtension |
| :---- | :---- |
| inScheme | 学習指導要領コードor教育データ標準に準じる |
| definition | 学習課題が属する単元名を表す文字列。 |
| recommendedActivityTypes | http://adlnet.gov/expapi/activities/school-assessment |

### 2.2.3 学習課題の学年の指定方法 {#2.2.3-学習課題の学年の指定方法}

| type | ActivityExtension |
| :---- | :---- |
| inScheme | 学習指導要領コードor教育データ標準に準じる |
| definition | 対象学年を表す文字列。例: 5年。 |
| recommendedActivityTypes | http://adlnet.gov/expapi/activities/school-assessment |

### 2.2.4 学習課題の構成要素（子課題）の指定方法 {#2.2.4-学習課題の構成要素（子課題）の指定方法}

| type | ActivityExtension |
| :---- | :---- |
| definition | 学習課題を構成する子課題の配列。各要素はid, name, description, subject, unit を含むオブジェクトとして用いる。 |
| recommendedActivityTypes | http://adlnet.gov/expapi/activities/school-assessment |

## 2.3 学習課題の指示要素に関する記述方法 {#2.3-学習課題の指示要素に関する記述方法}

### 2.3.1 学習課題の実施期限の指定方法 {#2.3.1-学習課題の実施期限の指定方法}

| type | ContextExtension |
| :---- | :---- |
| definition | 学習課題の実施期間を示すオブジェクト。start/end プロパティを持ち、それぞれ日期文字列とする。context.extensions で使用する。 |
| recommendedVerbs | http://adlnet.gov/expapi/verbs/shared |

### 2.3.2 学習課題の配布対象範囲の指定方法 {#2.3.2-学習課題の配布対象範囲の指定方法}

| type | ContextExtension |
| :---- | :---- |
| definition | 学習課題の配布対象を表すオブジェクト。school, grade, class, student それぞれが配列として含まれ得る。 |
| recommendedVerbs | http://adlnet.gov/expapi/verbs/shared |

### 2.3.3 学習課題の学習指導要領コードの指定方法 {#2.3.3-学習課題の学習指導要領コードの指定方法}

| type | ContextExtension |
| :---- | :---- |
| definition | 文部科学省学習指導要領に基づく学習項目コードの配列。context.extensions において課題配布時などに使用する。 |
| recommendedVerbs | http://adlnet.gov/expapi/verbs/shared |

# **3\. 学習課題に関するユースケース** {#3.-学習課題に関するユースケース}

「学習課題」を次の通り定義する。  
「学習課題」とは以下のいずれかのObjectである。  
**① ”教職員”が”児童生徒”に対して行った学習活動の指示の内容を表すもの**  
**② ”児童生徒”が”自身”に対して行った学習活動の指示の内容を表すもの**

ここでの学習活動とは、それが児童生徒の学びに資すると教職員または児童生徒が考えるものすべてを指す。

学習活動の例

* 授業動画を視聴すること  
* ドリル問題に解答すること  
* テストを受けること  
* 新聞のニュースから興味のあるものを切り抜き、スクラップブックを作ること  
* 学習計画を作ること

学習課題の例

* 授業動画A,B,CをX月X日までに視聴すること（親課題）  
  * 授業動画Aを視聴すること（子課題A）  
  * 授業動画Bを視聴すること（子課題B）  
  * 授業動画Cを視聴すること（子課題C）  
* ドリル問題A,B,Cに解答し、X月X日までに正答率100％となるよう繰り返し取り組むこと  
* テストAをX月X日までに受けること  
* 新聞のニュースから興味のあるものを切り抜き、スクラップブックをX月X日までに作ること  
* 教科：aaa、単元：bbbの学習計画をX月X日までに作ること

学習課題は、学習活動要素と指示要素に分けられる。

学習活動要素：誰が、いつ、何を学ぶか。（＋その結果がどうであったか）  
指示要素：いつまでに、どこからどこまでを、超えるべき基準値は何か。

## 3.1 学習課題を作成する {#3.1-学習課題を作成する}

### 3.1.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 教職員または児童生徒が学習課題を作成したことを表すステートメント。 |
| verb | https://w3id.org/xapi/adl/verbs/created |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |
| location | $.object.definition.type |
| presence | included |
| location | $.object.definition.name\['ja-jp'\] |
| presence | recommended |
| location | $.object.definition.description\['ja-jp'\] |
| presence | recommended |

### 3.1.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "teacher-uuid-001"     }   },   "verb": {     "id": "https://w3id.org/xapi/adl/verbs/created",     "display": { "en": "created" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001",     "definition": {       "name": { "ja-jp": "理科の自由研究学習課題" },       "description": { "ja-jp": "5年生向け：水の三態について調べよう" },       "type": "http://adlnet.gov/expapi/activities/assessment",       "extensions": {         "https://example.com/xapi/extensions/grade": "5年",         "https://example.com/xapi/extensions/subject": "理科",         "https://example.com/xapi/extensions/due-date": "2025-11-15"       }     }   },   "timestamp": "2025-10-31T02:00:00.000Z" }  |
| :---- |

## 3.2 学習課題を配布する {#3.2-学習課題を配布する}

### 3.2.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 教職員が学習課題を児童生徒に配布したことを表すステートメント。 |
| verb | http://adlnet.gov/expapi/verbs/shared |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |
| location | $.object.definition.type |
| presence | included |
| location | $.object.definition.name\['ja-jp'\] |
| presence | recommended |
| location | $.object.definition.description\['ja-jp'\] |
| presence | recommended |

/\* range / due-period / mext-curriculum-code は MAY なので Rule では拘束しない \*/

### 3.2.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "teacher-uuid-001"     }   },   "verb": {     "id": "http://adlnet.gov/expapi/verbs/shared",     "display": { "en": "shared" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001",     "definition": {       "name": { "ja-jp": "理科の自由研究学習課題" },       "description": { "ja-jp": "5年生向け：水の三態について調べよう" },       "type": "http://adlnet.gov/expapi/activities/assessment",       "extensions": {         "https://example.com/xapi/extensions/grade": "5年",         "https://example.com/xapi/extensions/subject": "理科",         "https://example.com/xapi/extensions/due-date": "2025-11-15"       }     }   },   "timestamp": "2025-10-31T02:10:00.000Z" } |
| :---- |

## 3.3 学習課題を起動する

### 3.3.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 児童生徒が学習課題を起動したことを表すステートメント。 |
| verb | http://adlnet.gov/expapi/verbs/launched |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

### 3.3.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "student-uuid-001"     }   },   "verb": {     "id": "http://adlnet.gov/expapi/verbs/launched",     "display": { "en": "launched" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "timestamp": "2025-11-01T09:00:00.000Z" } |
| :---- |

## 3.4 学習課題を閲覧する

### 3.4.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 児童生徒が学習課題を閲覧したことを表すステートメント。 |
| verb | http://id.tincanapi.com/verb/viewed |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

### 3.4.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "student-uuid-001"     }   },   "verb": {     "id": "http://id.tincanapi.com/verb/viewed",     "display": { "en": "viewed" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "timestamp": "2025-11-01T09:01:00.000Z" } |
| :---- |

## 3.5 学習課題を異常終了する

### 3.5.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 児童生徒が学習課題を異常終了（放棄）したことを表すステートメント。 |
| verb | https://w3id.org/xapi/adl/verbs/abandoned |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

### 3.5.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "student-uuid-001"     }   },   "verb": {     "id": "https://w3id.org/xapi/adl/verbs/abandoned",     "display": { "en": "abandoned" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "timestamp": "2025-11-01T09:10:00.000Z" } |
| :---- |

## 3.6 学習課題を完了する

### 3.6.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 児童生徒が学習課題を完了したことを表すステートメント。 |
| verb | http://adlnet.gov/expapi/verbs/completed |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

### 3.6.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "student-uuid-001"     }   },   "verb": {     "id": "http://adlnet.gov/expapi/verbs/completed",     "display": { "en": "completed" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "timestamp": "2025-11-01T10:00:00.000Z" } |
| :---- |

## 3.7 学習課題の実施状況を初期化する

### 3.7.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 学習課題の実施状況が初期化されたことを表すステートメント。 |
| verb | http://adlnet.gov/expapi/verbs/initialized |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

### 3.7.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "student-uuid-001"     }   },   "verb": {     "id": "http://adlnet.gov/expapi/verbs/initialized",     "display": { "en": "initialized" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "timestamp": "2025-11-01T08:59:00.000Z" } |
| :---- |

## 3.8 学習課題を免除する

### 3.8.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 教職員が児童生徒の学習課題を免除したことを表すステートメント。 |
| verb | https://w3id.org/xapi/adl/verbs/waived |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

3.8.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "teacher-uuid-001"     }   },   "verb": {     "id": "https://w3id.org/xapi/adl/verbs/waived",     "display": { "en": "waived" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "timestamp": "2025-11-01T08:00:00.000Z" } |
| :---- |

## 3.9 学習課題成果にフィードバックする

### 3.9.1 プロファイル

| type | StatementTemplate |
| ----- | :---- |
| definition | 教職員が児童生徒の学習課題成果にコメントなどのフィードバックを行ったことを表すステートメント。 |
| verb | http://adlnet.gov/expapi/verbs/responded |
| objectActivityType | http://adlnet.gov/expapi/activities/school-assessment |
| rules |  |
| location | $.verb.display.en |
| presence | included |
| location | $.object.objectType |
| presence | included |
| location | $.object.id |
| presence | included |

/\* result.response / result.completion は設計書上 MAY のため Rule では拘束しない \*/

### 3.9.2 サンプルステートメント

| {   "actor": {     "objectType": "Agent",     "account": {       "homePage": "https://lms.example.jp",       "name": "teacher-uuid-001"     }   },   "verb": {     "id": "http://adlnet.gov/expapi/verbs/responded",     "display": { "en": "responded" }   },   "object": {     "objectType": "Activity",     "id": "https://lms.example.jp/assignments/1001"   },   "result": {     "response": "よく観察できていました。次は気温との関係も考えてみましょう。",     "completion": true   },   "timestamp": "2025-11-02T10:00:00.000Z" } |
| :---- |

