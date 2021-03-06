
# Associator

形状情報での理論値と画像処理での計算値を比較し、ピース番号を対応付けるプログラム。

## Contents

### associator.cpp
- メインのプログラム

### Puzzle.cpp, Puzzle.hpp
- チームメンバーの方が作成されたものを流用した、辺長や面積などを求めるプログラムとヘッダ

### externalディレクトリ
- 出力したHTMLを成形するためのCSSとJavaScript

### sample, sample100, ああああ, 全ピース, 練習フォルダ, A1, 1回戦第3試合、1回戦第3試合半減
- サンプル問題や大会で使われた問題のデータ（形状情報（理論値）と画像処理（計算値））
  - フォルダ名は適当です（名前の意味も忘れました）

## Features

### associator.cpp
- あらかじめ「理論値」「計算値」という名前のフォルダの中にそれぞれ形状情報と画像処理のデータ（ファイル名はどちらも「ピース.txt」）を格納しておき、「理論値」「計算値」と同じ階層に出力したHTMLを整形する「main.css」とHTMLを操作する「script.js」を格納しておく
- 「理論値」や「計算値」のフォルダの親フォルダをコマンドライン引数で指定すると、各フォルダの中にある「ピース.txt」を読み込む
-  各ピースデータ（頂点データ）からピースの角度、辺長、周長、面積を算出する
   - 角度が180±3度の場合、誤検出された頂点とみなしその頂点を削除
- 理論値と計算値の誤差の割合を算出し、指定した以上の差（頂点数の差、周長差、面積差、最大角度差、最小角度差）が出た場合は候補から除外する
- 候補の対応ピースの辺長差、角度差、周長差、面積差を算出し、評価値をつける
   - サンプル問題などの統計から、周長差が少ないものが高評価されるように調整済み
- 評価値順に並べ替え、各ピースに対応しそうランキングベスト5を作成
- HTMLを生成し、ランキング表を生成する
    - 唯一解を求める処理は、ピース数が合わないとほぼ意味を成さず、競技に適さないため削除

### script.js
- 評価値が高いものは青系、中間は緑系、低いものは赤系の背景色をつける
- 表の行をクリックすると評価値の表示を切り替えることができる
    - 評価値を常時表示にすると表が縦に長くなり、視認性が悪くなるため
    - 評価値は、似たピースがたくさんあり高得点ピースが多数ある場合に比較する目的で使うかも…？
- 右ペイン中央にある表の数字は対応ピースの数字と対応しており、クリックすると該当ピースの背景が黒くなる
    - ピースを実際に配置した結果適合していたら、そのピースが他のピースに対応することはないことが一目でわかる

