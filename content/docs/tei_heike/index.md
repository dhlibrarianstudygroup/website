---
title: "TEIマークアップ"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
## はしがき
勉強会はDHに関する文献の読書会からスタートした。読書会では"Digital Humanities in the Library : Challenges and Opportunities for Subject Specialists"（注）を読み進めたが、その中ではTEI（Text Encoding Initiative）に関する取り組みがしばしば紹介されており、読書会が進むにつれてメンバーの中でTEIに対する興味・関心が高まっていった。理論だけではなく、実際に手を動かしてDHについてより深く学びたいという意見が出たことや、TEIマークアップの経験があるメンバーがいたこともあり、 勉強会でTEIマークアップを実践することになった。  
勉強会ではTEIマークアップの練習台として『平家物語』百二十句本の京都府立京都学・歴彩館蔵本と国立国会図書館蔵本の二本を選択した。マークアップした章段は「扇の的」。選定にあたり、考慮したことは次の3点である。

- 有名な日本古典文学作品であること
- ほどよく異同があり、校異情報のマークアップの練習ができること
- 原本の画像がインターネット上で公開されていること

なお、翻刻は勉強会メンバーが担当した。

（注）Arianne, H.,Laura, B and Liorah, G (Eds.): Digital Humanities in the Library: Challenges and Opportunities for Subject Specialists,Association of Research Libraries (2015).

## マークアップの方針
以下は勉強会で『平家物語』「扇の的」にTEIマークアップを実践するにあたり、共有したマークアップの方針を例を挙げながら整理したものである。なお、方針の策定にあたっては下記ページを参考にさせていただいた。  

参考：日本語古典籍TEI本文データ作成要領  
https://github.com/TEI-EAJ/jpn_classical/blob/master/jpn_classical_guideline.md

### 異同箇所のマークアップについて
使用した京都府立京都学・歴彩館蔵本（以下、「京都本」と称する）と国立国会図書館蔵本（以下、「国会本」と称する）はそれぞれ国書データベースと国立国会図書館デジタルコレクションで原本の画像が公開されている。  
京都本は704コマ目から、国会本は15コマ目からが今回マークアップに取り組んだ「扇の的」の章段にあたる。

京都本：https://kokusho.nijl.ac.jp/biblio/100171975/704  
国会本：https://dl.ndl.go.jp/pid/2546105/1/15  

諸本の情報は`<listWit>`を用いて`<sourceDesc>`の中に次のように記述。  

~~~
<listWit>
<witness xml:id="京都">百二十句本　京都本</witness>
<witness xml:id="国会">百二十句本　国会本</witness>
</listWit>
~~~
  
今回は京都本を底本、国会本を対校本とした。  
したがって、異同は次のようにマークアップする（例文の異同箇所は<u>**下線**</u>で表示）。  
（京都本）あ<u>**は**</u>さぬきに平家をそむき  
（国会本）あ<u>**わ**</u>さぬきに平家をそむき  
~~~
<app><lem wit="#京都">あは</lem><rdg wit="#国会">あわ</rdg></app>さぬきに平家をそむき
~~~
このように、底本である京都本については`<lem>`、対校本である国会本は`<rdg>`で囲む。  
先述の`<listWit>`でxmlidをそれぞれ`京都` `国会`としたので、アトリビュートである`wit`の後ろは`#京都` `#国会`とする。

異同は単語単位で取ることとする。  
すなわち、例えば次の文章をマークアップする場合、下記のようにはマークアップしない。  
（京都本）はたそ<u>**て**</u>いろ<u>**え**</u>たるひたゝれに  
（国会本）はたそ<u>**で**</u>いろ<u>**へ**</u>たるひたゝれに  

【誤１】
~~~
はたそ<app><lem wit="#京都">て</lem><rdg wit="#国会">で</rdg></app>
いろ<app><lem wit="#京都">え</lem><rdg wit="#国会">へ</rdg></app>たるひたゝれに
~~~
【誤２】
~~~
<app><lem wit="#京都">はたそていろえ</lem><rdg wit="#国会">はたそでいろへ</rdg></app>たるひたゝれに
~~~  
こちらが正解。
~~~
<app><lem wit="#京都">はたそて</lem><rdg wit="#国会">はたそで</rdg></app>
<app><lem wit="#京都">いろえ</lem><rdg wit="#国会">いろへ</rdg></app>たるひたゝれに
~~~

### 人物情報
人物は`<persName>`でタグ付けする。誰を指すかわかる場合は`<persName corresp="#那須与一">`のようにする。  
`<body>`（本文情報）のうしろ、`<back>`の中にある`<listPerson>`で人物のリストを作ることができる。リストの中身の例は次の通り。  
~~~
<person xml:id="那須与一">
  <persName>
    <surname>那須</surname>
    <forename>与一</forename>
  </persName>
  <idno type="VIAF">http://viaf.org/viaf/6524312</idno>
</person>
~~~
このように、VIAFなどと紐付けることも可能。  
なお、本文でタグ付けしたときの`persName corresp=#`の後ろで使うのは`person xml:id=`の後ろの人名と同じ形。  
（代名詞や役職名など、本文中異なる名前で呼ばれていたとしても、同じ人物を指していることがわかるようにするための統一名）  

### 地名
要領は`<persName>`と同じ。  
地名は`<placeName>`でタグ付けする。どこを指すかわかる場合は`<placeName corresp="#鎌倉">かまくら</placeName>`のようにする。  
`<text>`（本文情報）のうしろ、`<back>`の中にある`<listPlace>`で地名のリストを作ることができる。リストの中身の例は次の通り。  
~~~
<place xml:id="鎌倉">
  <placeName>鎌倉</placeName>
  <location>
    <geo>35.31085 139.54698</geo>
  </location>
  <idno type="GeoNames">https://www.geonames.org/1860672/kamakura.html</idno>
</place>
~~~
本文でタグ付けしたときの`placeName corresp=#`の後ろで使うのは`place xml:id=`の後ろの地名と同じ形。  
`<location><geo>`は緯度・経度の情報。

### 日付
日付は`<date>`でタグ付けする。もし具体的な日付が分かれば`<date when="1900-09-27">`のように記述する。

### ページ（丁）の情報について
各丁、本文の前にページの情報を`<pb>`タグで記述する。  
例えば、16丁裏は次のような感じ。  
~~~
<pb n="16v" facs="https://kokusho.nijl.ac.jp/biblio/100171975/705"/>
~~~
アトリビュートの`n`の後ろに`数字`プラス表であれば`r`、裏であれば`v`でページ（丁）の情報を入れる。  
`facts`の後ろは国書データベースの該当ページのURL。
