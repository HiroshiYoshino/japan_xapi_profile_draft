ChatGPTにより生成

---

# ADR: QTI Result Reporting由来のxAPI Statement Templateを3層構造とする

## Status

Proposed

## Date

2026-05-13

## Decision

QTI Result ReportingからxAPI Statementを生成する際の標準Statement Templateを、以下の3層とする。

1. **QTI Test Result Statement**
2. **QTI Item Attempt Statement**
3. **QTI Response Variable Statement**

この3層は、QTI Result Reportingの構造における `testResult`、`itemResult`、`responseVariable` をxAPI側のStatement Templateとして明示的に対応させるものである。QTI RRの `assessmentResult` は `context` を必須、`testResult` を0または1件、`itemResult` を0件以上持つ構造であり、テスト単位・アイテム単位の結果報告を自然に表現できる。さらに、個々の回答は `responseVariable` の `candidateResponse` として表現されるため、複合設問や複数interactionを含むitemではResponse Variable単位のStatementを補助的に発行する。([IMS Global][1])

---

## Context

QTI Result Reportingは、assessmentの結果を報告するための情報モデルであり、結果データのルートである `assessmentResult` は、テストと1つ以上のitem attemptedの結果を報告できる。仕様上、`testResult` は任意であり、itemがテストに組み込まれず単独で提示される formative context も想定されている。([IMS Global][1])

`testResult` はテスト結果のコンテナであり、テスト識別子と記録日時を持つ。`testResult` が存在する場合、その後続の `itemResult` は当該テストセッションで提示対象となったitemに対応し、提示された全itemは対応する `itemResult` として報告されるべきとされている。([IMS Global][1])

`itemResult` はitem sessionの結果を表す。QTI RRでは、同じitemに対して複数の `itemResult` が出現でき、これは複数attempt、adaptive itemの進行、またはより詳細なtrackingを表す。この場合、それぞれ異なる `datestamp` を持つ必要がある。([IMS Global][1])

一方、回答値そのものは `itemResult` 配下の `responseVariable` として表現される。`responseVariable` は `identifier`、`cardinality`、`baseType`、`choiceSequence`、`scoreStatus`、`answeredStatus`、`correctResponse`、`candidateResponse` を持ち、`candidateResponse` は受験者が与えた回答である。([IMS Global][1])

QTI itemの実体では、interactionは `response-identifier` によりResponse Variableへ紐づく。たとえば `qti-choice-interaction`、`qti-inline-choice-interaction`、`qti-text-entry-interaction` などが、それぞれ `response-identifier` を持つ例がQTI BPIGに示されている。したがって、QTI RRからxAPI化する際に「interaction単位」と呼びたくなる粒度は、RRデータ上は厳密には **Response Variable単位** として扱うのが安全である。([IMS Global][2])

xAPI Statementは `actor`、`verb`、`object` を必須要素とし、結果情報は `result` に、文脈情報は `context` に格納できる。`result` には `score`、`success`、`completion`、`response`、`duration`、`extensions` が用意されており、QTI RRの得点、合否、完了、回答、所要時間、QTI固有属性を対応づけやすい。([GitHub][3])

xAPIにはInteraction Activityの表現もあり、`interactionType` として `choice`、`fill-in`、`matching`、`sequencing`、`numeric`、`other` などを使える。ただしxAPIのinteraction定義は単純化された表現であり、複雑なinteractionはActivity typeやActivity Definition extensionsで補うことが想定されている。([GitHub][3])

xAPI Profileでは、Statement Templateは「そのStatementがいつ使われ、どのデータが必要か」を定義するものとされる。したがって、QTI RR変換プロファイルとして、Test、Item Attempt、Response Variableの3つのStatement Templateを定義する。([ADL][4])

---

## Decision Details

## 1. QTI Test Result Statement

### 目的

テスト全体の結果を表すStatement。
`assessmentResult.testResult` が存在する場合に発行する。

### 発行単位

`testResult` 1件につき最大1Statement。

### 主な入力元

| xAPI field                           | QTI RR field                                             |
| ------------------------------------ | -------------------------------------------------------- |
| `actor`                              | `assessmentResult.context.sourcedId`                     |
| `verb`                               | テスト完了・採点・合否を表すverb                                       |
| `object.id`                          | `testResult.identifier` から生成したTest Activity IRI          |
| `object.definition.type`             | QTI assessment test用Activity Type                        |
| `result.score.raw`                   | test-level `outcomeVariable` の `SCORE` / `TOTAL_SCORE` 等 |
| `result.score.max`                   | `MAXSCORE` / `TOTAL_MAXSCORE` / `normalMaximum` 等        |
| `result.score.scaled`                | `raw / max` が算出可能な場合                                     |
| `result.success`                     | `masteryValue`、合否Outcome、または事前定義ルールから算出                  |
| `result.completion`                  | test completionを表すOutcomeから算出                            |
| `result.duration`                    | test-level `duration` が存在する場合                            |
| `timestamp`                          | `testResult.datestamp`                                   |
| `context.registration`               | `sessionIdentifier` から決定論的に生成したUUID                      |
| `context.contextActivities.category` | QTI-xAPI Profile Activity                                |
| `context.extensions`                 | QTI固有情報、元のsessionIdentifier、未マップOutcome等                 |

QTI RRの `Context.sourcedId` は受験者の一意識別子であり、`sessionIdentifier` は結果を生成したシステムがセッション識別のために付与するものとされる。xAPI側では、`registration` はattemptやsession、複数Activityにまたがる学習経験を表せるため、QTIセッション識別子の対応先として適している。([IMS Global][1])

### 推奨verb

標準では以下の優先順位で決定する。

1. 合否が明確に判定できる場合: `passed` / `failed`
2. 完了が明確に判定できる場合: `completed`
3. 採点結果のみを報告する場合: profile定義の `scored` または `reported`

### 備考

`testResult` が存在しないQTI RRも仕様上あり得るため、このStatementは必須発行ではない。item単独配信や小テスト以外のformative activityでは、Item Attempt Statementのみで成立させる。

---

## 2. QTI Item Attempt Statement

### 目的

item session、すなわち設問単位のattempt結果を表すStatement。
QTI RR変換の中心となるStatementである。

### 発行単位

`itemResult` 1件につき1Statement。

同一itemに複数の `itemResult` が存在する場合は、attemptごとに別Statementとして発行する。Statement IDは、少なくとも `registration`、`itemResult.identifier`、`itemResult.datestamp`、必要に応じて `sequenceIndex` を含めて決定論的に生成する。QTI RRでは、同じitemの複数結果は複数attemptやadaptive progressionを表し、それぞれ異なる `datestamp` を持つ必要があるため、この分離が自然である。([IMS Global][1])

### 主な入力元

| xAPI field                         | QTI RR field                                               |
| ---------------------------------- | ---------------------------------------------------------- |
| `actor`                            | `assessmentResult.context.sourcedId`                       |
| `verb`                             | `answered` / `attempted` / `completed` / `reported` 等      |
| `object.id`                        | item Activity IRI                                          |
| `object.definition.type`           | QTI assessment item用Activity Type                          |
| `result.score.raw`                 | item-level `outcomeVariable` の `SCORE`                     |
| `result.score.max`                 | item-level `MAXSCORE` / `normalMaximum`                    |
| `result.score.scaled`              | `raw / max` が算出可能な場合                                       |
| `result.success`                   | item-level SCORE、正誤Outcome、または採点結果から算出                     |
| `result.completion`                | `completionStatus` 等から算出                                   |
| `result.duration`                  | item-level `duration`                                      |
| `timestamp`                        | `itemResult.datestamp`                                     |
| `context.contextActivities.parent` | 対応するTest Activity                                          |
| `context.extensions`               | `sessionStatus`、`sequenceIndex`、`numAttempts`、未マップOutcome等 |

`itemResult` は `identifier`、`sequenceIndex`、`datestamp`、`sessionStatus` を持ち、配下に `itemVariable` を0件以上持つ。`itemVariable` には `numAttempts`、`duration`、`completionStatus` のような組み込み変数も含まれるため、Item Attempt Statementでは、item全体の状態・得点・完了・所要時間をまとめて表現する。([IMS Global][1])

### `result.response` の扱い

Item Attempt Statementの `result.response` は、原則として **単一の回答Response Variableのみを持つitem** の場合に限って設定してよい。

複数の回答Response Variableを持つitemでは、Item Attempt Statementの `result.response` に複数回答を無理に連結せず、Response Variable Statementへ分離する。これにより、xAPIの `result.response` が単一文字列であることによる曖昧さを避ける。

### 備考

Item Attempt Statementは、スコアリング・完了判定・item単位集計の主たる単位とする。Response Variable Statementを発行する場合でも、Item Attempt Statementは省略しない。

---

## 3. QTI Response Variable Statement

### 目的

item内の個別回答フィールド、すなわち `responseVariable` 単位の回答を表すStatement。
複合設問、複数interactionを含むitem、選択肢シャッフル、部分回答分析、回答過程の詳細分析に対応するために用意する。

### 発行単位

`itemResult` 配下の回答用 `responseVariable` 1件につき1Statement。

ただし、以下は標準ではResponse Variable Statementの発行対象外とする。

* `numAttempts`
* `duration`
* その他、回答ではなく状態・運用値を表す組み込み変数
* `candidateResponse` はあるが、学習者の回答ではなくシステム状態を表す変数

QTI RRでは `numAttempts` や `duration` も `itemVariable` として報告されるため、すべての `responseVariable` を無条件にStatement化すると、回答ではない値までinteractionとして記録してしまう。これらはItem Attempt Statementの `result.duration` や `context.extensions` に集約する。([IMS Global][1])

### 主な入力元

| xAPI field                                  | QTI RR field                                                                                 |
| ------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `actor`                                     | `assessmentResult.context.sourcedId`                                                         |
| `verb`                                      | `answered` / `responded` / `attempted` 等                                                     |
| `object.id`                                 | item Activity IRI + responseVariable identifier                                              |
| `object.definition.type`                    | `http://adlnet.gov/expapi/activities/cmi.interaction`、またはQTI response variable用Activity Type |
| `object.definition.interactionType`         | QTI interaction型から推定。推定不能なら `other`                                                          |
| `object.definition.correctResponsesPattern` | `correctResponse.value` をxAPI response patternへ変換可能な場合                                       |
| `result.response`                           | `candidateResponse.value` をxAPI response patternへ変換                                          |
| `result.completion`                         | `answeredStatus` から安全に導出可能な場合                                                                |
| `timestamp`                                 | 親 `itemResult.datestamp`                                                                     |
| `context.contextActivities.parent`          | 対応するItem Activity                                                                            |
| `context.contextActivities.grouping`        | 対応するTest Activity                                                                            |
| `context.extensions`                        | `cardinality`、`baseType`、`choiceSequence`、`scoreStatus`、`answeredStatus` 等                   |

xAPIのInteraction Activityでは、`interactionType`、`correctResponsesPattern`、選択肢等のcomponent listを表現できる。また、xAPIのresponse pattern形式はinteractionTypeごとに定義され、learner responseにも同じ形式を使うとされている。([GitHub][3])

### `result.score` と `result.success` の扱い

Response Variable Statementでは、原則として `result.score` と `result.success` は設定しない。

理由は、QTIの採点はResponse Variable単位とは限らず、複数Response Variableを組み合わせたresponse processingによってitem-level Outcomeを生成する場合があるためである。QTI BPIGでは、固定テンプレートのresponse processingと一般response processingが説明され、複雑なitem、template生成item、adaptive item、composite itemでは一般response processingが必要になるとされている。([IMS Global][2])

例外として、以下の場合はResponse Variable Statementに `result.score` または `result.success` を入れてよい。

* Response Variable単体の採点結果が明示的に存在する
* item authoring側でResponse Variableごとの部分点Outcomeが定義されている
* `outcomeVariable.variable-identifier-ref` 等により、特定Response Variableとの対応が明示されている
* プロファイルで部分採点ルールが明文化されている

なお、xAPI仕様上も、`correctResponsesPattern` と `result.response` の比較だけでsuccessを推論すべきではない。xAPIではLearning Record ConsumersはresponseとcorrectResponsesPatternの比較からsuccessを推論できないとされている。([GitHub][3])

---

## Mapping Principles

## 1. Activity IDは安定IDにする

Test、Item、Response Variableの `object.id` は、attemptごとに変わらない安定したActivity IRIとする。

例:

```text
https://example.jp/xapi/qti/tests/{testIdentifier}
https://example.jp/xapi/qti/items/{itemIdentifier}
https://example.jp/xapi/qti/items/{itemIdentifier}/response-variables/{responseIdentifier}
```

attemptや記録日時は `object.id` に埋め込まず、Statement ID、`timestamp`、`context.registration`、`context.extensions` で識別する。

xAPIではActivity IDは単一のActivityを識別し、同じIDが複数の異なるActivityを指すとStatementの妥当性に疑義が生じるため、Activity IDの安定性を保つ必要がある。([GitHub][3])

## 2. QTI固有情報はextensionsに保持する

xAPI標準フィールドに自然に入らないQTI RR情報は、無理に標準フィールドへ押し込まず、profile管理下のextensionsとして保持する。

標準extensions候補:

| Extension                 | 値                                  |
| ------------------------- | ---------------------------------- |
| `qti:sessionIdentifier`   | QTI RR `context.sessionIdentifier` |
| `qti:itemResultDatestamp` | `itemResult.datestamp`             |
| `qti:sequenceIndex`       | `itemResult.sequenceIndex`         |
| `qti:sessionStatus`       | `itemResult.sessionStatus`         |
| `qti:responseIdentifier`  | `responseVariable.identifier`      |
| `qti:cardinality`         | `responseVariable.cardinality`     |
| `qti:baseType`            | `responseVariable.baseType`        |
| `qti:choiceSequence`      | `responseVariable.choiceSequence`  |
| `qti:scoreStatus`         | `responseVariable.scoreStatus`     |
| `qti:answeredStatus`      | `responseVariable.answeredStatus`  |
| `qti:sourceResultXmlRef`  | 元QTI RRデータへの参照、必要時                 |

QTI RRの `choiceSequence` は、シャッフルされた選択肢順を受験者が経験した順序として報告するための属性である。xAPIの標準interaction componentだけでは、提示時シャッフル順と元item定義の関係を完全に表しきれない場合があるため、extension保持を標準とする。([IMS Global][1])

## 3. Profile categoryを必ず付与する

全Statementに `context.contextActivities.category` としてQTI-xAPI変換ProfileのActivityを付与する。

xAPIでは `contextActivities.category` はStatementを分類するActivityであり、xAPI profileを示す用途が明示されている。([GitHub][3])

例:

```json
{
  "context": {
    "contextActivities": {
      "category": [
        {
          "id": "https://example.jp/xapi/profiles/qti-result-reporting"
        }
      ]
    }
  }
}
```

## 4. 階層関係はcontextActivitiesで表す

Response Variable、Item、Testの関係は `context.contextActivities` で表す。

推奨:

| Statement         | object            | parent                                       | grouping                                     |
| ----------------- | ----------------- | -------------------------------------------- | -------------------------------------------- |
| Test Result       | Test              | Course / Assessment delivery context, if any | —                                            |
| Item Attempt      | Item              | Test                                         | Course / Assessment delivery context, if any |
| Response Variable | Response Variable | Item                                         | Test                                         |

xAPIでは、`parent` はStatementのObject Activityと直接関係するActivity、`grouping` はより間接的な関係、`category` はprofile等による分類に使える。([GitHub][3])

---

## Template Summary

| Template                        | 発行条件                      | 粒度           | 主な役割                      |
| ------------------------------- | ------------------------- | ------------ | ------------------------- |
| QTI Test Result Statement       | `testResult` が存在する        | テスト結果        | テスト全体の得点、合否、完了、所要時間       |
| QTI Item Attempt Statement      | `itemResult` ごと           | item attempt | 設問単位のattempt、得点、完了、正誤、状態  |
| QTI Response Variable Statement | 回答用 `responseVariable` ごと | 回答フィールド      | 複合設問・複数interaction・部分回答分析 |

---

## Consequences

### Positive

この3層構造により、QTI RRの構造を壊さずにxAPIへ変換できる。`testResult`、`itemResult`、`responseVariable` の責務が明確になるため、テスト集計、item分析、回答分析をそれぞれ別粒度で実施できる。

Item Attempt Statementを中心に据えることで、QTI RRの自然な結果単位であるitem sessionを保持できる。さらにResponse Variable Statementを追加することで、複数interactionを持つcomposite itemや、text entry、choice、inline choice、slider等を組み合わせたitemでも、回答値を曖昧にせず記録できる。

Response Variable Statementを「interaction」ではなく「response variable」として定義することで、QTI RRに直接存在しない `interactionResult` のような概念を捏造せずに済む。これは、QTI content上のinteractionが `response-identifier` でResponse Variableへ紐づく設計とも整合する。([IMS Global][2])

### Negative

Statement件数は、Test + Itemのみの方式より増える。特に複合itemでは、1つの `itemResult` から複数のResponse Variable Statementが生成される。

Response Variable Statementを正しく発行するには、単なるQTI RR XMLだけでなく、元のQTI item定義を参照してinteractionTypeを推定する必要がある場合がある。QTI RRだけでは、`responseVariable.identifier` は分かっても、それがchoice interactionなのかtext entry interactionなのかを常に確実に判断できるとは限らない。

また、Response Variable単位の `success` や `score` は原則設定しないため、細かな部分正誤分析を行う場合は、authoring時の部分点Outcomeや追加メタデータが必要になる。

---

## Alternatives Considered

## Alternative 1: Test Result Statement + Item Attempt Statementの2層のみ

### 判断

不採用。

### 理由

QTI RRの基本構造には沿うが、複数Response Variableを持つitemで `result.response` が曖昧になる。1つのitemに複数のtext entry、inline choice、matching、slider等が混在する場合、Item Attempt Statementだけでは「どの回答値がどのinteractionに対応するか」を分析しづらい。

## Alternative 2: QTI Interaction Statementを主単位にする

### 判断

不採用。

### 理由

QTI RRには `interactionResult` という直接の結果単位が存在しない。RR上で観測できる回答単位は `responseVariable` と `candidateResponse` である。そのため、interaction単位を主単位にすると、元item定義の解析に強く依存し、QTI RR単体からの変換としては不安定になる。

## Alternative 3: すべてのItemVariableをStatement化する

### 判断

不採用。

### 理由

`itemVariable` には回答だけでなく、`numAttempts`、`duration`、`completionStatus`、`SCORE`、`MAXSCORE` などの状態・Outcomeも含まれる。これらをすべてStatement化すると、学習者の行為ではない値までStatementとして記録され、ノイズが増える。状態値やOutcomeはItem Attempt Statementの `result` または `extensions` に集約する方が自然である。([IMS Global][1])

## Alternative 4: UIイベント単位のStatementを生成する

### 判断

不採用。

### 理由

QTI RRは結果報告モデルであり、クリック、フォーカス、ドラッグ、入力途中などのイベントログではない。UIイベント単位のStatementが必要な場合は、QTI RR変換とは別に、delivery engine側でイベントログ用xAPI Profileを定義する。

---

## Implementation Notes

## Statement ID

各Statement IDはUUIDv5等により決定論的に生成する。

推奨seed:

```text
Test Result:
{registration}:{testIdentifier}:{testResult.datestamp}

Item Attempt:
{registration}:{testIdentifier}:{itemIdentifier}:{itemResult.datestamp}:{sequenceIndex}

Response Variable:
{registration}:{testIdentifier}:{itemIdentifier}:{itemResult.datestamp}:{responseVariable.identifier}
```

これにより、同じQTI RRを再処理しても重複Statementを生成しにくくなる。

## Response Variableの発行対象フィルタ

標準では以下を「回答用Response Variable」とみなす。

* 元QTI item定義でinteractionの `response-identifier` から参照されている
* `candidateResponse` を持つ
* `identifier` が `numAttempts`、`duration` 等の組み込み状態値ではない
* profile設定で除外されていない

## xAPI interactionTypeへの変換

| QTI interaction例                       | xAPI `interactionType`     |
| -------------------------------------- | -------------------------- |
| `qti-choice-interaction`               | `choice`                   |
| `qti-inline-choice-interaction`        | `choice` または `likert`、用途次第 |
| `qti-order-interaction`                | `sequencing`               |
| `qti-match-interaction`                | `matching`                 |
| `qti-text-entry-interaction`           | `fill-in`                  |
| essay / extended text                  | `long-fill-in`             |
| numeric input                          | `numeric`                  |
| slider                                 | `numeric` または `other`      |
| hotspot / graphic / custom interaction | `other`                    |

変換不能または情報損失が大きい場合は、`interactionType: "other"` とし、QTI interaction typeや元response dataをextensionsに保持する。

## Scoring Updateの扱い

外部採点や人手採点がある場合でも、標準テンプレートとしては独立した第4層を設けない。
`sessionStatus = pendingExternalScoring`、`pendingResponseProcessing`、`scoreStatus = notscored` 等は、Item Attempt StatementおよびResponse Variable Statementのextensionsに保持する。

採点完了後に結果を再送する場合は、同じ3層テンプレートで新たな採点済みStatementを発行するか、運用ポリシーに応じて訂正・voiding方針を別ADRで定義する。QTI RRでは `sessionStatus` に `pendingExternalScoring` や `pendingResponseProcessing` があり、`scoreStatus` でも `notscored` / `scored` を表せるため、採点状態は3層テンプレート内で表現可能である。([IMS Global][1])

---

## Final Decision Statement

QTI RRからxAPI Statementを生成する標準Profileでは、Statement Templateを **QTI Test Result Statement、QTI Item Attempt Statement、QTI Response Variable Statement** の3層とする。

この設計では、`testResult` をテスト全体、`itemResult` をitem attempt、`responseVariable` をitem内の回答フィールドとして扱う。スコア・合否・完了は原則としてTestまたはItem層に保持し、Response Variable層は回答値、回答状態、選択肢順、正答パターン等の詳細表現を担う。これにより、QTI RRの情報モデルとxAPIのStatement/Profileモデルの両方に整合し、単純な単一設問から複合itemまで拡張可能な変換方針を標準化できる。

[1]: https://www.imsglobal.org/sites/default/files/spec/qti/v3/rr-bind/index.html "Question and Test Interoperability (QTI): Results Reporting Information Model and XSD Binding"
[2]: https://www.imsglobal.org/spec/qti/v3p0/impl "QTI v3 Best Practices and Implementation Guide | IMS Global Learning Consortium"
[3]: https://github.com/adlnet/xAPI-Spec/blob/master/xAPI-Data.md "xAPI-Spec/xAPI-Data.md at master · adlnet/xAPI-Spec · GitHub"
[4]: https://adlnet.gov/guides/xapi-profile-server/user-guide/Profiles.html "Profiles | Advanced Digital Learning Initiative"
