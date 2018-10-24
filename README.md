# Haskellとは:green_book:
 - 純粋関数型プログラミング言語
   - 何をするかではなく何であるかを伝える
   - 変数を設定したら変更できない
   - 関数は副作用を持たない（副作用: プログラムの状態が変化すること）
     - 純粋関数: 副作用を持たない関数
     - 何かを計算してその結果を返すのみ
     - 参照透明性という性質を持つ（同じ引数で呼ばれたら同じ値を返す）
 - 遅延評価を行う
   - なるべく必要になるまで計算を行わない
   - 参照透明性を持つため、いつ実行してもよい
 - 静的型付け言語
   - 型がコンパイル時に決定する
 - 型推論
 - 命令型のプログラミング言語に比べ、コードは短くバグが少ない
 - 拡張子は.hs
 
# 開発環境
 - Haskell Platform
   - https://www.haskell.org/platform/
   - ghci 対話モードでの起動
   - :q or :quit 対話モードの終了
   - :l ファイル名（拡張しなし）ファイルのロード
   - :r 読み込んだスクリプトをリロード
   - :? ヘルプを見る
   
# はじめの一歩
## 演算子
 - 演算子に優先順位あり（+, -, * , /）%はない
 - 負の値は括弧()でくくらないとエラーが出る
 - 真理値 True, False
 - 論理積 &&
 - 論理和 ||
 - 論理否定演算子 not
 - 同じ型の値が等しい ==
 - 同じ型の値が等しくない /=
 
## 関数呼び出し
 - 演算子も関数
 - 中置関数
 - 前置関数 
 - succ関数（successor, 次に大きい数を返す）
 - min関数 min 1 2
 - max関数 min 1 2
 - 関数の適用は全ての演算の中でもっとも高い優先度を持つ
 - 2引数の前置関数は\`(バッククオート)でかこむと中置関数になる
 
## 関数定義
 - 関数名 引数 = 実装
 - doubleMe x = x * 2
 - doubleUs x y = x * 2 + y * 2
 - 関数定義の中で他の関数も呼べる
 - if文ではelse句が必須（常に何かを返す）
```haskell
doubleSmallNumber x = if x > 100
                        then x
                        else x*2
```
 - 'も関数名ににつかえる（慣習的に使われている）
 - 関数は大文字では始められない
 
## リスト
 - 同じ型の要素を複数格納できる（letは名前の定義）
```haskell
let numbers = [1,2,3]
```
 - リストの連結
```haskell
[1,2,3] ++ [4,5,6]
"hello" ++ "world"
```
 - 文字列は文字のリスト['o','n','e']
 - リストの先頭に追加（cons演算子）
 ```haskell
 'H':"ELLO"
 ```
 - [1,2]は1:2:3:[]の糖衣構文
 - リストへのアクセス
```haskell
 Prelude> "HELLO" !! 1
'E'
```
 - リストのネスト
```haskell
[[1,2,3],[2,3,4,5]]
```
 - 辞書順でのリストの比較 <, >, ==, <=, >=
   - 空でないリストは空リストよりも大きい
 - その他のリスト操作
```haskell
Prelude> head "HELLO" 
'H'
Prelude> tail "HELLO" 
"ELLO"
Prelude> last "HELLO" 
'O'
Prelude> init "HELLO" 
"HELL"
Prelude> length "HELLO" 
5
Prelude> null "HELLO" 
False
Prelude> null "" 
True
Prelude> reverse "HELLO" 
"OLLEH"
Prelude> take 3 "HELLO" 
"HEL"
Prelude> drop 3 "HELLO" 
"LO"
Prelude> maximum [1,4,2]
4
Prelude> sum [1,4,2]
7
Prelude> product [1,4,2]
8
Prelude> elem 4 [1,4,2]
True
```
 - レンジ
```haskell
-- 1から100の整数
[1..100]
```
 - ステップ付きレンジ
```haskell
-- 1から100までの整数のうち、2の倍数
[2,4..100]
-- 1から100までの整数のうち、3の倍数
[3,6..100]
```
 - 無限リスト（遅延評価なので無限に評価することはない）
 ```haskell
 -- 13の倍数のうち、最初の10個
 take 10 [13,26..]
 ```
 - 無限リストの生成関数
```haskell
Prelude> take 10 (cycle [1,2,3])
[1,2,3,1,2,3,1,2,3,1]
Prelude> take 10 (repeat 2)
[2,2,2,2,2,2,2,2,2,2]
Prelude> replicate 4 5
[5,5,5,5]
```

 - 内包表記（リストのフィルタリング、変換、組み合わせを行う方法）
```haskell
-- 20以下の整数を2倍したリスト
Prelude> [x*2 | x <- [1..20]]
[2,4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40]
```
 - 条件（述語）を持つ内包表記
```haskell
Prelude> [x*2 | x <- [1..20], x*2 > 20]
[22,24,26,28,30,32,34,36,38,40]

Prelude> [x | x <- [50..100], x `mod` 7 == 3]
[52,59,66,73,80,87,94]

-- 出力をif文にする
Prelude> [if x > 3 then "A" else "B"  | x <- [1..6], odd x]
["B","B","A"]

-- 複数の述語
Prelude> [ x | x <- [1..10], x /= 3, x /= 4]
[1,2,5,6,7,8,9,10]

-- 複数のリスト（全ての組み合わせ）
Prelude> [ x+y | x <- [1,2], y <- [100, 1000] ]
[101,1001,102,1002]

Prelude> [ x ++ " "  ++ y | x <- ["red", "blue", "green"], y <- ["light", "banana"] ]
["red light","red banana","blue light","blue banana","green light","green banana"]

-- リストから取り出した値を利用しない場合は_
Prelude> let length' xs = sum [1 | _ <- xs]
Prelude> length "HELLO"
5

-- 文字列の処理に内包表記を利用する
Prelude> [ c | c <- "Hello", c `elem` ['A'..'Z']]
"H"
Prelude> [ c | c <- "Hello", c `elem` ['a'..'z']]
"ello"

-- ネストしたリストの操作はネストした内包表記を利用する
Prelude> [ [ x | x <- xs, even x ] | xs <- [[1,2,3], [2,3,4]] ]
[[2],[2,4]]
```
 
