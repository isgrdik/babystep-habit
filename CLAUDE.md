# プロジェクト概要
古川武士「あきれるほど小さい習慣」の読者向けLINEサポートサービス登録LP（`index.html`）。
ターゲット：習慣化に挫折した経験がある30〜50代。
トーン：やさしく、背中を押す。押しつけがましくない。

---

# カラー（CSS変数）

```css
--green: #24c45a        /* CTAボタン、アクセント */
--green-dark: #13a947
--green-soft: #e9f8ef   /* アイコン背景など */
--text: #23313d         /* 本文・見出し */
--sub: #5e6c78          /* サブテキスト・補足 */
--line: #e1edf0         /* ボーダー */
--card: #ffffff
--radius: 22px
```

- ハードコードの色は使わず、必ずCSS変数で管理する
- テキストカラーは `var(--text)`（本文）または `var(--sub)`（補足）を使う

---

# タイポグラフィ

- フォント: Noto Sans JP（システムフォントフォールバックあり）
- 大見出し（h1）: clamp(28px, 8.2vw, 42px), font-weight: 600
- 中見出し（h2）: clamp(23px, 6.4vw, 31px), font-weight: 600
- 本文: 16px, line-height: 1.78
- 補足テキスト: 13px, color: var(--sub)
- 改行制御: `<span style="white-space:nowrap">` で語句の途中改行を防ぐ

---

# レイアウト

- 最大幅: 520px（スマホファースト、縦長LP）
- 広幅（760px〜）では最大1080pxに拡張
- 中央揃え（`.page` で管理）
- セクション padding: 56px 0（border-topなし、余白で区切る）
- カード border-radius: 22px（`--radius`）
- ドロップシャドウ: 0 10px 28px rgba(38,58,75,.07)

---

# セクション構成

1. **トップバー** - ロゴ画像 + 「古川武士「あきれるほど小さい習慣」実践サポート」
2. **ヒーロー** - 書籍画像（左）+ キャッチコピー・CTAボタン（右）
3. **共感セクション** - 「今度こそ続けたい、と思ったけどこんなことはありませんか？」3枚カード（イラスト入り）
4. **ブリッジ** - 「本を読むだけでは、習慣は変わりません。」+ 下向きシェブロン
5. **仕組みセクション** - テキスト（左）+ スマホモックアップ（右）
6. **4ステップ** - テキストのみ、SPは縦積み＋下向きシェブロン区切り、PCは横並び
7. **習慣カテゴリ** - 6テーマ（早起き・運動・勉強・片付け・脱スマホ・その他）
8. **安心3カード** - プライバシー・個人情報・無料
9. **フォーム（#form）** - メアド入力 → プライバシー同意チェック → 送信ボタン
10. **FAQ** - アコーディオン形式

---

# CTAボタン仕様（`.cta`）

- テキスト: 「無料ではじめる」に統一
- 背景: linear-gradient(#2bdc62, #19b84f)
- テキスト: 白, 17px, bold
- border-radius: 999px（pill型）
- 幅: 100%（モバイル）、max-width: 380px（デスクトップ）
- アイコン: SVGメールアイコン（封筒型）を左に添える

---

# フォーム仕様

- メアド入力はチェックなしでも入力可能
- 送信時にプライバシーポリシーの同意チェックを確認
- 未チェックで送信すると「※プライバシーポリシーに同意するにチェックを入れてください」を表示
- 「プライバシーポリシー」のテキストをクリックでモーダル表示（`privacy.md` をfetchしてmarked.jsでレンダリング）
- 送信成功時はフォームを非表示にして完了メッセージを表示

---

# ルール（禁止事項）

- jQueryは使わない、バニラJSのみ
- インラインstyleは書かない、classで管理（改行制御の `white-space:nowrap` のみ例外）
- 画像にはすべてalt属性を入れる
- 外部CSSフレームワーク（Bootstrap等）は使わない
- font-awesomeは使わない、アイコンはSVGか絵文字で代替
- セクション間のボーダーラインは使わない（余白で区切る）

---

# クラス命名規則（実装済み）

- セクション: `.empathy-section`, `.bridge-section`, `.mechanism-section`, `.steps-section`, `.trust-section`, `.form-section`
- ボタン: `.cta`
- カード: `.card`
- コンテナ: `.page`

---

# 画像ファイル

- `images/favicon.png` … ファビコン
- `images/icon.png` … トップバーのロゴ（ベビステちゃん）
- `images/hero-pc.png` / `images/hero-sp.png` … ヒーローの書影画像（PC/SP）
- `images/illust1.png`〜`images/illust3.png` … 共感セクションのイラスト
- `images/mechanism-illust-pc.png` / `images/Mechanism-illust-sp.png` … 仕組みセクションのベビステちゃん画像（PC/SP）
- `images/form-success-area-pc.png` / `images/form-success-area-sp.png` … フォーム送信完了時の画像（PC/SP）
- `images/profile.png` … 監修者プロフィール写真
- `images/book.png` … 関連書籍の書影

Markdownパーサー（`privacy.md` 表示用）は `marked.js` をCDN（jsDelivr）から読み込む形式に変更済み。`images/` にローカルファイルとしては置かない。

---

# デザインメモ

- 全体的にやわらかい印象。角丸多用。
- グリーンを差し色として要所に使う（多用しない）
- セクション間のボーダーは廃止、余白で区切る
- ステップ説明はSP縦積み（シェブロン区切り）、PC横並び（右向きシェブロン）
- スマホモックアップはHTMLで再現（LINEチャット風）
