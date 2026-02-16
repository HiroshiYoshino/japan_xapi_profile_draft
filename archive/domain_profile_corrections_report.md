# ドメインプロファイル修正完了報告

## 修正日時
2026年2月16日

## 修正対象ファイル

### 修正実施: Assessment Profile
- **ファイル**: `assessment/v1.0.0/assessment_profile.md`
- **修正箇所**: 1箇所

### 確認のみ（修正不要）
- **LMS Profile**: `lms/v1.0.0/lms_profile.md`
- **eBook Profile**: `ebook/v1.0.0/ebook_profile.md`
- **Group-LST Profile**: `group-lst/v1.0.0/group-lst_profile.md`

---

## 実施した修正

### 1. Assessment Profile: content-typeの説明文修正

**修正箇所**: 4.3.3.2　学習コンテンツやページの参照 - 記述規則（Rules）

**修正前**:
```
| **コンテンツの種類** | ... | recommended | hint(ヒント), result(結果), explanation(解説) 等 |
```

**修正後**:
```
| **コンテンツの種類** | ... | recommended | hint(ヒント)、result(結果)、explanation(解説)のいずれか。Core Profileで定義。 |
```

**修正理由**:
- Core Profileで`content-type`は`string`型（enum）として定義されており、単一値
- 「等」という表現が複数値を示唆する可能性があるため、「のいずれか」に変更して単一値であることを明確化
- Core Profileへの参照を明示

---

## 修正不要と判断した理由

### 1. unitの配列型への対応

**LMS Profile**:
- 説明文: 「学習課題が属する単元名。」
- Core Profileへの参照: 適切
- **判定**: 説明文はCore Profileへの参照のみで、型を明示していないため修正不要

**Assessment Profile**:
- 説明文: 「Core Profileで定義された単元名Extension。」「Core Profileで定義された単元名拡張。」
- **判定**: Core Profileへの参照のみで、型を明示していないため修正不要

**eBook Profile**:
- unitの使用なし
- **判定**: 修正不要

**Group-LST Profile**:
- unitの使用なし
- **判定**: 修正不要

### 2. assessment-typeの配列型から単一値への対応

**Assessment Profile**:
- 説明文: 「診断的(diagnostic)、形成的(formative)、総括的(summative)のいずれか。」「のいずれかを指定。」
- **判定**: 説明文が既に単一値を明確に示しているため修正不要

### 3. course-of-study-code、subject、gradeなどのその他のExtension

**全プロファイル**:
- 説明文: すべてCore Profileへの参照として記述
- 具体的な型やスキーマの記述なし
- **判定**: Core Profileで定義されているため、ドメインプロファイル側での修正不要

---

## Core Profileとの整合性確認

### Assessment Profile

| Extension | Core Profile定義 | Assessment Profile説明 | 整合性 |
|:---|:---|:---|:---:|
| unit | array型 | Core Profileで定義された単元名Extension | ✅ |
| subject | array型 | Core Profileで定義された教科Extension | ✅ |
| grade | array型 | Core Profileで定義された学年Extension | ✅ |
| course-of-study-code | array型 | Core Profileで定義された学習指導要領コードExtension | ✅ |
| difficulty | string型 | Core Profileで定義された難易度Extension | ✅ |
| content-type | string (enum) | hint、result、explanationのいずれか。Core Profileで定義 | ✅ |
| assessment-type | string (enum) | diagnostic、formative、summativeのいずれか | ✅ |
| purpose-of-question | array型 | 学習指導要領より細粒度の学習目標を記録 | ✅ |
| question-order | integer型 | デジタルドリルやCBTにおける問題の出題順序 | ✅ |

### LMS Profile

| Extension | Core Profile定義 | LMS Profile説明 | 整合性 |
|:---|:---|:---|:---:|
| unit | array型 | 学習課題が属する単元名 | ✅ |
| subject | array型 | Core Profileで定義された教科Extension | ✅ |
| grade | array型 | Core Profileで定義された学年Extension | ✅ |
| due-date | string (date-time) | 学習課題の実施期限日。ISO 8601形式 | ✅ |

### eBook Profile
- Core Profileで定義されたExtensionの使用なし
- ドメイン固有のExtensionのみ使用
- **整合性**: ✅ 問題なし

### Group-LST Profile
- scrapbook-item-typeのみCore Profileから使用
- **整合性**: ✅ 問題なし

---

## 今後の対応事項

### 1. サンプルStatement（別紙）の修正

各ドメインプロファイルにサンプルStatement（JSON形式）が別紙として存在する場合、以下の修正が必要：

**修正が必要な箇所**:
- `unit`: string型 → array型に変更
  - 例: `"unit": "第1章"` → `"unit": ["第1章"]`
- `subject`: string型 → array型に変更
  - 例: `"subject": "理科"` → `"subject": ["理科"]`
- `grade`: string型 → array型に変更
  - 例: `"grade": "5年"` → `"grade": ["5年"]`
- `course-of-study-code`: string型 → array型に変更（該当する場合）

**対象プロファイル**:
- LMS Profile
- Assessment Profile
- その他、サンプルStatementが存在するプロファイル

**注記**: 現時点ではv1.0.0ディレクトリ内にサンプルStatementファイルは見つかっていません。archiveディレクトリ内の古いファイルには存在しますが、これらは修正対象外です。

### 2. 実装ガイドラインの更新

実装者向けに以下の情報を提供することを推奨：

1. **データ型変更の通知**
   - `unit`, `subject`, `grade`, `course-of-study-code`は配列型
   - 単一値の場合は要素数1の配列として記録

2. **移行ガイド**
   - 既存実装からの移行方法
   - 後方互換性への影響

3. **ベストプラクティス**
   - Extension使用時の具体例
   - ActivityExtensionとContextExtensionの使い分け

---

## まとめ

### 実施した作業
1. ✅ Core Profileの更新（前回完了）
2. ✅ 各ドメインプロファイルの確認
3. ✅ Assessment Profileの修正（1箇所）
4. ✅ 整合性の検証

### 確認結果
- すべてのドメインプロファイルはCore Profileの定義と整合性が取れている
- 説明文レベルでの矛盾や齟齬は存在しない
- ドメインプロファイル本体の修正は最小限（1箇所のみ）

### 残存する課題
- サンプルStatement（別紙）の存在と修正の必要性について、現時点では未確認
- 別紙が存在する場合は、配列型への変更が必要

---

## 参考情報

### 関連ドキュメント
- [Core Profile](core/v1.0.0/core_profile.md) - 更新済み
- [Extension整理の改善提案](document/extension_reorganization_proposal.md)
- [Core Profile統合まとめ](document/core_profile_integration_summary.md)

### 修正完了日
2026年2月16日
