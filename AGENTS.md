# AGENTS.md — medical-student-study

このファイルは Codex CLI / Cursor / Aider / Claude Code / GitHub Copilot Agent など、
AIコーディングアシスタントがこのリポジトリで作業する際の**プロジェクト規約**です。
セッション開始時に必ず読んでください。

---

## プロジェクト概要

**目的**: 札幌医科大学 心臓血管外科 中島智博 が運営する、医学生向けの心血管外科 学習教材サイト。
単一HTMLファイル群を GitHub Pages / Netlify で公開しています。

**公開URL**:
- GitHub Pages: https://ntath-git.github.io/medical-student-study/
- Netlify ミラー: https://fascinating-baklava-23640d.netlify.app/

**ローカル作業ディレクトリ**:
`/Users/tomohironakajima/My Drive/Python_Lesson/2026_MedicalStudent_Study/`

**GitHubリポジトリ**: `NTATH-git/medical-student-study`

**トピック管理(Obsidian側)**:
`/Users/tomohironakajima/My Drive/Python_Lesson/2026_Obsidian/MedicalStudent-Study-Topics.md`

---

## 重要な制約(必ず守ること)

### 🛑 PII / 個人情報
- 公開サイトなので、**患者個人情報・症例画像・実カルテ・実検査値**は絶対に載せない
- 教育目的の架空・一般化した記述のみ
- 学会発表症例も identifiable な情報は禁止

### 🛑 著作権
- 教科書・論文の図表を**そのままコピーしない**
- 必要なら自作SVG/概念図に置き換える
- 引用は文章のみとし、出典(著者・誌名・年・OR/RR等の数値)を明記

### 🛑 ユーザー氏名表記
- 必ず「**中島 智博**(なかじま ともひろ)」
- 「中嶋」「智宏」「智弘」「智浩」は **誤記**(絶対に使わない)
- ローマ字: Tomohiro Nakajima

### 🛑 所属表記(必要な場合)
- 「札幌医科大学 医学部 外科学第二講座 心臓血管外科」
- 英語: "Division of Cardiovascular Surgery, Department of Surgery, Sapporo Medical University, Sapporo, Hokkaido, Japan"
- **Division を Department より先**に書く

---

## デザイン規約(全ページ統一)

### ファイル構造
- **単一HTMLファイル**(CSS/JS すべて埋め込み、外部依存なし)
- ビルドステップ無し ― そのままブラウザで開ける
- ファイル名: `snake_case.html` (例: `cv_catheter_removal.html`)

### カラースキーム(CSS変数)
```css
--navy: #0b2545;        /* ヘッダー、見出し */
--navy-light: #13315c;  /* nav背景、ホバー */
--accent: #c62828;      /* アクセント赤(ボタン、border-left) */
--accent-light: #ef5350;/* page-nav背景(うす赤) */
--bg: #f7f8fa;
--card: #fff;
--text: #1a1a1a;
--muted: #5a6473;
--border: #e1e5ea;
--success: #2e7d32;
--warn: #ef6c00;
--danger: #c62828;
```

### フォント
```css
font-family: -apple-system, BlinkMacSystemFont, "Hiragino Sans", "Yu Gothic", "Meiryo", sans-serif;
```

### 必須UI要素
1. **header**(navyグラデーション、タイトル+サブタイトル+対象学年メタ)
2. **page-nav**(赤バー、左寄せ📚メニューボタン)
3. **nav**(navy、横スクロール可、セクションアンカー一覧)
4. **drawer**(左から出る全ページメニュー、**CSS-only**実装、`#menuToggle:checked ~ .drawer`)
5. **disclaimer**(黄色の学習目的注意書き、ページ冒頭)
6. **section**(各セクション、`border-left:5px solid var(--accent)` の h2)
7. **quiz**(7-10問、選択肢4つ、解説付き、最終得点表示)
8. **glossary**(用語集、英日対訳テーブル)
9. **footer**(目次に戻るリンク、学習目的の注意)
10. **back-to-top** ボタン(右下、スクロールで表示)

### モバイル対応
- `100dvh` + `env(safe-area-inset-bottom)` でドロワーがiOSで切れないように
- `touch-action: manipulation` でタップ応答性
- `@media (hover:hover)` で iOS の first-tap hover 偽動作を防ぐ
- min-height 44px(タップターゲット)

### ドロワーの実装(重要 ― CSS-only)
```html
<input type="checkbox" id="menuToggle" class="menu-toggle-input">
<div class="page-nav">
  <label for="menuToggle" class="page-nav-menu-btn">📚 メニュー</label>
</div>
<!-- ... -->
<label for="menuToggle" class="drawer-backdrop"></label>
<aside class="drawer">
  <div class="drawer-head">
    <label for="menuToggle" class="drawer-close">×</label>
    <h3>📚 全ページメニュー</h3>
  </div>
  <!-- ... -->
</aside>
```
- JSは使わない(iOS/Firefoxでのfirst-tap問題回避のため)
- ×ボタンは **drawer-head の左側**(右側だと指が届きにくい)
- 既存ページの infection_control.html か fr_vs_gauge.html を**そのままコピー**して中身だけ差し替える のが最も安全

---

## 公開済みページ一覧(2026-05-26 時点 32ページ)

### 🫀 心血管総論
- `cardiovascular_surgery_intro.html` — 心血管外科 総論
- `cardiovascular_pressures.html` — 心血管の圧
- `infection_control.html` — 感染制御の総論
- `fr_vs_gauge.html` — Fr とゲージの違い

### 🪡 心臓手術手技
- `avr_open_procedure.html` — 正中切開 AVR
- `brain_isolation_technique.html` — 弓部置換 + Brain Isolation Technique
- `surgical_instruments.html` — 手術器械
- `gowning_technique.html` — ガウンテクニック

### 🫶 補助循環(MCS)
- `iabp.html` / `va_ecmo.html` / `vv_ecmo.html` / `impella.html`

### ⚙️ 体外循環・心筋保護
- `cpb_basics.html` / `myocardial_protection.html` / `cpb_simulator.html`

### 🩺 血管外科
- `evar_endoleak.html` / `mesenteric_iliac_collateral.html`
- `spinal_cord_ischemia.html` / `csf_drainage.html`
- `marfan_syndrome.html` / `loeys_dietz_syndrome.html`

### 💊 周術期管理
- `cv_catheter_removal.html` / `drain_removal.html` / `npwt_basics.html`
- `hit_syndrome.html` / `anticoagulant_management.html`
- `contrast_nephropathy.html` / `hemodialysis_basics.html`
- `chylothorax.html` / `radiation_protection.html`

### 📚 リファレンス
- `body_negative_pressure.html` — 陰圧の生理
- `cvs_glossary.html` — 用語集

### 目次
- `index.html` — トップページ(カード一覧)

---

## 新しいページを追加するときのワークフロー

新規ページを作る場合、以下**4つすべて**を更新すること(忘れがちなので注意):

### Step 1: 新HTMLファイルを作成
- 既存ページ(例: `fr_vs_gauge.html` か `infection_control.html`)をテンプレートとしてコピー
- `<title>`, `<header>`, `<nav>`, 各 `<section>`, クイズ, 用語集を埋める
- ドロワーの `<a class="current">` マークは自動付与されるので不要

### Step 2: index.html を2箇所更新
1. **カードグリッド**: 適切なカテゴリ(`<div class="category">`)内に新カードを追加
   ```html
   <a href="新ファイル名.html" class="card">
     <h4>ページタイトル</h4>
     <p class="desc">概要(60-120文字)</p>
     <div class="tags"><span class="tag all">全学年</span><span class="tag">分野</span></div>
   </a>
   ```
2. **ドロワー**: index.html末尾の `.drawer-content > .drawer-section` 内にも追加

### Step 3: 全既存ページのドロワーを更新
全30+ページの `<aside class="drawer">` 内 `.drawer-section` に新ページのリンクを追加。
Pythonワンライナーで一括処理を推奨(例は本リポジトリのgit log参照)。

### Step 4: Obsidianのトピック管理を更新
`/Users/tomohironakajima/My Drive/Python_Lesson/2026_Obsidian/MedicalStudent-Study-Topics.md`
の「📚 公開済み」セクションの表に1行追加。

### Step 5: コミット & プッシュ
```bash
git add -A
git commit -m "Add [トピック名] page"
git push
```

数分後に GitHub Pages / Netlify 両方に反映されます。

---

## コンテンツ品質ガイドライン

### 各ページの構成(順序)
1. **disclaimer**(学習用注意書き)
2. **概要/総論/なぜ重要か** ― 文脈設定
3. **本論(3-7セクション)** ― 病態・手技・原理など
4. **臨床応用/例/落とし穴**
5. **覚え方/ゴロ合わせ**(任意)
6. **クイズ**(7-10問、4択、解説必須)
7. **用語集**(英日対訳テーブル、15-30項目)
8. **footer**

### 文体
- 「ですます調」または「である調」をページ内で統一
- 既存ページは「ですます調」が主流
- 医学用語は初出で日本語(英語)併記、または英語(日本語)併記
- 重要数値は `<span class="num-highlight">` または `<strong>` でハイライト

### エビデンスの出し方
- メタアナリシス・大規模RCTは著者+年+誌+OR/RRを明記
  - 例: "de Jonge 2017 BJS, OR 0.72 (95%CI 0.59-0.88)"
- ガイドラインは発行団体+年
  - 例: "WHO 2018 Global Guidelines"
- callout `.evidence`(緑) や `.evidence-box` で目立たせる

### 視覚要素
- 大事な対比は **`.vs-grid` + `.vs-card`** (赤vs青の2カラム)
- 3点セットなどは **`.component-grid` + `.component-card`**
- 注意喚起は **`.callout.danger`**(赤)
- ヒントは **`.callout.tip`**(青)
- 一般注意は **`.callout`**(黄)

---

## クロスツール作業時の注意

このリポジトリは複数のAIツール(Claude Code, Codex, Cursorなど)から編集される可能性があります。

### 作業前
```bash
cd "/Users/tomohironakajima/My Drive/Python_Lesson/2026_MedicalStudent_Study/"
git pull origin main
```

### 作業後
```bash
git add -A
git status  # 意図しないファイルが含まれていないか確認
git commit -m "..."
git push origin main
```

### 注意ファイル(コミットしない)
- `.DS_Store` (gitignore済み)
- `【Study】 alias` (macOSエイリアスファイル、untrackedのまま)
- 個人メモ・実症例データ

### Pre-commit hooks
このリポジトリには現在 pre-commit hook は無し。

---

## トラブルシューティング

### ドロワーが正しく開かない / レイアウトが崩れる
過去にCSS-only実装に切り替えた際、古いJS実装のCSSが残存して衝突した事例あり。
チェック項目:
- `.drawer` の重複定義(`right:0` の古い版が残っていないか)
- `_openDrawer`, `_menuBtn` などの古いJS変数

### GitHub Pages がデプロイされない
2026-05-23 にPNG画像追加後 一時的にPagesが止まった経緯あり。
- jsdelivr経由でファイル参照 / Netlifyミラー で回避可能
- Settings → Pages → Build and deployment を再確認

### iOS で first-tap が反応しない
`@media (hover:hover)` で `.page-nav-menu-btn:hover` を囲うこと(`hover:none`なiOSではhover擬似クラスを発火させない)。

---

## このファイルの更新ルール

新規ページ追加・デザイン規約変更・新しい制約が出てきたら、このファイルも一緒に更新してください。
最終更新の日付や更新者を冒頭に書く必要はありません(git log を見れば分かる)。
