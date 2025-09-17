---
title: "TEI/XML編集環境"
weight: 5
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
# VSCodeでTEIを編集する環境を整える

**この記事は2024年8月時点の情報に基づいて作成しています。**

### 前提

---

- XMLファイルの編集には専用のエディタ（編集ソフト）が便利
- TEIの分野ではOxygenが代表的なソフトであるが、ライセンス費用が高価なため、初学者や学術機関に所属していない人には手を出しにくい
- テキストエディタの一つであるVSCodeは様々な拡張機能をインストールすることで機能追加ができる。XMLやTEI/XML編集用の拡張機能も開発・公開されている


### 手順

---

1. **VSCodeのインストール**
    - 下記サイトからOSに応じたインストーラをダウンロードし、実行する。
        - https://code.visualstudio.com/download
    
2. **拡張機能のインストール**
    - Japanese Language Pack for VS Code
        - https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ja
        - UIを日本語表示にするための拡張機能
    - TEI Japanese Editor
        - https://marketplace.visualstudio.com/items?itemName=ldas.vscode-japanese-tei
        - TEI/XMLのマークアップに便利な機能（Webview、ruby・appの入力補助、カスタム表示）が追加できる
        - Webview表示を縦書きにする設定
            - 拡張機能を右クリック＞拡張機能の設定を開く
            - ODDファイル：vs-code-japanese-teiを選択
    - Scholarly XML
        - https://marketplace.visualstudio.com/items?itemName=raffazizzi.sxml
        - XMLの構文（整形式）チェック
        - スキーマに基づいた文書の妥当性チェック
        - 現在の環境で使用できる要素のサジェストとツールチップ
        - Ctrl+Eで選択部分をタグで囲む
    - Auto Close Tag
        - https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-close-tag
    - Auto Rename Tag ★任意
        - https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag 
    - Close HTML/XML tag★任意
        - https://marketplace.visualstudio.com/items?itemName=Compulim.compulim-vscode-closetag
        
3. **日本語スキーマファイルの作成と適用**
    - TEIスキーマ
        - TEI/XMLのタグのルールを記述した「スキーマ」ファイルを用意
        - スキーマファイルを読み込むことで使用できるタグの候補や解説を表示できる
        - デフォルトだとタグの説明は英語だが、日本語用のスキーマファイルを作成すれば、タグの説明は日本語で表示される
    - [Romaの解説](https://digitalnagasaki.hatenablog.com/entry/2017/08/26/095642)
        - スキーマファイルを編集・作成するためのウェブアプリケーション
    - 手順
        - https://romabeta.tei-c.org/ にアクセス
        - TEI_ALL（customize by reducing TEI）を選択し、STARTを押下
        - Language of elements and attributes　と　Documentation Language　を日本語にする
        - 「RELAX NG schema」を選択し、ファイルをダウンロード。任意（ここではTEIファイルと同じ階層）の場所に置く
        
4. **ユーザスニペットの設定**
- ファイル＞ユーザ設定＞ユーザー スニペットの構成＞「新しいスニペット」を選択し、任意のファイル名（ここでは「teiall.json」）で保存する。
- デフォルトで記載されている記述を削除し、下記の文字列をコピペして上書き保存する。
- 2行目<?xml-model href="tei_all.rng" schematypens="http://relaxng.org/ns/structure/1.0" type="application/xml"?>,”のhrefの値には3で作成したスキーマファイルのパス（絶対パス）を記載する。ここではtei_all.rngとこの後作成するxmlファイルが同じ階層にある想定とする。（同じ階層にないとスキーマファイルが認識されない。）

```json
	{"TEI P5 All": {
		"prefix": "teiall",
		"body": [
			"<?xml version=\"1.0\" encoding=\"UTF-8\"?>",
			"<?xml-model href=\"tei_all.rng\" schematypens=\"http://relaxng.org/ns/structure/1.0\" type=\"application/xml\"?>",
			"<TEI xmlns=\"http://www.tei-c.org/ns/1.0\">",
			"  <teiHeader>",
			"      <fileDesc>",
			"         <titleStmt>",
			"            <title>${1:Title}</title>",
			"         </titleStmt>",
			"         <publicationStmt>",
			"            <p>${2:Publication Information}</p>",
			"         </publicationStmt>",
			"         <sourceDesc>",
			"            <p>${3:Information about the source}</p>",
			"         </sourceDesc>",
			"      </fileDesc>",
			"  </teiHeader>",
			"  <text>",
			"      <body>",
			"         <p>${4:Some text here.}</p>",
			"      </body>",
			"  </text>",
			"</TEI>"
		],
		"description": "Oxygen-like TEI (P5) All Boilerplate"
		}
	}
```

### 動作確認

---

- 「ファイル」＞「新しいテキストファイル」でxmlファイルを作成→任意の名前を付けて保存する。
- 「teiall」と入力し、4で作成したユーザスニペットが呼び出せることを確認する。
- 「<」と入力し、候補のTEIタグと日本語の説明文が表示されることを確認する。
- TEIJapaneseEditorの機能
    - コマンドが使えるか
 
    | ショートカット | 動作 | キーボード |
    | --- | --- | -- |
    | Generate panel | プレビューを開く | ctrl+k v |
    | Insert ruby | ルビを挿入する | ctrl+k r |
    | Insert warichu | 割注を挿入する | ctrl+k w |

### 参考サイト

---
- [TEI/XMLファイルの編集を支援するVSCode拡張機能の使用例](https://zenn.dev/nakamura196/articles/d2733cc49d1239)
- [フリーソフトで快適TEI/XML（Oxygenを使わない道） - digitalnagasakiのブログ](https://digitalnagasaki.hatenablog.com/entry/2020/02/14/031218)
- [VSCode で XML（Scholarly XML🚧編） - UTDH / 東京大学人文情報学](https://scrapbox.io/utdh/VSCode_で_XML（Scholarly_XML🚧編）)

