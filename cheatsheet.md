マークダウン記法
<div style="text-align: right">
文責：岩崎　遥
</div>

# 箇条書き
- サンプル
	- sample
	- sample
- サンプル
- サンプル

# 番号付きリスト
1. 1番目
2. 2番目
3.半角なし

# 引用
### 引用
>お世話になっております岩崎です。
>
>ご連絡いただいた件に関しまして。

### 二重引用
>お世話になっております岩崎です。
>
>ご連絡いただいた件に関しまして。
>
>>こんにちは
>>
>>あああああ

# code記法 インストールコマンドは`sudo apt-get install`です
- バッククォーテーションを一回押すと自動認識するので画面に表示されないがそこは注意が必要です。

# 強調表示<イタリック>
normal *italic* normal

normal _italic_ normal
- アンダーバーかアスタリスクで囲う

# 強調表示<ストロング>
normal **strong** normal
normal __normal__ normal
- アンダーバー、アスタリスク2つで囲う

# 強調表示+イタリック
normal ***strongitalic*** normal
normal ___strongitalic___
- アンダーバー、アスタリスク3つで囲う

# 水平線
***
sample text
***

見出し＋水平線(ハイフン3つ)
---
sample

___
アンダーバーで囲う
___


# リンク
[Google先生](https://google.com)
>
へのリンクです。

- 書き方は[名前]のあとに(URL)を記述する

https://google.com

# 取り消し線
~~なんでやねん~~
- チルダ〜2つで取り消し線の記述

# pre記法
~~~
class hoge
	def hogehoge
		print'hoge'
	end
end
~~~
- 〜3つで囲う

# pre記法（シンタックスハイライト)
~~~python
class python:
	def function():
		print('hogehoge')
~~~
- チルダ3つのあとに言語名を記載する
# 表組み

|test1|test2|test3|
|:--|--:|:--:|
|align left|align right|align center|
|a|b|c|

# 数式
$$ e^{ i\pi }=-1\\
e^{i\theta} = cos\theta + isin\theta$$

- チルダ3つのあとにmathと記載してもOK

# チェックボックス
- [x] yes
- [ ] no

# json形式によるグラフの描画
### 棒グラフ
```chart
{
"type": "bar",
    "data": {
      "labels": ["8月1日", "8月2日", "8月3日", "8月4日", "8月5日", "8月6日", "8月7日"],
      "datasets": [
        {
          "label": "A店 来客数",
          "data": [62, 65, 93, 85, 51, 66, 47],
          "backgroundColor": "rgba(219,39,91,0.5)"
        },{
          "label": "B店 来客数",
          "data": [55, 45, 73, 75, 41, 45, 58],
          "backgroundColor": "rgba(130,201,169,0.5)"
        },{
          "label": "C店 来客数",
          "data": [33, 45, 62, 55, 31, 45, 38],
          "backgroundColor": "rgba(255,183,76,0.5)"
        }
      ]
    },
    "options": {}
}
```
### 円グラフ
```chart
{
"type": "pie",
    "data": {
      "labels": ["8月1日", "8月2日", "8月3日", "8月4日", "8月5日", "8月6日", "8月7日"],
      "datasets": [
        {
          "label": "A店 来客数",
          "data": [62, 65, 93, 85, 51, 66, 47],
          "backgroundColor": "rgba(219,39,91,0.5)"
        },{
          "label": "B店 来客数",
          "data": [55, 45, 73, 75, 41, 45, 58],
          "backgroundColor": "rgba(130,201,169,0.5)"
        },{
          "label": "C店 来客数",
          "data": [33, 45, 62, 55, 31, 45, 38], "backgroundColor": "rgba(255,183,76,0.5)"
        }
      ]
    },
    "options": {}
}
```
- チルダ3つのあとにjsonと記載
- json形式で表記する必要があります

