---
title: "GitHub共同編集環境"
weight: 6
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
# GitHubでTEI/XMLを共同編集する

### 経緯

---

勉強会でTEIマークアップを進めるにあたって、TEI/XMLを複数人で共同編集する環境が必要となった。
そこで、GitHub Organizationのアカウントを作成し、非公開リポジトリにTEI/XMLや翻刻テキストデータ、作業方針等を置いて作業環境を整えた。

* [若手図書館員DH勉強会のGitHub](https://github.com/dhlibrarianstudygroup)
（2025年1月現在、TEI/XML編集リポジトリは非公開。今後の成果は順次公開予定）


### 前提

---

* Git：オープンソースのバージョン管理システム。
* GitHub：Gitのリモートリポジトリとして利用できる、クラウドベースのプラットフォーム。
* バージョン管理システムを利用することで、ファイルの古いバージョンを参照して差分をチェックしたり、複数人が別々に編集した変更をまとめて取り込んだりすることができる。


### 編集の手順

---

『平家物語』のTEI/XMLを編集する場合：
1. GitHub Organization「dhlibrarianstudygroup」のプライベートリポジトリ「tei_heike」にアクセスする。
2. 画面右上の「Fork」から、Organizationのリポジトリを個人のGitHubアカウントにフォークする。
3. 個人アカウント上でファイルを編集する。（ファイルを開いた直後はプレビューになっているので、右上の「Edit this file」から編集に移行する。）
4. 「Commit changes」から、編集後のリポジトリをmainブランチにコミットする。
5. 個人アカウントでリポジトリ「tei_heike」を開く→「Contribute」からOrganizationにプルリクエストを送る。（=個人アカウントで更新した版を、元のリポジトリにマージしてもらうよう依頼する）
6. Organizationのリポジトリを確認し、プルリクエストが届いていることを確認。問題なさそうであれば、「Merge pull request」ボタンをクリックしてマージする。
7. リポジトリの内容が更新されていることを確認する。
