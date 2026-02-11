

ebookに関する

xAPIプロファイル標準仕様（案）

2026年2月5日版

# 

# 目次 {#目次}

[**目次	1**](#目次)

[**1.　本ドキュメントについて	5**](#1.　本ドキュメントについて)

[1.1　位置づけ	5](#1.1　位置づけ)

[1.2　目的	5](#1.2　目的)

[1.3　前提条件	5](#1.3　前提条件)

[1.4　定義範囲	6](#1.4　定義範囲)

[**2.　本ドキュメントの構成について	7**](#2.　本ドキュメントの構成について)

[2.1　構成要素	7](#2.1　構成要素)

[**3.　メタ情報	8**](#3.　メタ情報)

[3.1　本章の位置づけ	8](#3.1　本章の位置づけ)

[3.2　構成要素	8](#3.2　構成要素)

[**4.　concepts	9**](#4.　concepts)

[4.1　本章の位置づけ	9](#4.1　本章の位置づけ)

[4.2　対象	9](#4.2　対象)

[4.3　前提条件	9](#4.3　前提条件)

[4.4　Verb	9](#4.4　verb)

[　4.4.1 Verbの定義	9](#　4.4.1-verbの定義)

[　4.4.2 電子書籍（ebook）におけるVerbの整理方針	9](#　4.4.2-電子書籍（ebook）におけるverbの整理方針)

[　4.4.3 電子書籍（ebook）におけるVerb一覧	9](#　4.4.3-電子書籍（ebook）におけるverb一覧)

[　4.4.3.1 launched	9](#　4.4.3.1-launched)

[　4.4.3.2 terminated	10](#　4.4.3.2-terminated)

[　4.4.3.3 opened	10](#　4.4.3.3-opened)

[　4.4.3.4 closed　	10](#　4.4.3.4-closed　)

[　4.4.3.5 read	10](#　4.4.3.5-read)

[　4.4.3.6 completed　	11](#　4.4.3.6-completed　)

[　4.4.3.7 noted	11](#　4.4.3.7-noted)

[　4.4.3.8 highlighted	11](#　4.4.3.8-highlighted)

[　4.4.3.9 bookmarked	11](#　4.4.3.9-bookmarked)

[　4.4.3.10 delated	12](#　4.4.3.10-delete)

[　4.4.3.11 progressed	12](#　4.4.3.11-progressed)

[　4.4.3.12 interacted	12](#　4.4.3.12-interacted)

[4.5　ActivityType	13](#4.5　activitytype)

[　4.5.1 ActivityTypeの定義	13](#　4.5.1-activitytypeの定義)

[　4.5.2 電子書籍（ebook）におけるActivityTypeの整理方針	13](#　4.5.2-電子書籍（ebook）におけるactivitytypeの整理方針)

[　4.5.3 電子書籍（ebook）におけるActivityType一覧	13](#　4.5.3-電子書籍（ebook）におけるactivitytype一覧)

[　4.5.3.1 viewer	13](#　4.5.3.1-viewer)

[　4.5.3.2 content	13](#　4.5.3.2-content)

[　4.5.3.3 page	14](#　4.5.3.3-page)

[　4.5.3.4 bookmark	14](#　4.5.3.4-bookmark)

[　4.5.3.5 annotation	14](#　4.5.3.5-annotation)

[　4.5.3.6 settings	15](#　4.5.3.6-settings)

[4.6　ContextExtension	15](#4.6　contextextension)

[　4.6.1　ContextExtensionの定義	15](#　4.6.1　contextextensionの定義)

[　4.6.2　電子書籍（ebook）におけるContextExtensionの整理方針	15](#　4.6.2　電子書籍（ebook）におけるcontextextensionの整理方針)

[　4.6.3　電子書籍（ebook）におけるContextExtension一覧	15](#　4.6.3　電子書籍（ebook）におけるcontextextension一覧)

[**5.　StatementTemplate	16**](#5.　statementtemplate)

[5.1　本章の位置づけ	16](#5.1　本章の位置づけ)

[5.2　前提条件	16](#5.2　前提条件)

[5.3　StatementTemplate一覧	17](#5.3　statementtemplate一覧)

[5.3.1　プラットフォームの起動	17](#5.3.1　プラットフォームの起動)

[5.3.1.1　基本仕様	17](#5.3.1.1　基本仕様)

[5.3.1.2　記述規則（Rules）	17](#5.3.1.2　記述規則（rules）)

[5.3.1.3　Markdownテーブル	17](#5.3.1.3　markdownテーブル)

[5.3.2　プラットフォームの終了	18](#5.3.2　プラットフォームの終了)

[5.3.2.1　基本仕様	18](#5.3.2.1　基本仕様)

[5.3.2.2　記述規則（Rules）	18](#5.3.2.2　記述規則（rules）)

[5.3.2.3　Markdownテーブル	18](#5.3.2.3　markdownテーブル)

[5.3.3　コンテンツの利用開始	19](#heading=h.cr47m5fvs8nd)

[5.3.3.1　基本仕様	19](#heading=h.7vzmwdppd8xp)

[5.3.3.2　記述規則（Rules）	19](#heading=h.qls5dme1fbzp)

[5.3.3.3　Markdownテーブル	19](#heading=h.ax8lu8ss7mya)

[5.3.4　コンテンツの利用終了	21](#heading=h.jpta18f97tww)

[5.3.4.1　基本仕様	21](#heading=h.sev4qojbxa8h)

[5.3.4.2　記述規則（Rules）	21](#heading=h.5xpi09h424j)

[5.3.4.3　Markdownテーブル	21](#heading=h.7dixaw5aehyv)

[5.3.5　コンテンツの表示	23](#5.3.5　コンテンツの表示)

[5.3.5.1　基本仕様	23](#5.3.5.1　基本仕様)

[5.3.5.2　記述規則（Rules）	23](#5.3.5.2　記述規則（rules）)

[5.3.3.3　Markdownテーブル	23](#5.3.3.3　markdownテーブル)

[5.3.6　コンテンツの非表示	24](#5.3.6　コンテンツの非表示)

[5.3.6.1　基本仕様	24](#5.3.6.1　基本仕様)

[5.3.6.2　記述規則（Rules）	24](#5.3.6.2　記述規則（rules）)

[5.3.6.3　Markdownテーブル	24](#5.3.6.3　markdownテーブル)

[5.3.〇　コンテンツの精読	25](#5.3.〇　読書行動)

[5.3.〇.1　基本仕様	25](#5.3.〇.1　基本仕様)

[5.3.〇.2　記述規則（Rules）	25](#5.3.〇.2　記述規則（rules）)

[5.3.3.3　Markdownテーブル	25](#5.3.3.3　markdownテーブル-1)

[5.3.7　ページ移動	26](#heading=h.32o4y6acv9lb)

[5.3.7.1　基本仕様	26](#5.3.●.1　基本仕様)

[5.3.7.2　記述規則（Rules）	26](#5.3.●.2　記述規則（rules）)

[5.3.7.3　Markdownテーブル	26](#5.3.●.3　markdownテーブル)

[5.3.8　目次移動	28](#heading=h.p3bt0edolw0i)

[5.3.8.1　基本仕様	28](#heading=h.xzjq0tckkpe0)

[5.3.8.2　記述規則（Rules）	28](#heading=h.oiu90b25h7hf)

[5.3.8.3　Markdownテーブル	28](#heading=h.h2bp35pn8oau)

[5.3.9　縦ローリング	29](#5.3.9　縦ローリング)

[5.3.9.1　基本仕様	29](#5.3.9.1　基本仕様)

[5.3.9.2　記述規則（Rules）	29](#5.3.9.2　記述規則（rules）)

[5.3.9.3　Markdownテーブル	29](#5.3.9.3　markdownテーブル)

[5.3.10　横ローリング	30](#5.3.10　横ローリング)

[5.3.10.1　基本仕様	30](#5.3.10.1　基本仕様)

[5.3.10.2　記述規則（Rules）	30](#5.3.10.2　記述規則（rules）)

[5.3.10.3　Markdownテーブル	30](#5.3.10.3　markdownテーブル)

[5.3.11　リフロー遷移	31](#5.3.11　リフロー遷移)

[5.3.11.1　基本仕様	31](#5.3.11.1　基本仕様)

[5.3.11.2　記述規則（Rules）	31](#5.3.11.2　記述規則（rules）)

[5.3.11.3　Markdownテーブル	31](#5.3.11.3　markdownテーブル)

[5.3.12　しおり追加	32](#5.3.12　しおり追加)

[5.3.12.1　基本仕様	32](#5.3.12.1　基本仕様)

[5.3.12.2　記述規則（Rules）	32](#5.3.12.2　記述規則（rules）)

[5.3.12.3　Markdownテーブル	32](#5.3.12.3　markdownテーブル)

[5.3.13　しおり削除	33](#5.3.13　しおり削除)

[5.3.13.1　基本仕様	33](#5.3.13.1　基本仕様)

[5.3.13.2　記述規則（Rules）	33](#5.3.13.2　記述規則（rules）)

[5.3.13.3　Markdownテーブル	33](#5.3.13.3　markdownテーブル)

[5.3.14　ペン書き込み	34](#5.3.14　ペン書き込み)

[5.3.14.1　基本仕様	34](#5.3.14.1　基本仕様)

[5.3.14.2　記述規則（Rules）	34](#5.3.14.2　記述規則（rules）)

[5.3.14.3　Markdownテーブル	34](#5.3.14.3　markdownテーブル)

[5.3.15　ペン書き込み削除	35](#5.3.15　ペン書き込み削除)

[5.3.15.1　基本仕様	35](#5.3.15.1　基本仕様)

[5.3.15.2　記述規則（Rules）	35](#5.3.15.2　記述規則（rules）)

[5.3.14.3　Markdownテーブル	35](#5.3.14.3　markdownテーブル-1)

[5.3.16　線分書き込み	36](#5.3.16　線分書き込み)

[5.3.16.1　基本仕様	36](#5.3.16.1　基本仕様)

[5.3.16.2　記述規則（Rules）	36](#5.3.16.2　記述規則（rules）)

[5.3.16.3　Markdownテーブル	36](#5.3.16.3　markdownテーブル)

[5.3.17　線分書き込み削除	37](#5.3.17　線分書き込み削除)

[5.3.17.1　基本仕様	37](#5.3.17.1　基本仕様)

[5.3.17.2　記述規則（Rules）	37](#5.3.17.2　記述規則（rules）)

[5.3.17.3　Markdownテーブル	37](#5.3.17.3　markdownテーブル)

[5.3.18　一括削除	38](#5.3.18　一括削除)

[5.3.18.1　基本仕様	38](#5.3.18.1　基本仕様)

[5.3.18.2　記述規則（Rules）	38](#5.3.18.2　記述規則（rules）)

[5.3.18.3　Markdownテーブル	38](#5.3.18.3　markdownテーブル)

[5.3.19　拡大	39](#5.3.19　拡大)

[5.3.19.1　基本仕様	39](#5.3.19.1　基本仕様)

[5.3.19.2　記述規則（Rules）	39](#5.3.19.2　記述規則（rules）)

[5.3.19.3　Markdownテーブル	39](#5.3.19.3　markdownテーブル)

[5.3.20　縮小	40](#5.3.20　縮小)

[5.3.20.1　基本仕様	40](#5.3.20.1　基本仕様)

[5.3.20.2　記述規則（Rules）	40](#5.3.20.2　記述規則（rules）)

[5.3.20.3　Markdownテーブル	40](#5.3.20.3　markdownテーブル)

[5.3.21　背景色の変更	41](#5.3.21　背景色の変更)

[5.3.21.1　基本仕様	41](#5.3.21.1　基本仕様)

[5.3.21.2　記述規則（Rules）	41](#5.3.21.2　記述規則（rules）)

[5.3.21.3　Markdownテーブル	41](#5.3.21.3　markdownテーブル)

[5.3.22　文字色の変更	42](#5.3.22　文字色の変更)

[5.3.22.1　基本仕様	42](#5.3.22.1　基本仕様)

[5.3.22.2　記述規則（Rules）	42](#5.3.22.2　記述規則（rules）)

[5.3.22.3　Markdownテーブル	42](#5.3.22.3　markdownテーブル)

# 

# 1.　本ドキュメントについて {#1.　本ドキュメントについて}

## 1.1　位置づけ {#1.1　位置づけ}

　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つである電子書籍（ebook）における学習ログを対象として取りまとめたebook xAPIプロファイル標準仕様（案）である。  
　本仕様は、文部科学省が令和5年3月に策定した「デジタル教科書標準仕様書」に記載されている「別紙3 プラットフォーム機能一覧」を踏まえ、電子書籍プラットフォーム上で発生する操作、読書行動、注釈および表示設定の変更等に関する学習ログを体系的に記録するための仕様である。

## 1.2　目的 {#1.2　目的}

　本ドキュメントは、電子書籍（ebook）における学習ログについて、関係する事業者間で共通の理解のもとに取り扱うことを可能とするため、ebook xAPIプロファイルとしての考え方および記述の枠組みを整理し、共有することを目的とする。

## 1.3　前提条件 {#1.3　前提条件}

　本ドキュメントにおける各ユースケースは、xAPIプロファイル仕様で定義されているStatementTemplateおよびStatementTemplateRulesの構造および考え方に準拠して記載する。  
　各ユースケースに付随するStatementTemplate要素表には、StatementTemplateを構成する要素を示している。ただし、actorについては全ユースケース共通でAgentとするため、各ユースケースの規範表への個別の記載は行わないものとする。  
　本ドキュメントは、電子書籍（ebook）における学習ログの標準的な解釈および  
実装方針を読み手が理解しやすい形で示すことを主目的とした仕様書である。このため、xAPIプロファイル仕様上は必須である項目のうち、機械処理やプロファイル登録といった運用段階において主に必要となる項目については、本書の目的に照らし記載を省略する。各項目の省略理由は下記に示すとおりである。

* idに期待されるURI    
  * 省略理由：idはStatementTemplateをグローバルに一意に識別するためのURI を指定する項目であり、プロファイルの公開形態、管理主体、バージョニング方針が確定した段階で設計されるべきものである。本ドキュメントは標準仕様（案）としての整理および合意形成を目的としているため、現時点では具体的なURIの定義は行わない。  
* typeに期待される固定値StatementTemplate    
  * 省略理由：typeに指定される固定値StatementTemplateは、JSON-LD形式における機械可読性を担保するための項目である。本ドキュメントでは、読み手による理解を前提とした仕様書として、StatementTemplateの構造および位置づけを章構成および見出しによって明示しているため、当該項目は省略する。  
* inSchemaに期待されるURI   
  * 省略理由：inSchemaは、当該StatementTemplateが属するプロファイルおよびバージョンをURIにより示すための項目である。本ドキュメントでは、プロファイルの名称およびバージョン管理を文書構成および章立てにより管理していることから、inSchemaによる明示的な指定は行わない  
* prefLabel    
  * 省略理由：prefLabelはStatementTemplateに対する人可読な名称を付与するための項目である。本ドキュメントでは、各ユースケースを章・節の見出し（項目名）として明示しており、これをもって当該StatementTemplateを識別可能とするため、prefLabel の記載は省略する。  
    

　なお、これらの項目については、将来的にプロファイルの登録や機械可読な形式での提供が必要となる場合に、改めて検討することとする。

## 1.4　定義範囲 {#1.4　定義範囲}

　本ドキュメントは、電子書籍（ebook）のxAPIプロファイルを構成する要素のうち、メタ情報、concepts、Rulesおよび各操作行動に対応するStatementTemplateを定義することを目的とする。  
　ただし、電子書籍（ebook）の閲覧行動が非線形である特性を踏まえ、xAPIプロファイルにおける patternsは定義の対象外とする。  
　本ドキュメントに加え、実装者がxAPI Statementを正しく生成できるよう、理解および実装を補助する目的で、本ドキュメントで定義したユースケースのStatementTemplateに対応するJSON形式のStatementの例を別紙（仮名）として示す。

# 2.　本ドキュメントの構成について {#2.　本ドキュメントの構成について}

## 2.1　構成要素 {#2.1　構成要素}

　本ドキュメントは、本紙と別紙の2部構成で整理されている。  
　本紙は、xAPIプロファイル仕様に基づき、電子書籍（ebook）学習ログに関する標準的な解釈および実装方針を示すことを目的とする。本紙は、以下の要素を含む。

* メタ情報：プロファイル全体のメタ情報およびバージョン管理  
* Concepts：xAPI VerbやActivityType などの概念定義  
* Rules：StatementTemplateの検証規則  
* StatementTemplate：各ユースケースに対応するStatementTemplateの構造および必須要素

　別紙は、本紙で定義したStatementTemplateに基づき、実装者がxAPI Statementを生成する際の理解を補助することを目的とする。別紙には各ユースケースのStatementTemplateに対応するJSON形式のStatement例を示す。

　

# 3.　メタ情報 {#3.　メタ情報}

## 3.1　本章の位置づけ {#3.1　本章の位置づけ}

　本章では、本プロファイルを識別・管理するために必要なメタ情報を示す。  
　メタ情報は、StatementTemplateやConceptsの内容そのものではなく、プロファイル全体の情報として参照される項目である。　

## 3.2　構成要素 {#3.2　構成要素}

　プロファイルのメタ情報を構成する要素を示す。なお、本ドキュメントはxAPIプロファイル標準仕様（案）であるため、メタ情報の内容は仮置きであり、今後変更される可能性がある。

| 項目 | 説明 | 値 |
| :---- | :---- | :---- |
| プロファイル名 | プロファイルを識別する名称 | 電子書籍学習ログ xAPIプロファイル |
| バージョン | プロファイルの改訂番号やリリース状態 | v1.0 |
| 作成者/管理者 | プロファイルの作成者や責任者 | ICT CONNECT 21 |
| 作成日/更新日 | 文書化日または改訂日 | 2026年1月×日 |
| 言語 | メタ情報およびプロファイルの記載言語 | 日本語 |
| 目的/説明 | プロファイルが対象とする学習ログや用途 | 電子書籍プラットフォーム操作や読書行動を標準的に記録することを目的とする |

### 

## 

## 

# 4.　concepts {#4.　concepts}

## 4.1　本章の位置づけ {#4.1　本章の位置づけ}

　本章では、電子書籍（ebook）向け xAPIプロファイルにおいて使用されるconceptsを定義する。conceptsは、StatementTemplateから参照される共通定義であり、単体で xAPI Statementを構成するものではない。

## 4.2　対象 {#4.2　対象}

　conceptsの対象は、Verb、ActivityType、ContextExtensionの3項目とする。

## 4.3　前提条件 {#4.3　前提条件}

　本章に示す各 Conceptの定義（definition）は、当該 Conceptの見出し直下に記載するものとする。  
　本プロファイルでは、ADL または xAPI Communityにより既に定義されている語彙については、意味的な齟齬がない限り、それらをそのまま利用することとする。また、電子書籍（ebook）特有の操作や表現形式に依存する行為についてのみ、本プロファイル独自のVerbを定義する。外部プロファイルで既に定義されている語彙を参照する場合、本ドキュメントでは可読性向上を目的として、その概要情報を参考として記載することがある。これらは正式な xAPI Profile 仕様上の再定義を意図するものではない。

## 4.4　Verb {#4.4　verb}

### **　**4.4.1 Verbの定義 {#　4.4.1-verbの定義}

　　Verb は、学習者または利用者が電子書籍（ebook）上で行った操作行動の意味を定義する概念要素である。  
　xAPI StatementにおいてVerbは「何をしたか」を表す中核要素であり、特定の画面構成や実装方式に依存しない、行為そのものの意味語彙を提供する。

### 　4.4.2 電子書籍（ebook）におけるVerbの整理方針 {#　4.4.2-電子書籍（ebook）におけるverbの整理方針}

　　本プロファイルにおけるVerbは、以下の方針に基づき整理する。

* 電子書籍（ebook）において一般的に発生する操作行動を表すものを対象とする  
* 学習者の意図や結果ではなく、観測可能な操作行為を表す  
* 既存のxAPI語彙を優先的に利用する  
* Verbに対応する用途事例や備考を記載する


### 　4.4.3 電子書籍（ebook）におけるVerb一覧 {#　4.4.3-電子書籍（ebook）におけるverb一覧}

#### 　**4.4.3.1 launched** {#　4.4.3.1-launched}

* アクティビティを開始しようとしたことを示す。  
* 用途事例  
  * プラットフォームの利用開始  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://adlnet.gov/expapi/verbs/launched |

#### **　4.4.3.2 terminated** {#　4.4.3.2-terminated}

* アクティビティを正常に終了したことを示す。  
* 用途事例  
  * プラットフォームの利用終了  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://adlnet.gov/expapi/verbs/terminated |

#### **　4.4.3.3 opened** {#　4.4.3.3-opened}

* オブジェクトを開いたことを示す。  
* 用途事例  
  * コンテンツの表示開始  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/open |

#### **　4.4.3.4 closed**　 {#　4.4.3.4-closed　}

* オブジェクトを閉じたことを示す。  
* 用途事例  
  * コンテンツの表示終了  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/close |

#### **　4.4.3.5 read** {#　4.4.3.5-read}

* オブジェクトを読んだことを示す。  
* 用途事例  
  * 読書（精読）の開始  
  * 読書（精読）の終了  
* 備考  
  * コンテンツの特定範囲（ページ、章など）を学習対象として閲覧したことを記録するために用いる  
  * 単なる操作ではなく、「読書・学習」という認知的活動が発生したとみなされる場合に使用する  
  * 画面が同一画面内で2秒以上静止または低速移動していること  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/read |

#### **　4.4.3.6 completed**　 {#　4.4.3.6-completed　}

* アクティビティを正常に完了または終了したことを示す。  
* 用途事例  
  * コンテンツの読了  
* 備考  
  * 物理的な画面終了や離脱を意味するものではない  
  * プラットフォームの終了（terminated）や画面遷移によるコンテンツの表示終了（closed）と区別すること  
  * 読み飛ばしや中断ではなく、読了とみなせる行為に対して使用する  
  * 完了時点の位置情報（ページ番号等）はcontext/result extensionsで補足する  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://adlnet.gov/expapi/verbs/completed |

#### **　4.4.3.7 noted** {#　4.4.3.7-noted}

* メモ（注釈）したことを示す。  
* 用途事例  
  * ペン書き込み  
  * ページ上への線分描画  
* 備考  
  * notedの行為の削除を示す際は、object.definition.extensionsのoperation\_nameで表現する  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | https://w3id.org/xapi/adb/verbs/noted |

#### **　4.4.3.8 highlighted** {#　4.4.3.8-highlighted}

* 重要な部分をハイライトしたことを示す。  
* 用途事例  
  * ハイライトの追加  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | https://w3id.org/xapi/adb/verbs/highlighted |

#### **　4.4.3.9 bookmarked** {#　4.4.3.9-bookmarked}

* 電子書籍内にしおりを追加したことを示す。  
* 用途事例  
  * ページにしおりを設定  
* 備考  
  * 縦置き1ページ表示（layoutPortrait）とは区別する  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | https://w3id.org/xapi/adb/verbs/bookmarked |

#### **　4.4.3.10 delete** {#　4.4.3.10-delete}

* 電子書籍上の注釈・描画・しおりを削除したことを示す。  
* 用途事例  
  * ペン書き込み削除  
  * ページ上の線分描画の削除  
  * ページ上の全書き込みを削除  
  * ページに設定済みのしおりの削除

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/delete |

#### 　**4.4.3.11 progressed** {#　4.4.3.11-progressed}

* 電子書籍内での位置移動を示す。  
* 用途事例  
  * ページ送り、戻り、特定ページへの遷移  
  * ページ間の学習進行状況の記録  
  * 目次から特定章への遷移  
  * 章、節間の遷移  
* 備考  
  * 学習の非線形性を把握するための行動ログに利用  
  * ページ移動はobject（page）で識別する  
  * ページ単位の移動に対応する

| 項目 | 値 |
| :---- | :---- |
| id | http://adlnet.gov/expapi/verbs/progressed |

#### 　**4.4.3.12 interacted** {#　4.4.3.12-interacted}

* 電子書籍内の表示形式・閲覧設定の変更を示す。  
* 用途事例  
  * 縦ローリング  
  * 横ローリング  
  * リフロー遷移  
  * ページ拡大  
  * ページ縮小  
  * 背景色の変更  
  * 文字色の変更  
* 備考  
  * 変更箇所・内容はobject（page）で識別する  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://adlnet.gov/expapi/verbs/interacted |

## 4.5　ActivityType {#4.5　activitytype}

### 　4.5.1 ActivityTypeの定義 {#　4.5.1-activitytypeの定義}

　　ActivityTypeは、Statementにおいてobjectとして参照されるActivityが、どのような種類のリソースであるかを示す概念である。また、StatementTemplateのobjectTypeがActivityに指定される際に参照される。

### 　4.5.2 電子書籍（ebook）におけるActivityTypeの整理方針 {#　4.5.2-電子書籍（ebook）におけるactivitytypeの整理方針}

　　本プロファイルにおけるActivityTypeは、以下の方針に基づき整理する。

* 各StatementTemplateにおいてobjectとして参照される対象ごとにActivityTypeを定義する  
* プラットフォーム単位の操作とコンテンツ単位の操作を明確に区別し、同一ActivityTypeに複数の用途を混在させない  
* ActivityTypeはURI により一意に識別される  
* ActivityTypeの定義にあたっては、ADLが公式に定義しているActivityType や、  
  ActivityStreamsなどで広く利用されている既存の語彙を優先的に採用する  
* 既存のActivityTypeと意味的に整合する場合は、独自定義を行わず、既存の URI をそのまま利用する  
* 電子書籍（ebook）固有の対象であり、既存語彙では適切に表現できない場合に限り、本プロファイル独自のActivityTypeを定義する  
* 必要に応じて用途事例や備考を付与し、実装者がStatementを正しく生成できるよう補足情報を提供する


### 　4.5.3 電子書籍（ebook）におけるActivityType一覧 {#　4.5.3-電子書籍（ebook）におけるactivitytype一覧}

#### **　4.5.3.1 viewer** {#　4.5.3.1-viewer}

* 電子書籍プラットフォーム自体に対する操作や状態を示す。  
* 用途事例  
  * プラットフォームの起動  
  * プラットフォームの終了  
* 備考  
  * アプリ自体の利用時間を計測する際に使用する  
  * 特定の書籍内容に依存しないシステムレベルの操作を対象とする  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | https://w3id.org/xapi/ebook/activity-types/viewer |

#### **　4.5.3.2 content** {#　4.5.3.2-content}

* 電子書籍コンテンツ（書籍全体）または章・節などの構造単位を示す。  
* 用途事例  
  * コンテンツの利用開始  
  * コンテンツの利用終了  
  * 読書の開始  
  * 読書の終了  
* 備考  
  * 書籍全体、または章・節といった構造単位に関わる操作を対象とする  
  * ページ送りなど、ページ単位で意味を持つ移動はpage ActivityTypeで扱う  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/book |

#### **　4.5.3.3 page** {#　4.5.3.3-page}

* 電子書籍内の特定のページ（物理的または論理的な最小単位）を示す。  
* 用途事例  
  * ページ移動  
  * 目次移動  
  * 縦ローリング  
  * 横ローリング  
  * リフロー遷移  
* 備考  
  * 学習者が今どこを見ているか、という位置情報を特定するために使用する  
  * リフロー型コンテンツの場合は、表示領域の識別に用いる  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/page |

#### **　4.5.3.4 bookmark** {#　4.5.3.4-bookmark}

* 特定のページに対して付与される「しおり」というオブジェクトを指す。  
* 用途事例  
  * しおりの追加  
  * しおりの削除  
* 備考  
  * ページそのものではなく、ユーザーが後で参照するために作成した目印を対象とする  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/bookmark |

#### **　4.5.3.5 annotation** {#　4.5.3.5-annotation}

* 学習者が電子書籍上に追加したテキストメモ、注釈、または手書きの描画要素を示す。  
* 用途事例  
  * ペン書き込み  
  * 線分書き込み  
  * 削除  
  * 一括削除  
* 備考  
  * テキスト注釈か描画かの区別は、必要に応じてExtensionsで補足する  
  * 個別削除と一括削除の区別も同様にExtensionsで補足する  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | http://activitystrea.ms/schema/1.0/note |

#### **　4.5.3.6 settings** {#　4.5.3.6-settings}

* プラットフォームの表示設定や閲覧環境の状態を指す。  
* 用途事例  
  * 拡大  
  * 縮小  
  * 背景色の変更  
  * 文字色の変更  
* 備考  
  * コンテンツの「内容」ではなく、ユーザーの「見やすさ」に関するカスタマイズ行為を対象とする  
  * 設定変更の結果（具体的な色や拡大率など）は、Result Extensions等に記録する  
* 識別情報

| 項目 | 値 |
| :---- | :---- |
| id | https://w3id.org/xapi/ebook/activity-types/settings |

## 4.6　ContextExtension {#4.6　contextextension}

### 　4.6.1　ContextExtensionの定義 {#　4.6.1　contextextensionの定義}

　　ContextExtensionはStatementのcontext.extensions配下で利用され、学習行動の詳細情報や補助情報を提供する。

### 　4.6.2　電子書籍（ebook）におけるContextExtensionの整理方針 {#　4.6.2　電子書籍（ebook）におけるcontextextensionの整理方針}

　　本プロファイルにおけるContextExtensionは、以下の方針に基づき整理する。

* 各StatementTemplate において、行動や対象に関連する追加情報を表すために定義する  
* ContextExtensionはURIにより一意に識別される  
* 値の語彙や型はプロファイル内で一貫性を持つ  
* 値の候補や特定の状況下での使用上の注意点を記載し、Statement生成時の誤用を防止する  
* すべてのContextExtensionは必須ではなく、StatementTemplateのrulesに従い presenceを指定することで実装上の取扱いを明確化する

### 　4.6.3　電子書籍（ebook）におけるContextExtension一覧 {#　4.6.3　電子書籍（ebook）におけるcontextextension一覧}

　　※各StatementTemplate内容を検討後に策定予定のため未作成

# 

# 5.　StatementTemplate {#5.　statementtemplate}

## 5.1　本章の位置づけ {#5.1　本章の位置づけ}

　本章では、電子書籍プロファイルにおける各操作のデータ構造を定義する。各テンプレートは以下の「基本仕様」および「記述規則」の構成で記述される。　

## 5.2　前提条件 {#5.2　前提条件}

* 基本仕様  
  * 冒頭にdifinitionの位置づけとして、Templateの目的やどのような操作を記録するためのものかを定義する。  
  * 識別情報  
    * Templateを管理上特定するための情報として3要素（id,inScheme,prefLabel）を含む。  
  * 判定条件  
    * 受信したStatementがどのTemplateに該当するかを自動判別するための固定値（Verb,objectActivityType）を示す。  
* 記述規則（Rules）  
  * Statement内の各プロパティに対する制約を示す。以下の要素を含む。  
    * データの所在（location）: JSONPath方式で記述されるデータの位置。  
    * presence：included（必須）、recommended（推奨）、optional（任意）のいずれか1つ。  
    * ScopeNoteの内容に基づいた値の定義や運用上の注意点。  
* Markdownテーブルの構成  
  * 各Templateの末尾には、システム設計・実装時に参照しやすいよう、記述規則（Rules）を一覧化したテーブルを配置する。

## 

## 5.3　StatementTemplate一覧 {#5.3　statementtemplate一覧}

### 5.3.1　プラットフォームの起動 {#5.3.1　プラットフォームの起動}

#### 5.3.1.1　基本仕様 {#5.3.1.1　基本仕様}

* 電子書籍プラットフォームがシステムとして起動されたことを記録するためのテンプレート。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/viewer-launched |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | プラットフォームの起動 |

* 判定条件

| verb | https://w3id.org/xapi/adl/verbs/launched |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/viewer |

#### 5.3.1.2　記述規則（Rules） {#5.3.1.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 開始された電子書籍プラットフォームを識別するIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/launchReason”  
   1. reccommended  
   2. 電子書籍プラットフォームの起動のきっかけを記録する  
   3. launchReasonの値は、以下のような文字列を想定する  
      1. 例："user-launch"（ユーザ操作による起動）、"resume"（前回セッションからの再開）、"system-launch"（システムによる自動起動）  
      2. 値の語彙は本プロファイル内で一貫して用いることが望ましい  
      3. 本StatementTemplateは、プラットフォーム単位の開始を記録するものである  
      4. 電子書籍コンテンツ単位の利用開始はopened、ページや章・節への移動はprogressedを使用する

#### 5.3.1.3　Markdownテーブル {#5.3.1.3　markdownテーブル}

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |  
| :--- | :--- | :--- |  
| \*\*開始された電子書籍プラットフォームを識別するIRIまたはURLを設定する\*\* | \`$.object.id\` | included |  
| \*\*launchReasonの値は、以下のような文字列を想定する\*\*\<br\>例："user-launch"（ユーザ操作による起動）、"resume"（前回セッションからの再開）、"system-launch"（システムによる自動起動）\<br\>値の語彙は本プロファイル内で一貫して用いることが望ましい。\<br\>本StatementTemplateは、プラットフォーム単位の開始を記録するものである。\<br\>電子書籍コンテンツ単位の利用開始は \`opened\`、ページや章・節への移動は \`progressed\` を使用する。 | \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/launchReason'\]\` | recommended |

### **5.3.2　プラットフォームの終了** {#5.3.2　プラットフォームの終了}

#### 5.3.2.1　基本仕様 {#5.3.2.1　基本仕様}

* 電子書籍プラットフォームの利用が終了したことを記録するために用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/viewer-terminated |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | プラットフォームの終了 |

* 判定条件

| verb | https://w3id.org/xapi/adl/verbs/terminated |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/viewer |

#### 5.3.2.2　記述規則（Rules） {#5.3.2.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 終了した電子書籍プラットフォームを識別するIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/terminationReason"  
   1. reccommended  
   2. 電子書籍プラットフォームの終了理由を記録する  
   3. terminationReasonの値は、以下のような文字列を想定する  
      1. 例："user-quit"、"timeout"、"system-close"  
   4. 本事象は、プラットフォーム全体のセッション終了を表すものであり、電子書籍コンテンツ単位の利用終了や、読書行為の終了を示すものではない  
   5. 電子書籍コンテンツ単位の利用終了はclosed、読書活動の確定はread、ページ移動はprogressedを使用する

#### 5.3.2.3　Markdownテーブル {#5.3.2.3　markdownテーブル}

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |  
| :--- | :--- | :--- |  
| \*\*終了した電子書籍プラットフォームを識別するIRIまたはURLを設定する\*\* | \`$.object.id\` | included |  
| \*\*terminationReasonの値は、以下のような文字列を想定する\*\*\<br\>例："user-quit"、"timeout"、"system-close"\<br\>値の語彙は本プロファイル内で一貫して用いることが望ましい。\<br\>本事象は、プラットフォーム全体のセッション終了を表すものであり、電子書籍コンテンツ単位の利用終了や、読書行為の終了を示すものではない。\<br\>電子書籍コンテンツ単位の利用終了は \`closed\`、読書活動の確定は \`read\`、ページ移動は \`progressed\` を使用する。 | \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/terminationReason'\]\` | recommended |

　　

### **5.3.5　コンテンツの表示** {#5.3.5　コンテンツの表示}

#### 5.3.5.1　基本仕様 {#5.3.5.1　基本仕様}

* 電子書籍コンテンツが画面上に正常に描画され、学習者が閲覧可能な状態になったことを記録するために用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/content-opened |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | コンテンツの表示 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/open |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/content |

#### 5.3.5.2　記述規則（Rules） {#5.3.5.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 表示されたコンテンツidまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/startPosition"  
   1. recommended  
   2. 表示された際の初期ページ番号または位置情報を記録する  
   3. プラットフォームの起動やコンテンツの利用開始とは区別する

#### 5.3.3.3　Markdownテーブル {#5.3.3.3　markdownテーブル}

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |  
| :--- | :--- | :--- |  
| \*\*表示されたコンテンツのIDまたはURLを設定する。\*\* | \`$.object.id\` | included |  
| \*\*コンテンツが表示された際の初期ページ番号または位置情報を記録する。\*\*\<br\>※本項目はプラットフォームの起動（launched）やコンテンツ全体の利用開始（attempted等）とは区別し、具体的な表示位置を特定するために用いる。 | \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/startPosition'\]\` | recommended |

### **5.3.6　コンテンツの非表示** {#5.3.6　コンテンツの非表示}

#### 5.3.6.1　基本仕様 {#5.3.6.1　基本仕様}

* 電子書籍コンテンツの表示を終了（閉じる、アプリを終了する、または別の教材へ切り替える等）したことを記録するために用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/content-closed |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | コンテンツの非表示 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/close |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/content |

#### 5.3.6.2　記述規則（Rules） {#5.3.6.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 表示を終了したコンテンツのIDまたはURLを設定。  
2. $.result.duration  
   1. included  
   2. コンテンツの表示（opened）から本イベント（closed）までの総経過時間を ISO 8601 Duration形式で記録する。  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/endPosition"  
   1. recommended  
   2. コンテンツを閉じた時点の最終的なページ番号または位置情報を記録する。  
   3. プラットフォームの終了やコンテンツの利用終了と区別する

#### 5.3.6.3　Markdownテーブル {#5.3.6.3　markdownテーブル}

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |  
| :--- | :--- | :--- |  
| \*\*表示を終了したコンテンツのIDまたはURLを設定する。\*\* | \`$.object.id\` | included |  
| \*\*コンテンツの表示（opened）から本イベント（closed）までの総経過時間をISO 8601 Duration形式（例：PT5M10S）で記録する。\*\* | \`$.result.duration\` | included |  
| \*\*コンテンツを閉じた時点の最終的なページ番号または位置情報を記録する。\*\*\<br\>※プラットフォーム全体の終了（terminated）や学習全体の完了とは区別し、特定の閲覧セッション終了時における最終到達位置を記録するために用いる。 | \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/endPosition'\]\` | recommended |

## 

### **5.3.〇　読書行動** {#5.3.〇　読書行動}

#### 5.3.〇.1　基本仕様 {#5.3.〇.1　基本仕様}

* 学習者がコンテンツ内の特定の箇所に対し、意識的な読み取りを行った結果を記録するために用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/reading-paged |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 読書行動 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/read |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/reading |

#### 5.3.〇.2　記述規則（Rules） {#5.3.〇.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 読書対象のコンテンツのidまたはURLを設定  
2. $.result.duration  
   1. included  
   2. 対象範囲（ページ等）に留まった正味の滞在時間を記録する  
   3. 記録の形式はISO 8601 Duration形式を採用すること  
   4. ページ遷移（progressed）やコンテンツ非表示（closed）が発生した瞬間に、直前の滞在時間を確定させて送信する  
3. $.context.extensions."https://w3id.org/xapi/ebook/extensions/startPosition"  
   1. recommended  
   2. 読書開始時点のページ番号（見開きの場合は若い番号）または位置情報を記録する  
   3. プラットフォームの起動やコンテンツの利用開始とは区別し、具体的な読書地点を特定するために用いる  
4. $.result.extensions."[https://w3id.org/xapi/ebook/extensions/endPosition](https://w3id.org/xapi/ebook/extensions/endPosition)"  
   1. recommended  
   2. 表示されていた範囲の最後の位置情報を記録する  
   3. 単一ページ表示の場合は startPosition と同一の値を設定し、見開きやスクロール表示の場合は、同時に見えていた末尾の位置を設定する

#### 5.3.3.3　Markdownテーブル {#5.3.3.3　markdownテーブル-1}

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |  
| :--- | :--- | :--- |  
| \*\*読書対象のコンテンツのIDまたはURLを設定する。\*\* | \`$.object.id\` | included |  
| \*\*対象範囲（ページ等）に留まった正味の滞在時間をISO 8601 Duration形式で記録する。\*\*\<br\>ページ遷移（progressed）やコンテンツ非表示（closed）が発生した瞬間に、直前の滞在時間を確定させて送信すること。 | \`$.result.duration\` | included |  
| \*\*読書開始時点のページ番号（見開きの場合は若い番号）または位置情報を記録する。\*\*\<br\>プラットフォームの起動やコンテンツの利用開始とは区別し、具体的な読書地点を特定するために用いる。 | \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/startPosition'\]\` | recommended |  
| \*\*表示されていた範囲の最後の位置情報を記録する。\*\*\<br\>単一ページ表示の場合は \`startPosition\` と同一の値を設定し、見開きやスクロール表示の場合は、同時に見えていた末尾の位置を設定する。 | \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/endPosition'\]\` | recommended |

### **5.3.●　ページ移動**

#### 5.3.●.1　基本仕様 {#5.3.●.1　基本仕様}

* 学習者が電子書籍コンテンツ内でページ移動したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/progressed-page |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | ページ移動 |

* 判定条件

| verb | http://adlnet.gov/expapi/verbs/progressed |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/content |

#### 5.3.●.2　記述規則（Rules） {#5.3.●.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. ページ移動が行われた電子書籍コンテンツのidまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/startPosition"  
   1. recommended  
   2. ページ移動の起点となったページ番号または位置情報を設定  
   3. 目次からの移動の場合は、目次を開く直前のページ番号を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/endPosition"  
   1. included  
   2. ページ移動の到達点となったページ番号または位置情報を設定  
4. $.result.extensions."https://w3id.org/xapi/ebook/extensions/navigationMethod"  
   1. recommended  
   2. ページ移動の操作方法を設定  
      1. 例：ボタン操作（button）、目次（toc）

#### 5.3.●.3　Markdownテーブル {#5.3.●.3　markdownテーブル}

| 項目説明 (Description / ScopeNote) | Location (JSONPath) | Presence |  
| :--- | :--- | :--- |  
| \*\*ページ移動が行われた電子書籍コンテンツのIDまたはURLを設定する。\*\* | \`$.object.id\` | included |  
| \*\*ページ移動の起点となったページ番号または位置情報を設定する。\*\*\<br\>移動が発生した瞬間に学習者がいた元の場所を記録する。目次からの移動の場合は、目次を開く直前のページ番号を設定する。 | \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/startPosition'\]\` | recommended |  
| \*\*ページ移動の到達点となったページ番号または位置情報を設定する。\*\*\<br\>移動が完了した時点のページ番号を記録する。 | \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/endPosition'\]\` | included |  
| \*\*ページ移動の操作方法を設定する。\*\*\<br\>例：\`flick\`（フリック）、\`button\`（ボタン操作）、\`toc\`（目次）、\`link\`（本文内リンク）など。 | \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/navigationMethod'\]\` | recommended |

### **5.3.9　縦ローリング** {#5.3.9　縦ローリング}

#### 5.3.9.1　基本仕様 {#5.3.9.1　基本仕様}

* 学習者が学習端末を縦方向に保持、あるいはビューア設定を選択し、縦置き1ページ表示で閲覧する操作を記録するために用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/scrolled-vertically |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 縦ローリング |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/interact |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/viewer |

#### 5.3.9.2　記述規則（Rules） {#5.3.9.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 表示レイアウトの変更が行われた電子書籍プラットフォームを識別するIRIまた“はURIを設定  
2. contextExtensions."https://w3id.org/xapi/ebook/extensions/displayOrientation"  
   1. included  
   2. 表示レイアウト変更後の画面向きを示す値を設定  
   3. 縦ローリングの場合は、端末が縦置きであることを示す値を指定  
   4. 端末の縦置きにより1ページ表示へ切り替えが行われた場合を対象とする

#### 5.3.9.3　Markdownテーブル {#5.3.9.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 表示レイアウトの変更が行われた電子書籍プラットフォームを識別するIRIまたはURIを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/displayOrientation'\]\` | included | 表示レイアウト変更後の画面向きを示す値を設定する。縦ローリングの場合は、端末が縦置きであることを示す値を指定する。端末の縦置きにより1ページ表示へ切り替えが行われた場合を対象とする。 |

### **5.3.10　横ローリング** {#5.3.10　横ローリング}

#### 5.3.10.1　基本仕様 {#5.3.10.1　基本仕様}

* 学習者が電子書籍プラットフォームの表示レイアウトを横置き見開き表示へと変更、あるいは選択した際の操作を記録するために用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/scrolled-horizontally |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 横ローリング |

* 判定条件

| verb | https://w3id.org/xapi/ebook/verbs/layoutLandscapeSpread |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/viewer |

#### 5.3.10.2　記述規則（Rules） {#5.3.10.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 表示レイアウトの変更が行われた電子書籍プラットフォームを識別するIRIまた“はURIを設定  
2. contextExtensions."https://w3id.org/xapi/ebook/extensions/displayOrientation"  
   5. included  
   6. 表示レイアウト変更後の画面向きを示す値を設定  
   7. 横ローリングの場合は、端末が横置きであることを示す値を指定  
   8. 端末の横置きにより1ページ表示へ切り替えが行われた場合を対象とする

#### 5.3.10.3　Markdownテーブル {#5.3.10.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 表示レイアウトの変更が行われた電子書籍プラットフォームを識別するIRIまたはURIを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/displayOrientation'\]\` | included | 表示レイアウト変更後の画面向きを示す値を設定する。横ローリングの場合は、端末が横置きであることを示す値を指定する。端末の横置きにより見開き表示（または横方向の1ページ表示）へ切り替えが行われた場合を対象とする。 |

　　

### 

### **5.3.11　リフロー遷移** {#5.3.11　リフロー遷移}

#### 5.3.11.1　基本仕様 {#5.3.11.1　基本仕様}

* 学習者が電子書籍コンテンツにおいて、ボタン操作または本文クリックによってリフロー画面を表示し、画面サイズに合わせてテキストを折り返し表示できる機能を使用したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/reflow-interacted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | リフロー遷移 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/interact |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/viewer |

#### 5.3.11.2　記述規則（Rules） {#5.3.11.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. リフロー表示への切り替えが行われた電子書籍プラットフォーム、または対象となるコンテンツのページを識別するIRIまたはURIを設定  
2. $.result.extensions."https://w3id.org/xapi/ebook/extensions/fontSize"  
   1. recommended  
   2. リフロー表示への切り替えに伴い設定された、変更後の文字サイズを数字で指定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/lineSpacing"  
   1. recommended  
   2. リフロー表示への切り替えに伴い設定された、変更後の行間を数字で指定

#### 5.3.11.3　Markdownテーブル {#5.3.11.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | リフロー表示への切り替えが行われた電子書籍プラットフォーム、または対象となるコンテンツのページを識別するIRIまたはURIを設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/fontSize'\]\` | recommended | リフロー表示への切り替えに伴い設定された、変更後の文字サイズを数字で指定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/lineSpacing'\]\` | recommended | リフロー表示への切り替えに伴い設定された、変更後の行間を数字で指定する。 |

　　

### **5.3.12　しおり追加** {#5.3.12　しおり追加}

#### 5.3.12.1　基本仕様 {#5.3.12.1　基本仕様}

* 学習者が電子書籍内の特定箇所にしおりを追加したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/bookmark |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | しおり追加 |

* 判定条件

| verb | https://w3id.org/xapi/adb/verbs/bookmarked |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-type/bookmark |

#### 5.3.12.2　記述規則（Rules） {#5.3.12.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. ブックマーク対象となった電子書籍コンテンツのURLまたは識別子を設定  
2. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. ブックマークを追加したページ番号、または位置情報を設定  
3. $.context.extensions."https://w3id.org/xapi/ebook/extensions/bookmarkid"  
   1. recommended  
   2. ブックマークをアプリ内で一意に識別するID  
   3. 削除時に対応するため保存を推奨

#### 5.3.12.3　Markdownテーブル {#5.3.12.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | ブックマーク対象となった電子書籍コンテンツのURLまたは識別子を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | ブックマークを追加したページ番号、または位置情報を設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/bookmarkid'\]\` | recommended | ブックマークをアプリ内で一意に識別するIDを設定する。削除時に対応するため保存を推奨する。 |

　

### **5.3.13　しおり削除** {#5.3.13　しおり削除}

#### 5.3.13.1　基本仕様 {#5.3.13.1　基本仕様}

* 学習者が電子書籍内の既存のしおりを削除したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/bookmark-deleted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | しおり削除 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/delete |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/bookmark |

#### 5.3.13.2　記述規則（Rules） {#5.3.13.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 削除対象のブックマークが紐づく電子書籍コンテンツのURLまたは識別子を設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/bookmarkid"  
   1. included  
   2. 削除対象のブックマークを特定するID。しおり追加時に付与したIDと同じ値を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. recommended  
   2. しおりが紐づいていたページ番号または位置情報  
   3. bookmarkidのみで特定が可能な場合は省略可能

#### 5.3.13.3　Markdownテーブル {#5.3.13.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 削除対象のブックマークが紐づく電子書籍コンテンツのURLまたは識別子を設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/bookmarkid'\]\` | included | 削除対象のブックマークを特定するID。しおり追加時に付与したIDと同じ値を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | recommended | しおりが紐づいていたページ番号または位置情報。\`bookmarkid\` のみで特定が可能な場合は省略してよい。 |

## 

### **5.3.14　ペン書き込み** {#5.3.14　ペン書き込み}

#### 5.3.14.1　基本仕様 {#5.3.14.1　基本仕様}

* 学習者が電子書籍コンテンツ上でペン機能を用いて、任意の手書き線・文字を書き込む操作を記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/pen-noted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | ペン書き込み |

* 判定条件

| verb | https://w3id.org/xapi/verbs/noted |
| :---- | :---- |
| objectActivityType | https://w3id.org/xapi/ebook/activity-types/annotation |

#### 5.3.14.2　記述規則（Rules） {#5.3.14.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. ペン書き込みが行われた電子書籍コンテンツのIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/annotationTool"  
   1. included  
   2. 使用された注釈ツールの種別を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. 書き込みが行われたページ番号、または位置情報を設定  
4. $.result.extensions."https://w3id.org/xapi/ebook/extensions/targetLocation"  
   1. recommended  
   2. ページ内の具体的な書き込み座標や範囲情報などを設定

#### 5.3.14.3　Markdownテーブル {#5.3.14.3　markdownテーブル}

\#\# 5.3.14.2　記述規則（Rules）

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | ペン書き込みが行われた電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/annotationTool'\]\` | included | 使用された注釈ツールの種別を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 書き込みが行われたページ番号、または位置情報を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/targetLocation'\]\` | recommended | ページ内の具体的な書き込み座標や範囲情報などを設定する。 |

### **5.3.15　ペン書き込み削除** {#5.3.15　ペン書き込み削除}

#### 5.3.15.1　基本仕様 {#5.3.15.1　基本仕様}

* 学習者が電子書籍コンテンツ上のペン書き込みを削除したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/pen-deleted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | ペン書き込み削除 |

* 判定条件

| verb | https://w3id.org/xapi/verbs/noted |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/note |

#### 5.3.15.2　記述規則（Rules） {#5.3.15.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 削除対象の書き込みが紐づく電子書籍コンテンツのIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/annotationTool"  
   1. included  
   2. 削除対象となったツールの種別を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. recommended  
   2. 削除対象の書き込みが紐づいたページ番号、または位置情報を設定  
4. $.result.extensions."https://w3id.org/xapi/ebook/extensions/targetLocation"  
   1. recommended  
   2. 削除対象の書き込み座標や範囲情報などを設定

#### 5.3.14.3　Markdownテーブル {#5.3.14.3　markdownテーブル-1}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 削除対象の書き込みが紐づく電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/annotationTool'\]\` | included | 削除対象となったツールの種別を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | recommended | 削除対象の書き込みが紐づいたページ番号、または位置情報を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/targetLocation'\]\` | recommended | 削除対象の書き込み座標や範囲情報などを設定する。 |

### 

### **5.3.16　線分書き込み** {#5.3.16　線分書き込み}

#### 5.3.16.1　基本仕様 {#5.3.16.1　基本仕様}

* 学習者が電子書籍コンテンツ上で線分書き込み機能を用いて、線を書き込む操作を記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/line-noted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 線分書き込み |

* 判定条件

| verb | https://w3id.org/xapi/verbs/noted |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/note |

#### 5.3.16.2　記述規則（Rules） {#5.3.16.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 書き込みが行われた電子書籍コンテンツのIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/annotationTool”  
   1. included  
   2. 使用された注釈ツールの種別を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber”  
   1. included  
   2. 線分が描画されたページ番号、または位置情報を設定  
4. $.result.extensions."https://w3id.org/xapi/ebook/extensions/targetLocation”  
   1. recommended  
   2. 線分の描画箇所（始点・終点などの座標情報）を設定

#### 5.3.16.3　Markdownテーブル {#5.3.16.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 書き込みが行われた電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/annotationTool'\]\` | included | 使用された注釈ツールの種別を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 線分が描画されたページ番号、または位置情報を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/targetLocation'\]\` | recommended | 線分の描画箇所（始点・終点などの座標情報）を設定する。 |

### 

### **5.3.17　線分書き込み削除** {#5.3.17　線分書き込み削除}

#### 5.3.17.1　基本仕様 {#5.3.17.1　基本仕様}

* 学習者が電子書籍コンテンツ上の線分を削除したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/line-deleted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 線分書き込み削除 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/delete |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/note |

#### 5.3.17.2　記述規則（Rules） {#5.3.17.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 削除対象の書き込みが紐づく電子書籍コンテンツのIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/annotationTool”  
   1. included  
   2. 削除対象となったツールの種別を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber”  
   1. included  
   2. 削除対象の線分が描画されたページ番号、または位置情報を設定  
4. $.result.extensions."https://w3id.org/xapi/ebook/extensions/targetLocation”  
   1. recommended  
   2. 削除対象の線分が描画された箇所（始点・終点などの座標情報）を設定

#### 5.3.17.3　Markdownテーブル {#5.3.17.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 削除対象の書き込みが紐づく電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/annotationTool'\]\` | included | 削除対象となったツールの種別を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 削除対象の線分が描画されたページ番号、または位置情報を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/targetLocation'\]\` | recommended | 削除対象の線分が描画された箇所（始点・終点などの座標情報）を設定する。 |

### 

### **5.3.18　一括削除** {#5.3.18　一括削除}

#### 5.3.18.1　基本仕様 {#5.3.18.1　基本仕様}

* 学習者が電子書籍コンテンツ上に作成したすべての書き込みを一括削除したことを記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/all-deleted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 一括削除 |

* 判定条件

| verb | http://activitystrea.ms/schema/1.0/delete |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/note |

#### 5.3.18.2　記述規則（Rules） {#5.3.18.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 一括削除対象となったペン書き込み・線分書き込みが行われた電子書籍コンテンツのIRIまたはURLを設定  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. 削除対象の注釈が存在したページ番号を設定

#### 5.3.18.3　Markdownテーブル {#5.3.18.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 一括削除対象となったペン書き込み・線分書き込みが行われた電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 削除対象の注釈が存在したページ番号を設定する。 |

　　

### 

### **5.3.19　拡大** {#5.3.19　拡大}

#### 5.3.19.1　基本仕様 {#5.3.19.1　基本仕様}

* 学習者による電子書籍コンテンツの表示倍率の拡大を記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/zoom-interacted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 拡大 |

* 判定条件

| verb | http://adlnet.gov/expapi/verbs/interacted |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/setting |

#### 5.3.19.2　記述規則（Rules） {#5.3.19.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 操作が行われた電子書籍コンテンツのIRIまたはURLを設定する  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. 拡大操作が行われた際の表示ページ番号を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/zoomLevel"  
   1. included  
   2. 拡大後のズームレベルを設定  
   3. 数値が大きいほど拡大していることを示す

#### 5.3.19.3　Markdownテーブル {#5.3.19.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 操作が行われた電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 拡大操作が行われた際の表示ページ番号を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/zoomLevel'\]\` | included | 拡大後のズームレベルを設定する。数値が大きいほど拡大していることを示す。 |

### 

### **5.3.20　縮小** {#5.3.20　縮小}

#### 5.3.20.1　基本仕様 {#5.3.20.1　基本仕様}

* 学習者による電子書籍コンテンツの表示倍率の縮小を記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/zoom-out-interacted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 縮小 |

* 判定条件

| verb | http://adlnet.gov/expapi/verbs/interacted |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/setting |

#### 5.3.20.2　記述規則（Rules） {#5.3.20.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 操作が行われた電子書籍コンテンツのIRIまたはURLを設定する  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. 縮小操作が行われた際の表示ページ番号を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/zoomLevel"  
   1. included  
   2. 縮小後の倍率を指定  
   3. 数値が小さいほど縮小していることを示す

#### 5.3.20.3　Markdownテーブル {#5.3.20.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 操作が行われた電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 縮小操作が行われた際の表示ページ番号を設定する |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/zoomLevel'\]\` | included | 縮小後のズームレベルを設定する。数値が減少するほど縮小していることを示す。 |

　

### 

### 

### **5.3.21　背景色の変更** {#5.3.21　背景色の変更}

#### 5.3.21.1　基本仕様 {#5.3.21.1　基本仕様}

* 学習者による電子書籍コンテンツの背景色変更を記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/background-color-setting-interacted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 背景色の変更 |

* 判定条件

| verb | http://adlnet.gov/expapi/verbs/interacted |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/setting |

#### 5.3.21.2　記述規則（Rules） {#5.3.21.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 変更が行われた電子書籍コンテンツのIRIまたはURLを設定する  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. 変更が行われた際の表示ページ番号を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/pageColor"  
   1. included  
   2. 変更後の背景色を設定

#### 5.3.21.3　Markdownテーブル {#5.3.21.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 変更が行われた電子書籍コンテンツ의 IRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 変更が行われた際の表示ページ番号を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/pageColor'\]\` | included | 変更後の背景色を設定する。 |

　　

### 

### **5.3.22　文字色の変更** {#5.3.22　文字色の変更}

#### 5.3.22.1　基本仕様 {#5.3.22.1　基本仕様}

* 学習者による電子書籍コンテンツの背景色変更を記録する際に用いる。  
* 識別情報

| id | https://w3id.org/xapi/ebook/templates/font-color-setting-interacted |
| :---- | :---- |
| inScheme | https://w3id.org/xapi/ebook/v1 |
| prefLabel | 文字色の変更 |

* 判定条件

| verb | http://adlnet.gov/expapi/verbs/interacted |
| :---- | :---- |
| objectActivityType | http://activitystrea.ms/schema/1.0/setting |

#### 5.3.22.2　記述規則（Rules） {#5.3.22.2　記述規則（rules）}

1. $.object.id  
   1. included  
   2. 変更が行われた電子書籍コンテンツのIRIまたはURLを設定する  
2. $.context.extensions."https://w3id.org/xapi/ebook/extensions/pageNumber"  
   1. included  
   2. 変更が行われた際の表示ページ番号を設定  
3. $.result.extensions."https://w3id.org/xapi/ebook/extensions/fontColor"  
   1. included  
   2. 変更後の文字色を設定

#### 5.3.22.3　Markdownテーブル {#5.3.22.3　markdownテーブル}

| 場所 (JSONPath) | 必須性 | 項目説明 |  
| :--- | :--- | :--- |  
| \`$.object.id\` | included | 変更が行われた電子書籍コンテンツのIRIまたはURLを設定する。 |  
| \`$.context.extensions\['https://w3id.org/xapi/ebook/extensions/pageNumber'\]\` | included | 変更が行われた際の表示ページ番号を設定する。 |  
| \`$.result.extensions\['https://w3id.org/xapi/ebook/extensions/fontColor'\]\` | included | 変更後の文字色を設定する。 |

　　  
