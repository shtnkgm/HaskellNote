# Haskellとは
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
