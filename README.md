# undo/redo環 - undo/redo ring
undoとredoを視覚的に分かりやすくするために作りました。
どこかのプログラムで実装したいときは、これを参考にしながら作ると良いかもしれません。

![参考スクリーンショット](https://cdn.discordapp.com/attachments/624598454387081227/993056556495159346/unknown.png)

(私が思いついた方法なので、より効率的なものは存在する可能性があります。)


## ボタン - buttons
|ボタン名|説明|
|-|-|
|OPERATE|操作をする|
|UNDO|UNDOする|
|REDO|REDOする|
|RESET|最初の状態に戻す|

## 変数 - variables
|変数名|型|説明|
|-|-|-|
|data[]|List|操作を記録しておくための配列|
|startFlag|Bool|dataの数が0のときはfalse、それ以外はtrue|
|undoLimit|int|UNDOできる限界のインデックス|
|redoLimit|int|REDOできる限界のインデックス|
|cursor|int|現在のカーソル位置のインデックス|

## 注意事項
このソフトは[Defold](https://defold.com/)で作成しました。
Defoldで使用されるプログラミング言語は「Lua」であり、その配列のインデックスは**1から**始まります。
通常のインデックスは0から始まるので、注意してください。(というか、ソースコードよりGUIを見ながら理解しましょう。)

それに伴って、`nex(idx)`, `pre(idx)` が特殊な実装になっていますが、インデックスが0から始まるプログラミング言語では楽に実装できます。
(以下はPythonで実装したものです。8はdataサイズです。)

```python
def next(idx: int) -> int:
    return (idx+1) % 8

def prev(idx: int) -> int:
    return (idx-1) % 8
```

