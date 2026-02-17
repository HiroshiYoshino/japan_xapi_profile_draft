# Extension整理の改善提案

## 1. 現状の課題

### 1.1 同一IRIでActivityExtensionとContextExtensionの両方で使用されている問題

現在、以下のExtensionが同じIRIでActivityExtensionとContextExtensionの両方として定義されています：

| Extension名 | 現在のIRI | 用途 |
|:---|:---|:---|
| subject (教科) | `https://w3id.org/japan-xapi/extensions/subject` | ActivityExtension / ContextExtension |
| grade (学年) | `https://w3id.org/japan-xapi/extensions/grade` | ActivityExtension / ContextExtension |
| course-of-study-code (学習指導要領コード) | `https://w3id.org/japan-xapi/extensions/course-of-study-code` | ActivityExtension / ContextExtension |
| unit (単元名) | `https://w3id.org/japan-xapi/extensions/unit` | ActivityExtension / ContextExtension |

**問題点:**
- 同じIRIが異なる場所（`$.object.definition.extensions`と`$.context.extensions`）で使用されるため、データの解釈や検証時に混乱が生じる
- xAPI Profile仕様上、ExtensionのTypeは明確に区別されるべき
- 実装時にどちらの用途かが不明確

### 1.2 Core Profileにおけるunitの二重定義

Core Profile内でunitが2回定義されています：

1. **1つ目の定義:**
   - Type: `ActivityExtension` / `ContextExtension`
   - Schema: `{ "type": "string" }`

2. **2つ目の定義:**
   - Type: `ActivityExtension` / `ContextExtension`
   - Schema: `{ "type": "array", "items": { "type": "string" } }`

**問題点:**
- 同一Extension名で異なるスキーマが存在
- 実装者が混乱する

---

## 2. 改善案

### 2.1 Extension用途の明確な分離（推奨案）

#### 方針A: IRIの場所による使い分け（Scope Noteで明確化）

同じExtensionでもActivityとContextで意味が異なる場合、IRIは同じでも、Scope Noteで使い分けを明記する。

**推奨されるパターン:**

```markdown
#### subject (教科)

- **IRI**: `https://w3id.org/japan-xapi/extensions/subject`
- **Type**: `ActivityExtension`, `ContextExtension`
- **Definition**: 学習対象の教科名。
- **Scope Note**: 
  - ActivityExtensionとして使用する場合: オブジェクト（コンテンツや課題）が対象とする教科を示す
  - ContextExtensionとして使用する場合: 学習活動が行われた教科のコンテキストを示す
  - 文部科学省教育データ標準の教科名コード表に準拠することを推奨する
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```
```

#### 方針B: IRIを完全に分離（最も明確だが冗長）

ActivityExtensionとContextExtensionで完全に異なるIRIを使用する。

**例:**
- ActivityExtension: `https://w3id.org/japan-xapi/extensions/activity/subject`
- ContextExtension: `https://w3id.org/japan-xapi/extensions/context/subject`

**メリット:**
- 最も明確で混乱がない
- プログラマティックに処理しやすい

**デメリット:**
- IRIが冗長になる
- 同じ概念を2つのIRIで管理する必要がある
- 既存の実装との互換性問題

#### 推奨: **方針A（Scope Noteで明確化）**

理由：
- xAPI Profileの一般的な実践では、同じ概念は同じIRIを使用
- Scope Noteで用途を明確にすることで実装者が理解可能
- IRIの増殖を防げる

### 2.2 unitの二重定義の解消

**推奨:**
- **単一定義に統一:** `array`型のみを採用
- 理由: 複数の単元にまたがる学習内容に対応可能（拡張性が高い）

```markdown
#### unit (単元名)

- **IRI**: `https://w3id.org/japan-xapi/extensions/unit`
- **Type**: `ActivityExtension`, `ContextExtension`
- **Definition**: 学習課題やコンテンツが属する単元名。
- **Scope Note**:
  - ActivityExtensionとして使用する場合: オブジェクト（コンテンツや課題）が対象とする単元を示す
  - ContextExtensionとして使用する場合: 学習活動が行われた単元のコンテキストを示す
  - 単一の単元の場合は要素数1の配列とする
  - 複数の単元にまたがる場合は複数の要素を含む配列とする
- **Schema**:
  ```json
  {
    "type": "array",
    "items": { "type": "string" }
  }
  ```
```

### 2.3 新規Extensionの追加整理

Core Profileに以下のExtensionを追加すべき：

| Extension名 | IRI | Type | 使用ドメイン |
|:---|:---|:---|:---|
| course-of-study-code | `https://w3id.org/japan-xapi/extensions/course-of-study-code` | ActivityExtension, ContextExtension | LMS, Assessment |
| purpose-of-question | `https://w3id.org/japan-xapi/extensions/purpose-of-question` | ActivityExtension | Assessment |
| question-order | `https://w3id.org/japan-xapi/extensions/question-order` | ActivityExtension | Assessment |
| content-type | `https://w3id.org/japan-xapi/extensions/content-type` | ActivityExtension | Assessment |
| assessment-type | `https://w3id.org/japan-xapi/extensions/assessment-type` | ContextExtension | Assessment |

---

## 3. ドメインプロファイル間の齟齬

### 3.1 発見された齟齬

現時点で、各ドメインプロファイル間に定義の齟齬は発見されませんでした。すべてのドメインプロファイルは：
- Core Profileで定義されたExtensionを参照している
- 同じIRIと同じ意味で使用している

---

## 4. ActivityTypeについて

### 4.1 現状

現在、Core ProfileにはActivityTypeが定義されていません。各ドメインプロファイルは独自のActivityTypeを定義しています：

- **eBook**: viewer, content, page, bookmark, annotation, settings
  - Namespace: `https://w3id.org/xapi/ebook/activity-types/`
- **Group-LST**: tool
  - Namespace: `https://w3id.org/japan-xapi/activity-types/group-lst/`

### 4.2 推奨

**ActivityTypeはドメイン固有のまま維持する**

理由：
- ActivityTypeは各ドメインの特性を強く反映する
- ドメイン間で共通利用されるActivityTypeが現時点で存在しない
- Core Profileの肥大化を防ぐ

---

## 5. 実装ガイドライン

### 5.1 Extension使用時の基本ルール

1. **ActivityExtensionの使用:**
   - オブジェクト自体の属性を示す場合に使用
   - `$.object.definition.extensions`に配置

2. **ContextExtensionの使用:**
   - 学習活動が行われた状況や環境を示す場合に使用
   - `$.context.extensions`に配置

3. **両方で同じIRIを使用する場合:**
   - Scope Noteで定義された用途に従う
   - 同一Statement内で両方に同じExtensionを含めることも可能（意味が異なる場合）

### 5.2 データ型の統一

- **単一値でも配列型を使用する場合:** 将来の拡張性を考慮し、要素数1の配列として記録
- **例:** `"subject": ["算数"]`（文字列 `"算数"` ではなく）

---

## 6. 移行計画

### 6.1 短期（v1.0.0リリース前）

1. Core Profileのunit二重定義を解消（array型に統一）
2. 不足しているExtensionをCore Profileに追加
3. すべてのExtensionにScope Noteを追加（ActivityとContextの使い分けを明記）
4. 各ドメインプロファイルのドキュメントを確認・更新

### 6.2 中長期（v1.x以降）

1. 実装事例に基づくベストプラクティスの文書化
2. Extension利用状況のモニタリング
3. 必要に応じた新規Extensionの追加または既存Extensionの改訂

---

## 7. まとめ

### 7.1 推奨事項

1. **同一IRIでActivityとContext両方に使用されるExtensionは、Scope Noteで用途を明確化する**
2. **unitはarray型に統一する**
3. **不足しているExtensionをCore Profileに追加する**
4. **ActivityTypeはドメイン固有として維持する**
5. **各Extensionに詳細なScope Noteを追加する**

### 7.2 期待される効果

- 実装者の混乱を防ぐ
- データの一貫性が向上
- ドメインプロファイル間の相互運用性が向上
- 将来の拡張が容易になる
