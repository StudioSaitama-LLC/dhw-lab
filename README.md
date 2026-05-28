# 現実科学研究所 LP（プロトタイプ実装）

design.md v0.2 に厳密準拠した LP のプロトタイプ実装。
Claude Design からハンドオフされたバンドルを apps/lp/ に配置したもの。

## デザインバリエーション

| パス | バージョン | 特徴 |
|---|---|---|
| `/` | **v0**（本ディレクトリ） | クリーム × 5色限定多色 × 三声部対位法 × ポスター組版 |
| `/v1/` | **v1**（[v1/README.md](v1/README.md)） | 紙・墨・朱・燐光（より禁欲的な明朝ベース） |

GitHub Pages 公開後:
- v0: https://studiosaitama-llc.github.io/dhw-lab/
- v1: https://studiosaitama-llc.github.io/dhw-lab/v1/

## 構成

| ファイル | 役割 |
|---|---|
| `index.html` | エントリ。フォント読み込み・CSS / JSX のロード |
| `styles/rsi-tokens.css` | デザイントークン（design.md §4 パレット、§3 タイポ三声部） |
| `styles/lp.css` | LP 全セクションのレイアウト・コンポーネント CSS |
| `components-lp.jsx` | 共有コンポーネント（TopBar / Footer / ContourField / WordCycle / ChapterMark） |
| `sections-1.jsx` | § 00 Hero ／ § 01 Concept ／ § 02 Mission |
| `sections-2.jsx` | § 03 Projects ／ § 04 Values ／ § 05 Contact |
| `app-lp.jsx` | App コンポジション（全セクションの組み立て） |

## 技術スタック

- **React 18.3.1**（CDN／UMD ビルド）
- **Babel Standalone**（ブラウザ内 JSX 変換）
- **Google Fonts**：DM Serif Display, Cormorant Garamond, Zen Old Mincho, Zen Kaku Gothic Antique, Shippori Mincho B1, JetBrains Mono
- ビルド不要のプロトタイプ。本実装は Vite + React or Astro への移行を想定

## ローカル起動

Babel Standalone が JSX ファイルを fetch するため、`file://` ではなく HTTP サーバ経由で開く必要がある。

```bash
# 方法1: Python（macOS 標準）
cd /Users/chiakikato/Projects/studiosaitama/clients/dhw-lab/apps/lp
python3 -m http.server 5173

# 方法2: Node.js（npx）
npx serve .

# その後ブラウザで
open http://localhost:5173/
```

## design.md v0.2 との対応

| design.md 章 | 実装箇所 |
|---|---|
| §4.2 基盤パレット（Crema / Ink / Vermilion / Teal / Indigo） | `styles/rsi-tokens.css` :root |
| §4.3 スケール別カラー（Pink / Violet / Yellow / Orange） | `styles/rsi-tokens.css` :root |
| §3.2 三声部書体（voice-1/2/3） | `styles/rsi-tokens.css` --voice-* |
| §5.2-1 WordCycle（Hero テキスト差し替え） | `components-lp.jsx` WordCycle |
| §2.3 等高線レイヤー（構造的揺らぎ） | `components-lp.jsx` ContourField |
| §2.4 カルーシュ（§ 章番号の色面化） | `components-lp.jsx` ChapterMark, `styles/lp.css` .cartouche |
| §2.5 印刷の温度（グレイン） | `styles/lp.css` .grain::after |
| §8.1 LP 章立て（§00〜§05） | `sections-1.jsx` / `sections-2.jsx` |
| §8.1 色の物語（Crema → 色面 → Vermilion → Ink） | 各セクションの background |

## セクション構成

| § | セクション | コンポーネント | 主背景色 |
|---|---|---|---|
| § 00 | Hero | `Hero` (sections-1) | Indigo `#2D3B8C` |
| § 01 | Concept（現実編集 4命題） | `Concept` (sections-1) | Crema `#F4E9D2` |
| § 02 | Mission（世界を満たせ） | `Mission` (sections-1) | Crema → 色相循環 |
| § 03 | Projects（4スケール） | `Projects` (sections-2) | Pink / Violet / Yellow / Orange |
| § 04 | Values（三柱） | `Values` (sections-2) | Ink `#1A1A18` |
| § 05 | Contact（参画フォーム） | `Contact` (sections-2) | Vermilion `#E54B2A` |
| Footer | フッター | `Footer` (components) | Ink |

## 次工程

1. **クライアントレビュー** ― 藤井学長 / 学長室 / DHU 広報
2. **本番ビルド移行** ― Vite + React (TS) or Astro 静的サイトへ
3. **コンテンツ更新** ― press-release-v0.5 / 趣意書 v2 の最終確定版を反映
4. **応募フォーム実装** ― 現在は alert モック。Tally / Google Forms / 自前 API に差し替え
5. **写真ディレクション** ― §08 学長ポートレート、その他キービジュアル
6. **アクセシビリティ検証** ― キーボード操作 / prefers-reduced-motion / コントラスト比

## ハンドオフ元

- Claude Design バンドル: `wO1i5nZPnQzO25Nk2eHxfw`
- 受領日: 2026-05-29
- 上位文脈: `../../docs/design.md` v0.2 / `../../docs/press-release-v0.5.md`
