CSS3 準拠

# 雑

文字コード合わせるのが基本  
HTML といっしょに合わせておいたほうがお得  
`@charset "utf-8";` & `<meta charset="UTF-8">` など

---

table of contents

- [雑](#雑)
  - [ショートハンド](#ショートハンド)
  - [ベンダープレフィックス](#ベンダープレフィックス)
- [tags](#tags)
  - [cursor](#cursor)
  - [border](#border)
  - [shadow系](#shadow系)
  - [display](#display)
  - [float, overflow, clear](#float-overflow-clear)
  - [疑似要素](#疑似要素)
    - [擬似クラス](#擬似クラス)
  - [gradient](#gradient)
  - [transition](#transition)

---

## ショートハンド

`margin`とか`padding`とか、1 つのプロパティに対して複数の引数を入れるやつで使える  
3 つ指定はあんまりつかわないんじゃね？4 つ指定は「時計回り」を意識

- 例
  - 1 つ指定 (margin: 10px;) : 上下左右すべて同じ値
  - 2 つ指定 (margin: 10px 20px;) : 上下 10px / 左右 20px
  - 3 つ指定 (margin: 10px 20px 0;) : 上 10px / 左右 20px / 下 0px
  - 4 つ指定 (margin: 10px 20px 0 15px;) : 上 10px / 右 20px / 下 0px / 左 15px

## ベンダープレフィックス

あまりにも新しい仕様など、古いブラウザでは一部対応していない CSS 関数 (gradient とか) が存在する (最近は少ないと思う)  
古いブラウザでも見れるようにする必要があるのか、など状況に合わせてベンダープレフィックス (`-webkit-`や`-moz-`などの文字列) を頭につけて、必要に応じて引数を変更する必要がある

MDN Web Docs あたりに詳細が書いてある印象

# tags

並びは適当 誰かアルファベット順ソートとかしといて

## cursor

マウスポインタが要素の上にあるときの状態を指定するプロパティ  
強制的に読込中にしたり利用不可のものにしたりできる

https://developer.mozilla.org/ja/docs/Web/CSS/cursor

## border

枠線 引数は `太さ (大体は1px), スタイル, 色 hex` の順  
例: `border: 1px solid #000` : 太さ1px, 線, 黒色のボーダー 

`border-collapse` を使うとボーダーの重なりを制御できる  
`collapse` でセルのボーダーが重なる (1px同士なら完全に重なる) `separate` でセルが離れる (デフォルト)  
collapse使っとくとなんかいい感じに見えがち

## shadow系
`box-shadow` とか `text-shadow` とかな  
引数は `Xシフト, Yシフト, ぼかし幅, 色 hex alpha可`

## display

インラインにしたりブロック状にしたり  
使いこなすのはちょっとめんどいかも 横並びにしたりするのにつかう

- `display`

  - inline (inline-block) : 子要素の次に余白がある場合、横並び (フッターなどに使用)
  - block : 余白の有り無しにかかわらず、横並び (サイトナビなどに使用)
  - grid : 縦並び (グリッド化、スマホ用 UI で使用？)

- [mdn web docs, display](https://developer.mozilla.org/ja/docs/Web/CSS/display)

## float, overflow, clear

`float`で要素を "浮かせる" ことができる  
サイトロゴとその他ボタンを横並びにするとかでつかう  
その他にも 2 カラムデザインを作るときにメイン部分を`float: left`、サイドバーを`float: right`で横に動かすなど  
Twitter は左 (メニュー)、真ん中 (タイムライン)、右 (トレンドとか検索)の 3 つに分けてそう

しかし `float` で要素を浮かせると高さがなくなる現象が起きる  
影響を受ける要素に対して `clear` で float 要素や回り込みを解除したり、 `overflow` であふれた部分を隠したり (`hidden`) 、あるいはいい感じにやらせる (`auto`) などで対処  
他にもやりようがあるかもしれない 必要に応じて検索ということで

- 参考
  - [mdn web docs, clear](https://developer.mozilla.org/ja/docs/Web/CSS/clear)
  - [mdn web docs, float](https://developer.mozilla.org/ja/docs/Web/CSS/float)
  - [zenn - overflow に関してまとめてみた。](https://zenn.dev/snake12379/articles/d440db8cd8be02)

## 疑似要素

この概念まじでむずい

`::`ではじまる 覚えるの無理だから MDN Docs をよめ
https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements

注意しなければいけないのは

> 1 つのセレクターで使用できる擬似要素は 1 つだけです。擬似要素が現れる場所は、それが現れる複雑セレクターまたは複合セレクター内の他のすべての要素の後でなければなりません。

だろうか セレクターにお気持ちがないと理解難しい説あり

after はなんかちょっとややこしかった https://developer.mozilla.org/ja/docs/Web/CSS/::after

### 擬似クラス

疑似要素と近い `:` ではじまる  
`:hover` とか `:focus` がつかわれがち

擬似クラスと疑似要素は連結できる

```css
p:first-child::first-line {
  font-size: 5000%;
}
```

みたいな感じ

## gradient

`background` や `background-color` に `gradient` 系を指定することでグラデーション  
引数は基本的に `方向, 1つめの色 (hex, alpha%), 2つめの色` で指定する  
方向が無指定の場合は基本的に上から下 (`to bottom` となる)

- `linear-gradient` で線形グラデーション (直線で色が変わっていく)
- `radial-gradient` で円形グラデーション (円形で色が変わっていく, 方向が circle と ellipse)

2016 年ぐらいのブラウザ (あほ古い Chrome とか IE10 とか) だとちゃんとでないかもしれない  
ベンダープレフィックスをつけるなりなんなりで対応

## transition

IE11 も Edge も対応してるからベンダープレフィックスはたぶんいらない  
CSS アニメーションの基本形 難しいことを考えずアニメーションをさせるならこれしかない
引数の順番は `影響させる要素 (background-colorとか 全て影響させるならall), 変化時間, 変化種類`  
変化時間は `100ms` とか `0.1s` とかでの指定が可能

- 変化の種類は以下
  - default: 変化なし
  - ease: 開始と終了をなめらかに
  - ease-in: 開始をゆっくりめに
  - ease-out: 終了をゆっくりめに
  - ease-in-out: 開始と終了をゆっくりめに (ease と何が違うん？)
  - linear: 直線的に
  - cubic-bezier(x1, y1, x2, y2): 3 次ベジェ曲線 4 つの数字をカンマ区切りで指定

ベジェ曲線は数学にお気持ちがないとかなり難しい  
VSCode がいい感じに候補出してくれるからそれで我慢か[cubic-bezier.com](https://cubic-bezier.com/)などのジェネレーターをたよれ

mdn web doc: https://developer.mozilla.org/ja/docs/Web/CSS/transition
