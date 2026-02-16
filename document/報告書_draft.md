# 効率的な統合分析・利活用に資するスタディ・ログの記述形式の調査研究（仮）

〜 日本の事業者の合意に基づく xAPI Profile群 〜

令和８年３月  
ICT CONNECT 21  
xAPI サブワーキンググループ

## 目次

1. [背景](#背景)
2. [目的](#目的)
3. [位置づけ](#位置づけ)
4. [基礎資料](#基礎資料)
5. [プロファイルドキュメントの概要](#プロファイルドキュメントの概要)
   - [5.1 Japan xAPI Core Profile](#51-japan-xapi-core-profile)
   - [5.2 Japan xAPI LMS Profile](#52-japan-xapi-lms-profile)
   - [5.3 Japan xAPI Assessment Profile](#53-japan-xapi-cbt-profile)
   - [5.4 Japan xAPI eBook Profile](#54-japan-xapi-ebook-profile)
   - [5.5 Japan xAPI Group Learning Support Tool Profile](#55-japan-xapi-group-learning-support-tool-profile)
6. [今後の課題](#今後の課題)
7. [メンバー](#メンバー)
8. [付録](#付録)

---

## 1. 背景

近年、GIGA スクール構想により全国の学校で 1 人 1 台端末の整備が急速に進み、教育現場におけるデジタル化が大きく前進している。これに伴い、学習活動の履歴情報であるスタディ・ログが多様な教育アプリケーションや学習管理システムから得られるようになり、学習状況の可視化、個別最適な学びの実現、教育改善に向けたエビデンス創出などへの活用可能性が高まっている。従来は取得が困難であった細粒度の学習データが、現在では初等中等教育段階においても収集・分析できる環境が整いつつあり、スタディ・ログの利活用は教育 DX を推進する基盤としてますます重要性を増している。

こうした中、スタディ・ログの技術標準として、米国ADLが策定し大学・企業・軍で広く採用されている xAPI（Experience API） や、米国1EdTech が策定した Caliper Analytics が注目されている。xAPI は、学習者の行動を「Actor（行為主体）」「Verb（行為）」「Object（対象）」といった構造で表すことで、学内外の多様な学習活動を統一的に記述できる枠組みを提供する。

日本国内においては、2016年度に京都大学 緒方研究室が開始した科学研究費補助金(S)の事業においてスタディ・ログ記述にxAPIを採用し、また2018年度に開始した内閣府 SIP事業においてxAPI Profile を規定しており、日本におけるスタディ・ログはxAPIを用いて記述する流れが定着した。一方、スタディ・ログに含めるべき内容に関する議論や合意形成が事業者間でなされていないのが現状である。xAPIはスタディ・ログを記述する枠組みのみを提供しており、含めるべきデータの詳細は事業者に一任されている。この状況のままスタディ・ログ活用の社会実装を進めると、複数事業者が異なる記述内容や粒度のログを出力することになる。自治体や学校がこのログを統合して分析すると、その工数が増大し、またデータ処理の専門性が求められることで、現場でのログの利活用が阻害される恐れがある。

そのため、日本の教育現場に適合する形でスタディ・ログの記述内容を整理し、事業者間で合意形成された統一的な記述形式を策定することが必要である。本報告はこうした背景を踏まえ、xAPIを用いて日本国内の事業者が共通して採用可能なスタディ・ログ記述形式を規定することで、教育データの円滑な流通と効果的な学習分析の実現を目指すものである。

## 2. 目的

本報告は上記の背景を踏まえ、日本における教育DX事業者が参加して策定した以下のxAPI Profile仕様を示すことを目的とする。

- 日本国内で流通するスタディ・ログが準拠すべき共通仕様 (Japan xAPI Core Profile)
- LMS (学習eポータル/学習管理システム) が出力するスタディ・ログが準拠すべき仕様 (Japan xAPI LMS Profile)
- CBT (Computer Based Testing) およびデジタルドリルが出力するスタディ・ログが準拠すべき仕様 (Japan xAPI Assessment Profile)
- 電子書籍 (eBook) が出力するスタディ・ログが準拠すべき仕様 (Japan xAPI eBook Profile)
- グループ学習支援ツールが出力するスタディ・ログが準拠すべき仕様 (Japan xAPI Group Learning Support Tool Profile)

## 3. 位置づけ

xAPI は、アメリカADL (Advanced Distributed Learning) が策定したスタディ・ログの記述仕様であり、スタディ・ログをJSON形式で記述し、Actor(主体)、Verb(動作)、Object(対象) などの情報を含む。

学習活動には様々な種類があり、その種類ごとにスタディ・ログに含むべき内容（Verb等）が異なるため、学習活動ごとに「どのようにProfileを書くべきか」という仕様を集約した xAPI Profile が策定されている。本報告書で定義するプロファイル群は、xAPI Profile Specification に準拠しつつ、日本の初等中等教育の実情に合わせて策定されたものである。

特に、全ドメインで共通して利用される語彙やルールを定義した「Core Profile」を基盤とし、その上に各ドメイン（LMS, Assessment, eBook, Group Learning Support Tool）ごとの詳細な仕様を定義する階層構造をとっている。これにより、ドメイン横断的なデータ分析の可能性を担保している。

## 4. 基礎資料

本報告の内容策定にあたり、以下のドキュメントおよび仕様を参照した。

- [xAPI Profile Specification](https://adlnet.github.io/xapi-profiles/xapi-profiles-structure.html)
- [ADL xAPI Profile Server](https://github.com/adlnet/xapi-authored-profiles/tree/master/Profile_Server_Profiles)
- [文部科学省 教育データ標準](https://www.mext.go.jp/a_menu/other/data_00001.htm)
- 内閣府 戦略的イノベーション創造プログラム「相互運用性を確保したペダゴジカル情報プラットフォームの研究開発・実用化検討」のための xAPI プロファイル利用に関する仕様
- 文部科学省 令和5年度教育データの利活用推進事業 報告書「CBTシステム(MEXCBT)の拡充・活用推進、教育データの利活用推進事業」〜xAPIの標準化に関する調査研究事業〜事業報告書
- 文部科学省 令和5年度教育データの利活用推進事業 プロファイルサーバー/京都大学緒方研究所プロファイルサーバー
- デジタル庁 令和5年度実証報告書「令和5年度教育関連データのデータ連携の実現に向けた実証調査研究」実証事業報告書
- デジタル庁 令和6年度実証報告書「令和6年度 スタディログの活用に関する調査研究」実証事業報告書
- EDE研究会資料 SIG1研究会「教育データ利活用のための情報基盤システムと国際技術標準」


## 5. プロファイルドキュメントの概要

### 5.1 Japan xAPI Core Profile

#### 5.1.1 概要

Japan xAPI Core Profile（以下、Core Profile）は、日本の初等中等教育における学習ログの基盤となる共通語彙（Concepts）および共通ルールを定義したプロファイルである。全体アーキテクチャにおける **Core Concept Profile** としての役割を果たし、各ドメインプロファイル（Assessment, eBook, LMS, Group-LST等）で共通利用されるConceptsを体系的に定義する。

Core Profileは **Concept（概念定義）** を主とし、Statement Template は原則として定義しない。各ドメインの具体的な学習活動パターンは、それぞれのドメインプロファイルで定義される。

主に以下の要素を提供する。

- **共通語彙 (Concepts)**:
    - **Extensions**: `grade` (学年), `subject` (教科), `course-of-study-code` (学習指導要領コード), `unit` (単元名), `difficulty` (難易度), `due-date` (期限日) など、複数のドメインで共通して利用される拡張語彙。

#### 5.1.2 プロファイルの位置づけと役割

Core Profileは、以下の階層構造において基盤を提供する：

```
┌─────────────────────────────────────┐
│     Japan xAPI Core Profile         │
│   (共通語彙・共通Extension定義)      │
└────────────┬────────────────────────┘
             │ 参照
    ┌────────┼────────┬────────┐
    │        │        │        │
┌───▼───┐ ┌─▼──┐ ┌──▼───┐ ┌──▼────────┐
│  LMS  │ │eBook│ │ CBT  │ │ Group-LST │
│Profile│ │Profile│ │Profile│ │  Profile  │
└───────┘ └─────┘ └──────┘ └───────────┘
```

この構造により、ドメイン間でのデータの一貫性と相互運用性を確保している。

#### 5.1.3 定義されるExtension一覧

Core Profileでは、学校教育の粒度（大きな枠組みから細かい要素）に従って、以下の11のExtensionを定義している：

| Extension名 | Activity | Context | 主な使用ドメイン | データ型 | 説明 |
|:---|:---:|:---:|:---|:---|:---|
| **grade** (学年) | ✓ | ✓ | 全ドメイン | array | 対象学年（文部科学省教育データ標準推奨） |
| **subject** (教科) | ✓ | ✓ | 全ドメイン | array | 学習対象の教科名 |
| **course-of-study-code** (学習指導要領コード) | ✓ | ✓ | LMS, Assessment | array | 文部科学省学習指導要領に基づく学習項目コード |
| **unit** (単元名) | ✓ | ✓ | 全ドメイン | array | 学習課題やコンテンツが属する単元名 |
| **purpose-of-question** (問題の趣旨) | ✓ | - | Assessment | array | 学習指導要領コードより細粒度の学習目標 |
| **content-type** (コンテンツの種類) | ✓ | - | Assessment | string (enum) | hint/result/explanationの種別 |
| **question-order** (問題の出題順序) | ✓ | - | Assessment | integer | デジタルドリル・CBTにおける出題順序 |
| **difficulty** (難易度) | - | ✓ | Assessment等 | string | 学習コンテンツの難易度レベル |
| **assessment-type** (評価のタイプ) | - | ✓ | Assessment | string (enum) | diagnostic/formative/summativeの種別 |
| **scrapbook-item-type** (アイテムタイプ) | ✓ | - | Group-LST | string | スクラップブック要素の種類 |
| **due-date** (期限日) | - | ✓ | LMS | date-time | 課題等の実施期限日（ISO 8601形式） |

#### 5.1.4 ActivityExtensionとContextExtensionの使い分け

Core Profileでは、同じ概念（例：subject, grade, unit）が ActivityExtension と ContextExtension の両方で使用できるように設計されている。各Extensionには詳細なScope Noteが付与され、用途を明確化している：

- **ActivityExtension**: オブジェクト（コンテンツ・課題）自体の属性を示す
  - 配置先：`$.object.definition.extensions`
  - 例：この課題が対象とする教科・学年

- **ContextExtension**: 学習活動が行われた状況や環境を示す
  - 配置先：`$.context.extensions`
  - 例：学習活動が行われた教科・学年のコンテキスト

この設計により、同じStatement内で「課題の対象学年」と「学習者の現在学年」を区別して記録することが可能になっている。

#### 5.1.5 データ型の統一と標準化

本プロジェクトでは、以下のデータ型標準化を実施した：

1. **配列型の統一**: subject, grade, unit, course-of-study-code は、単一値の場合も要素数1の配列として記録
   - 理由：複数の教科・単元にまたがる学習活動への拡張性確保
   - 例：`"subject": ["算数"]`（`"subject": "算数"` ではない）

2. **enum型の導入**: content-type と assessment-type は、許可された値のみを持つ文字列型
   - content-type: `"hint"`, `"result"`, `"explanation"`
   - assessment-type: `"diagnostic"`, `"formative"`, `"summative"`

3. **ISO 8601準拠**: due-date は国際標準の日時形式
   - 例：`"2025-11-15T23:59:59Z"`

#### 5.1.6 文部科学省教育データ標準との連携

Core Profileで定義される以下のExtensionは、文部科学省が策定する教育データ標準との整合性を考慮している：

- **subject (教科)**: 教育データ標準の教科名コード表に準拠することを推奨
- **grade (学年)**: 教育データ標準（主体情報）の「学年」項目の要素名を推奨
- **course-of-study-code (学習指導要領コード)**: 文部科学省学習指導要領コードを使用

この連携により、学習ログと既存の教育データとの統合分析が容易になる。

#### 5.1.7 ドメインプロファイルとの関係

各ドメインプロファイルは、Core Profileで定義されたExtensionを以下のように利用している：

**LMS Profile**:
- course-of-study-code, unit, subject, grade, due-date を使用
- 課題配布・提出・評価のコンテキストで活用

**Assessment Profile**:
- purpose-of-question, question-order, content-type, assessment-type を含む8つのExtensionを使用
- CBT/デジタルドリルの詳細な記録に対応

**eBook Profile**:
- Core ProfileのExtensionは使用せず、ドメイン固有のExtensionのみ定義
- 電子書籍特有の操作（ページ、しおり、注釈等）に特化

**Group-LST Profile**:
- scrapbook-item-type のみを使用
- 協働学習ツール特有のオブジェクト管理に活用

#### 5.1.8 実装時の推奨事項

Core Profile準拠のStatementを実装する際は、以下の点に留意することを推奨する：

1. **Extension配置の明確化**: ActivityとContextで用途を明確に区別する
2. **配列型の一貫性**: 単一値でも配列として記録し、将来の拡張性を確保
3. **標準コードの活用**: 教育データ標準や学習指導要領コードを積極的に使用
4. **バージョン管理**: `$.version` プロパティでxAPIバージョンを明記

#### 5.1.9 今後の展望

Core Profileは、今後も以下の観点から継続的に改善を図る予定である：

- 実装事例に基づくベストプラクティスの文書化
- Extension利用状況のモニタリングと必要に応じた追加・改訂
- 教育データ標準の更新に伴うマッピングのメンテナンス
- 新たなドメインプロファイル追加時の共通語彙の拡充

### 5.2 Japan xAPI LMS Profile

**概要**

Japan xAPI LMS Profile は、学習管理システム（LMS）および学習eポータル上での学習プロセスを記録するためのプロファイルである。
主に以下の学習活動を対象としている。

- **学習課題の作成・配布**: 教員による課題（Assessment）の作成 (`created`) および児童生徒への配布 (`shared`)。
- **学習課題の実施**: 児童生徒による課題の開始 (`launched`) および完了 (`completed`)。
- **フィードバック**: 教員による課題成果へのコメントや評価 (`responded`)。

**本プロジェクトの成果**

- 本プロファイルでは、学習課題の作成、配布、提出、評価といったLMSの基本的なワークフロー、および個々の学習活動への取り組み状況を記録するStatementTemplateを定義した。これにより、教職員が児童生徒に指示した学習課題の実施状況を追跡することが可能になり、学習支援や学習履歴の蓄積に活用できる。一方で、コース学習のような長期間にわたる学習活動や、非線形な学習パス（個別最適な学習における自由進度学習など）の複雑なパターン定義は、今回のバージョンでは対象外としている。

### 5.3 Japan xAPI Assessment Profile

**概要**

Japan xAPI Assessment Profile は、デジタルドリルやCBT（Computer Based Testing）システムにおけるアセスメント実施ログを記録するためのプロファイルである。
以下の操作を対象とする。

- **アセスメントの開始**: 学習者がドリルやテストを開始し、一連の問題に取り組み始める(`attempted`)。
- **問題への回答**: 学習者がドリルやテストの個々の問題に対して回答を行う。(`answered`)
  - 得点情報（素点、最大点、正規化スコア）、回答内容、所要時間、出題順序などを詳細に記録する。
- **コンテンツの参照**: 問題に取り組む中で、ヒントのような回答に関わるコンテンツを参照する。また、ドリルやテストの終了後、結果や解説を参照する。(`viewed`)
- **アセスメントの終了**: 学習者がドリルやテストを終了する。(`completed`)


**本プロジェクトの成果**

- 本プロファイルでは、CBT・デジタルドリルの試験開始から問題回答、結果参照にいたるまでのアセスメント実施プロセスを体系的に記録するStatementTemplateを定義した。特に問題への回答時に、得点情報（素点、最大点、正規化スコア）、回答内容、所要時間、出題順序などを詳細に記録することにより、学習者の達成度や学習パターンの詳細な追跡が可能になり、学習支援や評価に活用できる。一方で、アダプティブ・ラーニングにおける動的な出題制御（出題エンジンの挙動）やIRT(項目反応理論)の運用を考慮しての回答記録の取り扱いまではカバーしていない。また、LMS同様、非線形な回答順序に関するパターン定義は対象外としている。

### 5.4 Japan xAPI eBook Profile

**概要**

Japan xAPI eBook Profile は、デジタル教科書や教材ビューア上での閲覧行動を記録するためのプロファイルである。
以下の操作を対象とする。

- **ビューア/コンテンツの起動**: ビューア自体の起動 (`launched`) および特定書籍の閲覧開始 (`open`)。
- **ページ操作**: ページめくり等の進行 (`progressed`)。
- **インタラクション**: 拡大・縮小、設定変更 (`interacted`)。
- **注釈・書き込み**: マーカーやメモの作成 (`noted`)。

**本プロジェクトの成果**

- 本プロファイルでは、電子書籍プラットフォーム上で発生するプラットフォーム関連操作（起動・終了）、コンテンツ表示関連操作（ページ移動、目次移動）、読書行為（読書時間の記録）、注釈機能（しおり、ハイライト等）を体系的に記録するStatementTemplateを定義した。これにより、学習者の読書行動をきめ細かく追跡し、学習支援やプラットフォーム改善に活用することが可能になる。一方で、電子書籍の閲覧行動は極めて非線形であり、特定の「正解ルート」が存在しないため、行動パターンの定義（xAPI Patterns）は今回対象外とした。また、視線追跡などの生体情報との連携は含んでいない。

### 5.5 Japan xAPI Group Learning Support Tool Profile

**概要**

Japan xAPI Group Learning Support Tool Profile は、協働学習（グループワーク）支援ツールにおける相互作用を記録するためのプロファイルである。
以下の操作を対象とする。

- **ツール/コンテンツ利用**: ツールの起動、スライド等の共有コンテンツ利用開始。
- **オブジェクト作成**: 共有ホワイトボード等へのテキスト・図形配置 (`created`)。
- **議論・コミュニケーション**: 議論スレッドの作成 (`create`)、返信 (`replied`)、スタンプ/いいね (`voted-up`)。

**本プロジェクトの成果**

- 本プロファイルでは、グループ学習支援ツール内での個人の考えの作成・編集、他者への反応（いいね、コメント等）、グループでの共同編集といった操作ログを記録するStatementTemplateを定義した。これにより、グループ学習における個人の貢献度合いや相互作用の状況を追跡し、協働学習の支援や評価に活用することが可能になる。一方で、複数人が同時多発的に操作を行う同期型協働学習においては、"誰の操作によって状態が変化したか" の因果関係が複雑になるが、本プロファイルでは個々の操作ログの記録に留め、状態同期の完全な再現まではスコープとしていない。また、非線形な活動であるためパターン定義は対象外である。


## 6. 今後の課題

各プロファイル固有の課題に加え、全体として以下の共通課題が挙げられる。

1.  **メタデータの整備について**
    - 各プロファイルで参照されるメタデータ（教科、単元、評価タイプなど）について、文部科学省の教育データ標準や既存のコードセットとのマッピングを継続的にメンテナンスする必要がある。
2.  執筆中

## 7. メンバー

作業中

## 8. 付録

### 付.1 Profileの登録・公開について

#### GitHubでの機械可読ファイル公開

策定されたプロファイル（JSON-LD形式）は、バージョン管理システム（GitHub等）を用いて管理し、変更履歴を追跡可能にする。

#### URLリダイレクション (w3id.org) の設定

プロファイルのIRIは、特定のサーバーや組織に依存しない永続的なID（PURL）として設計されている。`w3id.org` によって定義されたIRIが常に最新の（あるいは指定バージョンの）仕様書の実体にリダイレクトされるよう設定を行う。

### 付.2 既存verbのIRIと定義

各ドメインプロファイルで使用している既存verbのIRIについて、定義の原文と日本語訳を併記する。
掲載順は、IRIのドメインごと、アルファベット順とする。

#### activitystrea.ms

| IRI | Definition (EN) | 日本語訳 |
| :-- | :-- | :-- |
| http://activitystrea.ms/close | Indicates that the actor has closed the object. For instance, the object could represent a ticket being tracked in an issue management system. | アクターがオブジェクトを閉じたことを示す。例えば、オブジェクトは課題管理システムで追跡されているチケットを表す場合がある。 |
| http://activitystrea.ms/delete | Indicates that the actor has deleted the object. This implies, but does not require, the permanent destruction of the object. | アクターがオブジェクトを削除したことを示す。これはオブジェクトの恒久的な破棄を含意するが、必須ではない。 |
| http://activitystrea.ms/open | Indicates that the actor has opened the object. For instance, the object could represent a ticket being tracked in an issue management system. | アクターがオブジェクトを開いたことを示す。例えば、オブジェクトは課題管理システムで追跡されているチケットを表す場合がある。 |

#### adlnet.gov

| IRI | Definition (EN) | 日本語訳 |
| :-- | :-- | :-- |
| http://adlnet.gov/expapi/verbs/answered | Indicates the actor replied to a question, where the object is generally an activity representing the question. The text of the answer will often be included in the response inside result. | アクターが質問に回答したことを示す。オブジェクトは通常その質問を表すアクティビティである。回答テキストは多くの場合、result内のresponseに含まれる。 |
| http://adlnet.gov/expapi/verbs/attempted | Indicates the actor made an effort to access the object. An attempt statement without additional activities could be considered incomplete in some cases. | アクターがオブジェクトへのアクセスを試みたことを示す。追加のアクティビティを伴わないattemptedステートメントは場合によっては不完全と見なされることがある。 |
| http://adlnet.gov/expapi/verbs/completed | Indicates the actor finished or concluded the activity normally. | アクターが活動を正常に完了した、または完了に至ったことを示す。 |
| http://adlnet.gov/expapi/verbs/initialized | Indicates the activity provider has determined that the actor successfully started an activity. | アクティビティ提供者がアクターが活動を正常に開始したと判断したことを示す。 |
| http://adlnet.gov/expapi/verbs/interacted | Indicates the actor engaged with a physical or virtual object. | アクターが物理的または仮想のオブジェクトとやり取りしたことを示す。 |
| http://adlnet.gov/expapi/verbs/launched | Indicates the actor attempted to start an activity. | アクターが活動の開始を試みたことを示す。 |
| http://adlnet.gov/expapi/verbs/progressed | Indicates a value of how much of an actor has advanced or moved through an activity. | アクターが活動内でどの程度進んだかの値を示す。 |
| http://adlnet.gov/expapi/verbs/responded | Used to indicate a user responding to a help or chat request | ヘルプまたはチャットの要求に対してユーザーが応答したことを示すために使用される。 |
| http://adlnet.gov/expapi/verbs/shared | Indicates the actor's intent to openly provide access to an object of common interest to other actors or groups. | アクターが他のアクターまたはグループに共通の関心対象へのアクセスを公開する意図を示す。 |
| http://adlnet.gov/expapi/verbs/terminated | Indicates that the actor successfully ended an activity. | アクターが活動を正常に終了したことを示す。 |

#### id.tincanapi.com

| IRI | Definition (EN) | 日本語訳 |
| :-- | :-- | :-- |
| http://id.tincanapi.com/verb/replied | The actor posted a reply to a forum, comment thread or discussion. | アクターがフォーラム、コメントスレッド、またはディスカッションに返信を投稿したことを示す。 |
| http://id.tincanapi.com/verb/viewed | Indicates that the actor has viewed the object. | アクターがオブジェクトを閲覧したことを示す。 |
| http://id.tincanapi.com/verb/voted-up | Indicates that the actor has voted up for a specific object. This is analogous to giving a thumbs up. | アクターが特定のオブジェクトに賛成票を投じたことを示す。これは「いいね」を付けることに相当する。 |

#### w3id.org

| IRI | Definition (EN) | 日本語訳 |
| :-- | :-- | :-- |
| https://w3id.org/xapi/adb/verbs/bookmarked | Persisting the current location (page) where the reader stopped the ebook activity. | 読者が電子書籍アクティビティを中断した現在位置（ページ）を保持する。 |
| https://w3id.org/xapi/adb/verbs/noted | Add annotation or notes to selected text within an ebook or highlight. | 電子書籍内の選択テキストに注釈やメモを追加する、またはハイライトする。 |
| https://w3id.org/xapi/adb/verbs/read | Indicates that the actor has read the object. | アクターがオブジェクトを読んだことを示す。 |
| https://w3id.org/xapi/adl/verbs/abandoned | Indicates the activity provider has determined that the session was abnormally terminated either by an actor or due to a system failure. | アクティビティ提供者が、アクターまたはシステム障害によりセッションが異常終了したと判断したことを示す。 |
| https://w3id.org/xapi/adl/verbs/created | Indicates the actor has created an object. | アクターがオブジェクトを作成したことを示す。 |
| https://w3id.org/xapi/adl/verbs/waived | Indicates that the learning activity requirements were met by means other than completing the activity. A waived statement is used to indicate that the activity may be skipped by the actor. | 学習アクティビティ要件が完了以外の手段で満たされたことを示す。waivedステートメントは、アクターがアクティビティをスキップできることを示すために使用される。 |
