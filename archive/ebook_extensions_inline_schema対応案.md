# ebook Extensions inlineSchema 対応案

## 背景

現状の ebook プロファイルでは、Extensions 一覧の `inlineSchema` 欄が JSON Schema そのものではなく、型メモに近い略記になっている。

対象箇所：

- [ebook_profile.md](ebook/v1.0.0/ebook_profile.md#L152)

例えば、現状は以下のような表記になっている。

- `string`
- `enum [paging, index]`

人間向けの説明としては読めるが、将来 xAPI Profiles の Extension Concept に落とし込む場合には弱い。Profile 化を見据えるなら、`inlineSchema` は Draft-07 として解釈可能な JSON Schema に正規化しておくのが安全である。

## 問題点

- `inlineSchema` が JSON Schema ではなく略記であるため、機械的な検証に使えない。
- xAPI Profiles の Extension Concept に移植する際に、そのままでは再利用できない。
- `enum` 値の意味や、位置情報文字列の書式制約が文章側にしか現れず、スキーマと整合しにくい。

## 対応案

### 1. 最小対応案

一覧表はそのまま維持し、`inlineSchema` 欄の値だけを略記から Draft-07 互換の JSON Schema に置き換える。

例：

```json
{"type":"string"}
```

列挙型は以下のようにする。

```json
{"type":"string","enum":["paging","index"]}
```

ebook の各 extension は、最低限次のように正規化できる。

- `startPosition`: `{"type":"string"}`
- `endPosition`: `{"type":"string"}`
- `navigationMethod`: `{"type":"string","enum":["paging","index"]}`
- `contentPosition`: `{"type":"string"}`
- `bookmarkId`: `{"type":"string"}`
- `annotationTool`: `{"type":"string","enum":["freehand","straightline","textinput"]}`
- `targetLocation`: `{"type":"string"}`

### 2. 推奨対応案

Extensions 一覧は概要表にとどめ、各 extension ごとに小見出しを立てて、以下を個別に定義する。

- IRI
- Type
- Definition
- inlineSchema

構成例：

- 3.6.2.1 `startPosition`
- 3.6.2.2 `endPosition`
- 3.6.2.3 `navigationMethod`
- 以下同様

この形にすると、型だけでなく意味上の制約も書きやすい。例えば `navigationMethod` なら、Definition に以下を明示できる。

- `paging`: 前後ページ送りによる遷移
- `index`: 目次や一覧からの遷移

人間向け仕様としても読みやすくなり、将来の Profile 化でもそのまま移植しやすい。

### 3. よりよい正規化案

単に `type: string` にするだけでなく、最低限の制約も付与する。

例：

```json
{
  "type": "string",
  "minLength": 1
}
```

列挙型：

```json
{
  "type": "string",
  "enum": ["paging", "index"]
}
```

位置情報系の `targetLocation` や `contentPosition` については、将来的にフォーマットを明示できるなら `pattern` の導入も検討できる。

ただし、現時点で書式が固まっていないなら、無理に `pattern` を入れず、Definition に書式仕様を記述するだけに留めた方が安全である。

## 実務上のおすすめ

実際には、以下の順で進めるのがよい。

1. [ebook_profile.md](ebook/v1.0.0/ebook_profile.md#L152) の `inlineSchema` 欄を Draft-07 互換の JSON Schema 文字列へ置換する。
2. 各 extension の Definition を 1 文ずつ補強する。
3. 必要になった段階で、一覧表を個別節へ展開する。

## 注意点

- xAPI Profiles では `schema` と `inlineSchema` の併用は避ける前提なので、文書上でも「この一覧の `inlineSchema` は JSON Schema Draft-07 準拠」と明記した方がよい。
- `textinput` や `straightline` のような enum 値は、相互運用性のため一度決めたら安易に変更しない方がよい。
- `targetLocation` や `contentPosition` は、現状 `string` でもよいが、viewer 間の互換性を持たせたい場合は別途書式仕様の標準化が必要である。

## まとめ

最小修正で済ませるなら、`inlineSchema` 欄を Draft-07 互換の JSON Schema 文字列に置き換えるだけでも十分効果がある。

一方で、将来本当に xAPI Profiles の Extension Concept として整備する前提なら、一覧表だけで済ませず、各 extension を個別節で定義する構成に寄せるのが望ましい。