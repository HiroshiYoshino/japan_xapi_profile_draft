

 

Group learning support toolに関する

xAPIプロファイル標準仕様（案）

2025年12月16日版

1. # 本ドキュメントについて

   　本ドキュメントは、日本の教育DX事業者が共有して利用するスタディ・ログ（xAPI形式）の仕様策定に向け、ICT CONNECT 21 技術ワーキンググループの配下に設置されたxAPIサブワーキンググループの1つであるグループ学習支援ツール（Group-lst）分野における学習ログを対象として取りまとめたGroup Learning Support Tool xAPIプロファイル標準仕様（案）である。  
   　本仕様は、京都大学緒方研究室が策定しているプロファイル案および内閣府戦略的イノベーション創造プログラムでの「相互運用性を確保したペダゴジカル情報プラットフォームの研究開発・実用化検討」のための xAPI プロファイル利用に関する仕様を踏まえて、グループ学習におけるコンテンツの操作、学習活動等の学習ログを体系的に記録可能な仕様として位置づいている。  
     
   　なお、本プロファイルは、LMS xAPIプロファイルに位置づけられている「学習課題」に対して、その具体物を個人あるいは集団で協働的に操作する学習活動を範囲とする。  
   　ここでのグループ学習とは、個人ないし集団が行う学習活動を指す。グループ学習でありつつ、個人の学習活動も範囲とする理由として、個人の考えを作成した後にグループで交流し、また、グループで交流したことを踏まえて個人の考えを編集するといった往還が見られるためであり、厳密に弁別できないためである。  
     
   学習活動の例（ユースケース）  
* 自分や自分たちの考えをテキストやオブジェクト等で表現すること  
* 友達の考えに対して「いいね」を送ること  
* 友達の考えに対してコメントしたりフィードバックしたりすること


# 2.　本ドキュメントの構成について

　本ドキュメントでは、共通ユースケースと特有ユースケースの2つに区分して整理している。  
　共通ユースケースは、下記の6種から成り立っている。

1. ツールの起動  
2. ツールの終了  
3. ツール内での活動開始  
4. ツール内での活動終了  
     
   　特有ユースケースは、特定の条件や操作にのみ発生するもので、下記の9種類から成り立っている。  
1. オブジェクト操作  
   1. オブジェクト（テキスト）の作成  
   2. オブジェクト（図形）の作成  
   3. オブジェクトの削除  
   4. オブジェクトの移動  
   5. オブジェクトのコピー  
   6. オブジェクトのペースト  
2. コメント  
   1. スレッドの立ち上げ  
   2. スレッドの書き込み  
3. スタンプ  
   1. スタンプの送信

# 3.　共通ユースケース

　3.1　ツールの起動

| definition | 本項目は、グループ学習支援ツールが起動したことを記録する |
| ----- | :---- |
| verb | https://w3id.org/xapi/adl/verbs/launched |
| objectActivityType | https://w3id.org/xapi/group-lst/activity-type/group\_learning\_support\_tool |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | 起動したツールのIRIまたはURLを設定 |

　3.2　ツールの終了

| definition | 本項目は、グループ学習支援ツールの利用が終了したことを記録する |
| ----- | :---- |
| verb | https://w3id.org/xapi/adl/verbs/terminated |
| objectActivityType | https://w3id.org/xapi/group-lst/activity-type/group\_learning\_support\_tool |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | 終了したツールのIRIまたはURLを設定 |

　3.3　ツール内での活動開始

| definition | 本項目は、ツール内のコンテンツの利用を開始したことを記録する際に用いる。対象コンテンツが初めて開かれ、編集可能な状態になったことを契機として記録する |
| ----- | :---- |
| verb | https://w3id.org/xapi/adl/verbs/launched |
| objectActivityType | http://id.tincanapi.com/activitytype/slide |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | 利用を開始したコンテンツIRIまたはURLを設定 |

　3.4　ツール内での活動終了

| definition | 本項目は、学習者がコンテンツの利用を終了したことを記録する際に用いる。対象コンテンツが閉じられ、閲覧ができない状態になったことを契機として記録する |
| ----- | :---- |
| verb | https://w3id.org/xapi/adl/verbs/exited |
| objectActivityType | http://id.tincanapi.com/activitytype/slide |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | 利用を終了したコンテンツIRIまたはURLを設定 |

# 4.　特有ユースケース1　オブジェクト

　4.1　オブジェクト（テキスト）の作成

| definition | 本項目は、学習者がコンテンツ内でオブジェクトを作成したことを記録する |
| ----- | :---- |
| verb | https://w3id.org/xapi/scrapbook/verbs/created |
| objectActivityType | http://id.tincanapi.com/activitytype/slide |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | コンテンツのIDまたはURLを設定 |
| location | $.object.definition.extensions."http://example.com/xapi/object/extensions/scrapbook".itemType \= "text" |
| 　presence | included |
| 　scopeNote | オブジェクトの種類をextensionsで指定する |
| location | $.result.response |
| 　presence | included |
| 　scopeNote | 入力した文字列 |

　4.2　オブジェクト（図形）の作成

| definition | 本項目は、学習者がコンテンツ内でオブジェクトを作成したことを記録する |
| ----- | :---- |
| verb | https://w3id.org/xapi/scrapbook/verbs/created |
| objectActivityType | http://id.tincanapi.com/activitytype/slide |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | コンテンツのIDまたはURLを設定 |
| location | $.object.definition.extensions."http://example.com/xapi/object/extensions/scrapbook".itemType \= "shape" |
| 　presence | included |
| 　scopeNote | オブジェクトの種類をextensionsで指定する |

# 5.　特有ユースケース2　コメント

　5.1　スレッドの立ち上げ

| definition | 本項目は、学習者がコンテンツ上で議論するためのスレッドを作成したことを記録する。ただし、特定のスライド、オブジェクトに対してコメントする場合は必要としない。その場合、5.2のrepliedでobject.idに対象物を指定する。 |
| ----- | :---- |
| verb | http://activitystrea.ms/create |
| objectActivityType | http://id.tincanapi.com/activitytype/discussion |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | 作られたスレッドのIRIまたはURLを設定 |

　5.2　スレッドの書き込み

| definition | 本項目は、学習者がコンテンツ上で議論するためのスレッドに書き込んだことを記録する |
| ----- | :---- |
| verb | http://id.tincanapi.com/verb/replied |
| objectActivityType | http://id.tincanapi.com/activitytype/discussion |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | 書き込んだスレッドのIRIまたはURLを設定 |
| location | $.result.response |
| 　presence | included |
| 　scopeNote | 入力した文字列 |

# 6.　特有ユースケース3　スタンプ

　6.1　スタンプの送信

| definition | 本項目は、学習者がコンテンツに対して「いいね」スタンプを送信したことを記録する |
| ----- | :---- |
| verb | http://id.tincanapi.com/verb/voted-up |
| objectActivityType | http://id.tincanapi.com/activitytype/slide |
| **rules** |  |
| location | $.object.id |
| 　presence | included |
| 　scopeNote | いいねしたコンテンツのIRIまたはURLを設定 |

