---
marp: true
paginate: true
backgroundColor: #fff
---

<style>
/* Google Fontsから日本語フォントを読み込み */
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700&display=swap');

/* --- 色やフォントの基本設定 --- */
:root {
  --color-background: #f8f8f4;
  --color-foreground: #3a3b5a;
  --color-heading: #4f86c6;
  --color-hr: #000000;
  --font-default: 'Noto Sans JP', 'Hiragino Kaku Gothic ProN', 'Meiryo', sans-serif;
}

/* --- スライド全体のスタイル --- */
section {
  background-color: var(--color-background);
  color: var(--color-foreground);
  font-family: var(--font-default);
  font-weight: 400;
  box-sizing: border-box;
  border-bottom: 8px solid var(--color-hr);
  position: relative;
  line-height: 1.7;
  font-size: 22px;
  padding: 56px;
}
section:last-of-type {
  border-bottom: none;
}

/* --- 見出しのスタイル --- */
h1, h2, h3, h4, h5, h6 {
  font-weight: 700;
  color: var(--color-heading);
  margin: 0;
  padding: 0;
}

/* タイトルページ(h1)のスタイル */
h1 {
  font-size: 56px;
  line-height: 1.4;
  text-align: left;
}

/* 通常スライドのタイトル(##) */
h2 {
  position: absolute;
  top: 40px;
  left: 56px;
  right: 56px;
  font-size: 40px;
  padding-top: 0;
  padding-bottom: 16px;
}

/* h2の疑似要素(::after)を使って、短い線を実装 */
h2::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 8px;
  width: 60px;
  height: 2px;
  background-color: var(--color-hr);
}

/* h2と後続コンテンツの間のスペースを確保 */
h2 + * {
  margin-top: 80px;
}

/* サブ見出し (例: 目的, 目標) */
h3 {
  color: var(--color-foreground);
  font-size: 28px;
  margin-top: 32px;
  margin-bottom: 12px;
}

/* --- リストのスタイル --- */
ul, ol {
  padding-left: 32px;
}
li {
  margin-bottom: 10px;
}

/* フッターとして機能する、太い青いラインを実装 */
footer {
  font-size: 0;
  color: transparent;
  position: absolute;
  left: 56px;
  right: 56px;
  bottom: 40px;
  height: 8px;
  background-color: var(--color-heading);
}

/* ★★★ ロゴの配置方法を、calc()を使った最も堅牢な方法に変更 ★★★ */
header {
  font-size: 0;
  color: transparent;
  background-image: url('ロゴ.png');
  background-repeat: no-repeat;
  background-size: contain;
  background-position: top right;
  
  position: absolute;
  top: 40px;
  
  /* rightプロパティの代わりに、calc()で左からの位置を計算して配置を安定させます */
  /* 計算式: (コンテナの幅 - ロゴの幅 - 右の余白) */
  left: calc(100% - 180px - 56px);
  
  /*
    【重要】下のwidthの値を変更した場合、
    上のcalc()内の「180px」も同じ値にしてください。
  */
  width: 180px;
  height: 50px;
}

/* --- 特別なクラス --- */
section.lead {
  border-bottom: 8px solid var(--color-hr);
}

/* タイトルページではフッターラインとロゴ(header)を非表示にする */
section.lead footer,
section.lead header {
  display: none;
}

section.lead h1 {
  margin-bottom: 24px;
}
section.lead p {
  font-size: 24px;
  color: var(--color-foreground);
}

/* グリッドレイアウト */
.grid-2x2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  margin: 32px 0;
}

.columns {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 2rem;
}

.columns > div {
  min-width: 0;
}

/* フィーチャーカード */
.feature-card {
  background-color: #ffffff;
  border: 2px solid #e0e0e0;
  border-radius: 12px;
  padding: 24px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.feature-card h3 {
  color: var(--color-heading);
  font-size: 24px;
  margin-bottom: 12px;
}

.feature-card p {
  color: var(--color-foreground);
  font-size: 18px;
  line-height: 1.6;
  margin: 0;
}

/* 強調スタイル */
strong {
  color: var(--color-heading);
  font-weight: 700;
}

/* 引用スタイル */
blockquote {
  background-color: #f0f4f8;
  border-left: 4px solid var(--color-heading);
  padding: 16px 24px;
  margin: 24px 0;
  border-radius: 0 8px 8px 0;
}

/* コードスタイル */
code {
  background-color: #f5f5f5;
  padding: 2px 6px;
  border-radius: 4px;
  font-family: 'Consolas', 'Monaco', monospace;
  font-size: 18px;
}

pre {
  background-color: #f5f5f5;
  padding: 16px;
  border-radius: 8px;
  overflow-x: auto;
  margin: 24px 0;
}

/* テーブルスタイル */
table {
  width: 100%;
  border-collapse: collapse;
  margin: 24px 0;
}

th, td {
  border: 1px solid #ddd;
  padding: 12px;
  text-align: left;
}

th {
  background-color: var(--color-heading);
  color: white;
  font-weight: 700;
}

/* ガイドライン用のスタイル */
.bad-example {
  background-color: #fbe9e7;
  color: #c62828;
  padding: 8px 16px;
  border-radius: 4px;
}
</style>

# Cursor 実践ガイド

<p style="text-align: center; font-size: 24px; margin-top: 32px;">AIコーディングの始め方</p>

---

## このガイドで学べること

<div class="columns">
<div>

### 対象者
- プログラミング経験者
- Cursor未経験または初学者

</div>
<div>

### 30分で習得
- Cursorの基本機能
- Tabでコード生成
- Ctrl+Kで即座修正
- Ctrl+Lで質問・相談

</div>
</div>

---

## 目次

<div class="columns">
<div>

1. **Cursorとは？**
2. **従来開発との違い**
3. **インストール**
4. **画面の説明**
5. **機能1：Tab補完**
6. **機能2：Ctrl+K編集**
7. **機能3：Ctrl+Lチャット**

</div>
<div>

8. **@シンボル活用**
9. **場面別使い分け**
10. **設定とセキュリティ**
11. **まとめ**
12. **おわりに**

</div>
</div>

---

## Cursorとは？

### AI統合型コードエディタ
**プログラミング効率を劇的に向上させる次世代エディタ**

<div class="columns">
<div>

- **VSCodeベース**  
  使い慣れたUI・拡張機能を活用
- **AI機能標準搭載**  
  コード生成・修正・質問が一体化
- **複数AIモデル対応**  
  OpenAI、Anthropic等を自由選択
- **全言語サポート**  
  JS、Python、Go等あらゆる開発対応

</div>
<div>



</div>
</div>

---

## 従来開発との違い

<div class="columns">
<div>

### 従来の開発
- **コード検索**  
  → 手動でコピペ
- **Stack Overflow検索**  
  → 回答を探して適用
- **手動デバッグ**  
  → 試行錯誤で解決
- **ドキュメント読込**  
  → 理解して実装

</div>
<div>

### Cursor開発
- **コメント記述**  
  → コード自動生成
- **AI質問**  
  → 即座に回答取得
- **エラー共有**  
  → 原因・解決策提示
- **自然言語指示**  
  → 実装完了

</div>
</div>

---



## 3分でインストール

### 簡単セットアップ

1. **[cursor.com](https://cursor.com)** でダウンロード
2. **インストール実行** 
3. **VSCode設定移行**(数ステップ)

---

## 画面の説明

<div class="columns">
<div>

### 主要エリア
- **エディタ領域**  
  コードを書く中心スペース
- **サイドバー**  
  ファイル一覧やAIチャットパネル
- **ターミナル**  
  コマンド実行・デバッグ出力

</div>
<div>

### AI機能の場所
- **Tab補完**  
  エディタ内で自動表示
- **Ctrl+K**  
  選択範囲で起動
- **Ctrl+L**  
  右サイドバーにチャット表示

</div>
</div>

> VSCodeに近い画面構成で、直感的に操作できます。

---



## 機能1：Tab補完

<div class="columns">
<div>

### 使い方
1. **コメント書く**  
   → 実装が自動生成
2. **Tab押す**  
   → 提案を採用
3. **Escape押す**  
   → 提案を拒否


### 活用のコツ
- 日本語コメントOK
- 具体的に書くほど精度UP
- 関数名から推測も可能

</div>
<div>

### 実践例
```javascript
// ユーザー認証のAPIコール関数
// ↓ Tabで以下が自動生成
async function authenticateUser(
  email, password
) {
  const response = await fetch(
    '/api/auth', {
    method: 'POST',
    headers: { 
      'Content-Type': 'application/json' 
    },
    body: JSON.stringify({ 
      email, password 
    })
  });
  return response.json();
}
```

</div>
</div>

---

## 機能2：Ctrl+K編集

<div class="columns">
<div>

### 使い方
1. **コード選択**
2. **Ctrl+K押す**
3. **自然言語で指示**

### 活用場面
- リファクタリング
- バグ修正
- スタイル統一
- パフォーマンス改善

</div>
<div>

### 実践例
```python
# 選択したコード
def process_data(data):
    result = []
    for item in data:
        if item > 0:
            result.append(item * 2)
    return result

# Ctrl+K → 「リスト内包表記に」
# ↓ 自動で変換
def process_data(data):
    return [item * 2 
            for item in data 
            if item > 0]
```

</div>
</div>


---

## 機能3：Ctrl+Lチャット（最強機能）

### 使い方
1. **Ctrl+L押す**
2. **質問・依頼入力**
3. **AIが回答・実行**

### 特徴
- **右サイドバーに表示**
- **コンテキスト理解**
- **3つのモードで使い分け**
- **@シンボルが豊富**

---

## Ctrl+L 3つのモード使い分け

<div class="columns">
<div>

#### 🤖 Agentモード
**作業してほしい時**
- コード変更・ファイル作成
- 自動実行・テスト

```
「ユーザー登録API作成」
→ 全自動で実装
```

#### ❓ Askモード  
**理解したい時**
- 説明のみ（変更なし）
- 原因分析・調査

```
「この関数の役割は？」
→ 詳細説明のみ
```

</div>
<div>

#### ✏️ Manualモード
**精密作業したい時**
- コンテキストの挿入を自身で行う

```
「api.tsのみ修正」
→ 他に影響なし
```

#### 💡 使い分けのコツ
- **大規模変更** → Agent(普段はこれだけでも十分)
- **理解・学習** → Ask  
- **細かい調整** → Manual

</div>
</div>

---

## @シンボルで精度アップ

<div class="columns">
<div>

### 使える@シンボル
- **@ファイル名**  
  特定ファイル参照
- **@web**  
  URL先のページ参照
- **@terminal**  
  ターミナル出力共有
- **@フォルダ名**  
  フォルダ全体参照

</div>
<div>

### 実践例
```
@src/api.ts にエラー処理追加
@terminal のエラーを解決
@web https://react.dev 参考に
@src/ 全体をリファクタリング
```

</div>
</div>



---


## 今すぐ試せる実践テクニック

<div class="columns">
<div>

### 1. コメント駆動開発
```javascript
// ユーザーデータを取得して
// フィルタリング
// → Tabで実装自動生成
```

### 2. エラー即解決
```
@terminal のエラーを解決
→ 原因分析＋修正コード提示
```

</div>
<div>

### 3. リファクタリング
```
// 選択範囲でCtrl+K
「パフォーマンス最適化して」
→ 改善コード自動生成
```

### 4. テスト生成
```
// 関数選択してCtrl+K
「ユニットテスト作成」
→ テストコード自動生成
```

</div>
</div>

---

## 設定：.cursorignore作成

<div class="columns">
<div>

### 機密情報を除外
```bash
# .cursorignore作成
.env*
*.key
*.pem
**/secrets/
node_modules/
*.log
```

</div>
<div>

### なぜ必要？
- **APIキー漏洩防止**
- **プライバシー保護**
- **処理速度向上**

### 設定確認
設定 > Privacy >  
Cursor Privacy Mode

</div>
</div>


---

## よくある失敗と対策

<div class="columns">
<div>

### ❌ 失敗パターン

#### 曖昧な指示
「コード改善して」  
→ 何も変わらない

#### コンテキスト不足
「エラー修正」  
→ 見当違いの提案

#### 範囲指定なし
「全部リファクタリング」  
→ 予期しない大変更

</div>
<div>

### ✅ 成功パターン

#### 具体的指示
「ループをmap関数に変更」  
→ 的確な修正

#### 情報提供
「@terminal のエラーを修正」  
→ 正確な解決

#### 範囲限定
「@api.ts のみ最適化」  
→ 安全な改善

</div>
</div>

---

## まとめ：今すぐアクション

<div class="columns">
<div>

### 覚えるのは3つだけ
1. **Tab** - コード生成
2. **Ctrl+K** - コード修正  
3. **Ctrl+L** - 質問・相談

</div>
<div>

### あとは実践するだけ

- **テスト作成**  
  「この関数のテストコードを書いて」と依頼すれば、AIが自動でテストを生成します。

- **コードレビュー**  
  「このコードをレビューして」と指示すると、改善点や指摘をAIが提示します。

- **コード解説**  
  「この関数の動作を解説して」と入力すれば、初心者にも分かりやすい説明が得られます。

</div>
</div>



---

## おわりに

> **Cursor** には  
> - **mcp**  
> - **cursorrules**  
> など、ここで紹介しきれないほど多彩な機能があります。  
> 
> たとえば  
> - **PR作成の自動化**  
> - **mcpによる外部サービス操作**  
> - **cursorrulesでのAI挙動カスタマイズ**  
> など、工夫次第で活用の幅は無限大です。

---