# Core Profile統合まとめ

## 実施内容

各ドメインプロファイル（LMS, eBook, Assessment, Group-LST）から以下の要素を抽出し、Core Profileに構造的に統合しました。

---

## 1. ActivityExtension

Core Profileに定義されたActivityExtensionの一覧：

| Extension名 | IRI | 使用ドメイン | 説明 |
|:---|:---|:---|:---|
| **subject** (教科) | `https://w3id.org/japan-xapi/extensions/subject` | 全ドメイン共通 | 学習対象の教科名（配列型） |
| **grade** (学年) | `https://w3id.org/japan-xapi/extensions/grade` | 全ドメイン共通 | 対象学年（配列型） |
| **course-of-study-code** (学習指導要領コード) | `https://w3id.org/japan-xapi/extensions/course-of-study-code` | LMS, Assessment | 学習指導要領に基づく学習項目コード（配列型） |
| **unit** (単元名) | `https://w3id.org/japan-xapi/extensions/unit` | 全ドメイン共通 | 学習課題やコンテンツが属する単元名（配列型） |
| **scrapbook-item-type** (アイテムタイプ) | `https://w3id.org/japan-xapi/extensions/scrapbook-item-type` | Group-LST | スクラップブック等で作成されるオブジェクトの種類 |
| **purpose-of-question** (問題の趣旨) | `https://w3id.org/japan-xapi/extensions/purpose-of-question` | Assessment | 問題の趣旨（配列型） |
| **question-order** (問題の出題順序) | `https://w3id.org/japan-xapi/extensions/question-order` | Assessment | 問題の出題順序（整数型） |
| **content-type** (コンテンツの種類) | `https://w3id.org/japan-xapi/extensions/content-type` | Assessment | ヒント、結果、解説などの種別 |

**注記:**
- **subject, grade, course-of-study-code, unit** は ActivityExtension と ContextExtension の両方で使用可能
- 各ExtensionのScope Noteで用途を明確化

---

## 2. ContextExtension

Core Profileに定義されたContextExtensionの一覧：

| Extension名 | IRI | 使用ドメイン | 説明 |
|:---|:---|:---|:---|
| **difficulty** (難易度) | `https://w3id.org/japan-xapi/extensions/difficulty` | Assessment等 | 学習コンテンツの難易度 |
| **subject** (教科) | `https://w3id.org/japan-xapi/extensions/subject` | 全ドメイン共通 | 学習活動が行われた教科のコンテキスト（配列型） |
| **grade** (学年) | `https://w3id.org/japan-xapi/extensions/grade` | 全ドメイン共通 | 学習活動が行われた学年のコンテキスト（配列型） |
| **course-of-study-code** (学習指導要領コード) | `https://w3id.org/japan-xapi/extensions/course-of-study-code` | LMS, Assessment | 学習活動における学習指導要領項目（配列型） |
| **unit** (単元名) | `https://w3id.org/japan-xapi/extensions/unit` | 全ドメイン共通 | 学習活動が行われた単元のコンテキスト（配列型） |
| **due-date** (期限日) | `https://w3id.org/japan-xapi/extensions/due-date` | LMS | 課題等の実施期限日（ISO 8601形式） |
| **assessment-type** (評価のタイプ) | `https://w3id.org/japan-xapi/extensions/assessment-type` | Assessment | 診断的、形成的、総括的 |

**注記:**
- **subject, grade, course-of-study-code, unit** は ActivityExtension と ContextExtension の両方で使用可能

---

## 3. objectActivityType（ドメイン固有）

ActivityTypeは各ドメインプロファイルで独自に定義されており、Core Profileには含めていません。

### eBook Profile のActivityType

| ActivityType | IRI | 説明 |
|:---|:---|:---|
| viewer | `https://w3id.org/xapi/ebook/activity-types/viewer` | 電子書籍ビューア |
| content | `https://w3id.org/xapi/ebook/activity-types/content` | 電子書籍コンテンツ |
| page | `https://w3id.org/xapi/ebook/activity-types/page` | ページ |
| bookmark | `https://w3id.org/xapi/ebook/activity-types/bookmark` | しおり |
| annotation | `https://w3id.org/xapi/ebook/activity-types/annotation` | 注釈 |
| settings | `https://w3id.org/xapi/ebook/activity-types/settings` | 設定 |

### Group-LST Profile のActivityType

| ActivityType | IRI | 説明 |
|:---|:---|:---|
| tool | `https://w3id.org/japan-xapi/activity-types/group-lst/tool` | グループ学習支援ツール |

**推奨事項:** ActivityTypeはドメイン固有の特性を反映するため、各ドメインプロファイルで管理することを推奨します。

---

## 4. ドメインプロファイル間の齟齬

### 4.1 発見された問題点

#### 問題1: 同一IRIでActivityExtensionとContextExtensionの両方で使用

以下のExtensionが同じIRIで両方のタイプとして使用されていました：

- **subject** (教科)
- **grade** (学年)
- **course-of-study-code** (学習指導要領コード)
- **unit** (単元名)

**対応:** 各ExtensionのScope Noteに用途を明記し、ActivityとContextでの使い分けを明確化しました。

#### 問題2: unitの二重定義

Core Profile内で `unit` が2回定義されていました：
- 1つ目: `string`型
- 2つ目: `array`型

**対応:** `array`型に統一し、単一単元の場合は要素数1の配列として記録することとしました。

#### 問題3: content-typeのスキーマ不一致

Assessmentプロファイルでは `content-type` が配列（array）として定義されていましたが、意味的には単一値が適切。

**対応:** Core Profileでは `string`型（enum）として定義し、統一しました。

#### 問題4: assessment-typeのスキーマ不一致

Assessmentプロファイルでは `assessment-type` が配列（array）として定義されていましたが、意味的には単一値が適切。

**対応:** Core Profileでは `string`型（enum）として定義し、統一しました。

### 4.2 齟齬なし（問題なし）

各ドメインプロファイル間で、以下の点については齟齬がありませんでした：

- すべてのドメインプロファイルが同じIRIを使用
- Extensionの意味的な解釈が一貫している
- Core Profileへの参照方法が統一されている

---

## 5. Extension整理の改善提案

### 5.1 推奨事項

1. **同一IRIでActivityとContext両方に使用されるExtensionは、Scope Noteで用途を明確化**
   - 実装: 完了
   - すべての該当ExtensionにScope Noteを追加

2. **データ型の統一**
   - `unit`: array型に統一（完了）
   - `content-type`: string型（enum）に統一（完了）
   - `assessment-type`: string型（enum）に統一（完了）

3. **ActivityTypeはドメイン固有として維持**
   - Core Profileには含めない
   - 各ドメインプロファイルで管理

### 5.2 Extension使用時の基本ルール

#### ActivityExtensionの使用:
- オブジェクト自体の属性を示す場合に使用
- `$.object.definition.extensions`に配置
- 例: 課題が対象とする教科・学年

#### ContextExtensionの使用:
- 学習活動が行われた状況や環境を示す場合に使用
- `$.context.extensions`に配置
- 例: 学習活動が行われた教科・学年のコンテキスト

#### 両方で使用する場合:
- Scope Noteで定義された用途に従う
- 同一Statement内で両方に同じExtensionを含めることも可能（意味が異なる場合）

---

## 6. Core Profile更新内容

### 6.1 追加されたExtension

以下のExtensionを新たにCore Profileに追加しました：

1. **course-of-study-code** (学習指導要領コード)
   - Type: ActivityExtension, ContextExtension
   - 使用ドメイン: LMS, Assessment

2. **purpose-of-question** (問題の趣旨)
   - Type: ActivityExtension
   - 使用ドメイン: Assessment

3. **question-order** (問題の出題順序)
   - Type: ActivityExtension
   - 使用ドメイン: Assessment

4. **content-type** (コンテンツの種類)
   - Type: ActivityExtension
   - 使用ドメイン: Assessment

5. **assessment-type** (評価のタイプ)
   - Type: ContextExtension
   - 使用ドメイン: Assessment

### 6.2 修正されたExtension

1. **unit** (単元名)
   - 二重定義を解消し、array型に統一
   - Scope Noteを追加

2. **subject** (教科)
   - Scope Noteを追加し、ActivityとContextの使い分けを明確化

3. **grade** (学年)
   - Scope Noteを追加し、ActivityとContextの使い分けを明確化

4. **difficulty** (難易度)
   - Scope Noteを追加

5. **due-date** (期限日)
   - Scope Noteを追加

6. **scrapbook-item-type** (アイテムタイプ)
   - Scope Noteを追加

---

## 7. 実装への影響

### 7.1 互換性への影響

- **後方互換性の破壊:** `unit`のデータ型変更（string → array）
  - 既存実装への影響: 既存の実装で`unit`を文字列として使用している場合、配列に変更する必要がある
  - 移行方法: `"unit": "第1章"` → `"unit": ["第1章"]`

- **後方互換性の維持:** その他のExtension
  - 既存のExtensionは意味を変えずにScope Noteを追加したのみ
  - 既存の実装はそのまま動作

### 7.2 ドメインプロファイルへの影響

各ドメインプロファイルは以下の修正が必要です：

1. **LMS Profile:**
   - `unit`の使用を配列型に更新

2. **eBook Profile:**
   - Core Profileへの参照を確認（ドメイン固有のextensionは影響なし）

3. **Assessment Profile:**
   - `unit`の使用を配列型に更新
   - `content-type`のスキーマをstringに更新
   - `assessment-type`のスキーマをstringに更新

4. **Group-LST Profile:**
   - `unit`の使用を配列型に更新（使用している場合）

---

## 8. まとめ

### 8.1 成果

1. **Core Profileの完成度向上**
   - 全ドメインで共通利用されるExtensionを整理
   - 各Extensionに詳細なScope Noteを追加

2. **データ一貫性の向上**
   - 同一概念に対して同一IRIを使用
   - データ型の統一

3. **実装者への明確なガイダンス**
   - ActivityとContextの使い分けを明記
   - 実装時の混乱を最小化

### 8.2 今後の課題

1. **各ドメインプロファイルの更新**
   - Core Profileの変更に合わせた修正
   - サンプルStatementの更新

2. **実装ガイドラインの整備**
   - Extension使用のベストプラクティス文書化
   - 移行ガイドの作成

3. **継続的なメンテナンス**
   - 実装事例に基づくフィードバック収集
   - 必要に応じた改訂

---

## 9. 参考資料

- [Core Profile](core/v1.0.0/core_profile.md) - 更新済み
- [Extension整理の改善提案](document/extension_reorganization_proposal.md) - 詳細な改善案
- [Core Profile Guidelines](document/document_rules/Core_Profile_Guidelines.md) - 記述ガイドライン
