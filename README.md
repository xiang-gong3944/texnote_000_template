# note-000-template

小規模から中規模の研究ノートを書くための、日本語 LaTeX ノート用テンプレートです。

このテンプレートは、リポジトリをシンプルで移植しやすい形に保ち、`texnote_001_foundations` や `texnote_002_codes_and_models` のような新しいノート用リポジトリへ簡単に派生できるように設計しています。

## 基本方針

- 最初は本文を `main.tex` に直接書く。
- 再利用する LaTeX 設定は `notestyle.sty` にまとめる。
- PDF は `latexmk main.tex` でビルドする。
- 既定のコンパイル経路は `uplatex + dvipdfmx` とする。
- 生成された PDF や補助ファイルは、原則として main ブランチにコミットしない。
- PDF のビルドと成果物としてのアップロードは GitHub Actions に任せる。

## リポジトリ名の規則

このテンプレートから派生したノート用リポジトリには、次の形式を使います。

```text
texnote_<3桁の番号>_<短い名前>
```

例:

```text
texnote_000_template
texnote_001_foundations
texnote_002_codes_and_models
texnote_003_topology_and_phases
texnote_004_algorithms_for_physics
```

番号は安定した識別子として扱います。短い名前は人間が読みやすくするための説明であり、ノートの成長にともなって多少実態とずれても構いません。

## ディレクトリ構成

```text
texnote_000_template/
├── README.md
├── LICENSE.md
├── .gitignore
├── .gitattributes
├── .latexmkrc
├── main.tex
├── notestyle.sty
├── references.bib
├── figures/
│   └── .gitkeep
└── .github/
    └── workflows/
        └── build.yml
```

## ビルド

次を実行します。

```bash
latexmk main.tex
```

ビルド設定は `.latexmkrc` に定義されています。

想定している LaTeX エンジンは次の組み合わせです。

```text
uplatex + dvipdfmx
```

## 必要なもの

次のツールを含む TeX ディストリビューションをインストールしてください。

- TeX Live または MacTeX
- latexmk
- uplatex
- dvipdfmx
- upbibtex

推奨する構成は次のとおりです。

```text
Windows: TeX Live
macOS: MacTeX
GitHub Actions: TeX Live ベースの action/container
```

## ファイル名の規則

Windows、macOS、Linux ベースの GitHub Actions のあいだで移植性を保つため、ファイル名には次の文字を使うことを推奨します。

- 小文字の英字
- 数字
- ハイフン
- ASCII 文字のみ

よい例:

```text
main.tex
references.bib
toric-code-lattice.pdf
logical-operator-example.png
```

避ける例:

```text
第1節.tex
Toric Code.png
図1_トーリックコード.PNG
```

## LaTeX スタイルの方針

`main.tex` には、文書ごとに固有の内容を書きます。

- タイトル
- 著者
- 日付
- 本文
- 文書固有のマクロ
- 参考文献の呼び出し

`notestyle.sty` には、再利用する設定を書きます。

- 共通パッケージ
- 定理環境
- ボックス環境
- 共通の数学演算子
- 共有する見た目の設定

目安としては、次のように考えると便利です。

```text
複数のノート用リポジトリで再利用するものは notestyle.sty に置く。
現在のノートだけに属するものは main.tex に残す。
```

## PDF の扱い

生成された PDF は、原則として main ブランチにコミットしません。

代わりに、GitHub Actions で PDF をビルドし、成果物としてアップロードします。

将来的に公開配布が重要になった場合は、次のような方法を検討します。

- GitHub Releases に PDF を添付する。
- GitHub Pages で PDF を公開する。
- コンパイル済み PDF 用の別ブランチを維持する。

## GitHub Actions

初期のワークフローは、次のことだけを行うようにします。

1. push、pull request、または手動実行で起動する。
2. `main.tex` をコンパイルする。
3. 生成された PDF を成果物としてアップロードする。

自動リリースへのアップロードや GitHub Pages へのデプロイのような複雑なワークフローは、基本テンプレートが安定してから追加します。

## このテンプレートから新しいリポジトリを作った後に行うこと

1. `texnote_<番号>_<名前>` の規則に従ってリポジトリ名を変更する。
2. `main.tex` のタイトル、著者、日付を編集する。
3. `main.tex` の導入文を置き換える。
4. 図を `figures/` に追加する。
5. 文献情報を `references.bib` に追加する。
6. ローカルで `latexmk main.tex` が動作することを確認する。
7. GitHub に push し、GitHub Actions で PDF がビルドされることを確認する。

## ライセンス

このテンプレートは MIT License で配布することを想定しています。

派生したノート用リポジトリでは、目的に応じてライセンスを選んでください。

- MIT License: 再利用可能なテンプレートやコードに近い内容に適しています。
- CC BY 4.0: 公開して共有する文章に適しています。
- CC BY-SA 4.0: 継承ライセンスを求める文章に適しています。
- ライセンスなし: 既定では all rights reserved になります。公開再利用を想定する場合は非推奨です。
