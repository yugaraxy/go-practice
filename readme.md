Goの組み込み型

整数
int, int8, int16, int32, int64, uint, uint8, uint16, uint32, uint64, uintptr, byte, rune

浮動小数点数
float32, float64

複素数
complex64, complex128

文字列
string

真偽値
bool

エラー
error


変数のゼロ値
・Goの変数は明示的な初期化をしなくても使える
    ・ゼロ値という値が設定され、型によっても違う
intやfloat64などの数値 -> 0
string -> ""
bool -> false
error -> nil


定数
・値の変わらないもの
・コンパイル時から値が変わらないもの
・リテラルで記述されることが多い
数値リテラル -> 100, 1.5, 1+4i
文字列リテラル -> "hoge"
ルーンリテラル -> 'A', '世'
真偽値リテラル -> true, false


2進数・8進数・16進数表記
・10進数表記以外にも対応
・数字の前にプレフィックスをつける
10進数 -> 100, 10.5
2進数 -> 0b1100100
8進数 -> 0144, 0o144(Go1.13)
16進数 -> 0x64, 0x1.5p+03(Go1.13)


数字の区切り
・桁を区切りたい場合などに使える
5_000_000_000_000
0b_1010_1010
3.1415_9265

定数式
・定数のみからなる演算式
・コンパイル時に計算される
四則演算 -> 100 + 200 -> 300
シフト演算 -> 1 << 2 -> 4
文字列結合 -> "Hello, " + "世界" -> "Hello, 世界"
関係演算/論理演算 -> !(10 == 20) -> true

名前付き定数
・定数に名前をつけて定義する
・変数定義といたように定数に名前がつけられる

定数の型
・型を持たない定数
・型を明示しない場合に定数は型を持たず、デフォルトの型を持つ
種類 | 例 | デフォルトの型
整数 | 100 | int
浮動小数点数 | 1.5 | float64
複素数 | 1+4i | complex128
ルーン | 'A', '世' | rune
文字列 | "hoge" | string
真偽値 | true | bool

右辺の省略
・名前付き定数定義の右辺が省略できる
・グループ化された名前付き定数で用いられる
・2つ目以降の名前付き定数の右辺を省略できる
・2つ目以降の定数定義の右辺は、1つめの定数の右辺と同じになる


コンポジット型
・複数のデータ型が集まって一つのデータ型になっている
1. 構造体・・・型の異なるデータ型を集めたデータ型
2. 配列・・・同じ型のデータを集めて並べたデータ型
3. スライス・・・配列の一部を切り出したデータ型
4. マップ・・・キーと値をマッピングさせたデータ型

コンポジット型のゼロ値
・データの表現方法によって違う
・構造体や配列は要素が全てゼロ値の値
・スタイスやマップはmakeなどで初期化が必要なためnilとなる
構造体 -> フィールドが全てゼロ値
配列 -> 要素が全てゼロ値
スライス -> nil
マップ -> nil

型リテラル
・型リテラルとは型の具体的な定義を書き下した型の表現方法
・コンポジット型などを表現するために使う
・変数定義やユーザ定義型などで使用する
・リテラルとは、識別子が付与されていないもの、という意味

構造体
・型の異なるデータ型の変数を集めたデータ型
・各変数はフィールドと呼ばれる
・フィールドの型は異なっても良い
・フィールドの型には組み込み型以外も使える
・コンポジット型やユーザ定義型も使える
構造体リテラル
・フィールドを指定して初期化

配列
・同じ型のデータを集めて並べたデータ構造
・要素の型は全て同じ
・要素数が違えば別の型
・要素数は変更できない
・型は型リテラルで記述することが多い

スライス
・配列の一部を切り出したデータ構造
・要素の型は全て同じ
・要素数は型情報に含まない
・背後に配列が存在する

スライスと配列の関係
・スライスはベースとなる配列が存在している

appendの挙動
・容量が足りるばあ愛
    新しい要素をコピーする
    lenを更新する
・容量が足りない場合
    元のおよそ2倍の容量の配列を確保し直す
    配列へのポインタを貼り直す
    元の配列から要素をコピーする
    新しい要素をコピーする
    lenとcapを更新する

マップ
・キーと値をマッピングさせるデータ構造
・キーと値の型を指定する
・キーには「==」で比較できる型しかNG

コンポジット型を要素にする
・コンポジット型を要素として持つコンポジット型
・スライスの要素がスライスの場合(2次元スライス) ex) [][]int
・マップの値がスライスの場合 ex) map[string][]int
・構造体のフィールドの型が構造体

関数
・一連の操作をまとめたもの
・引数で受け取った値をもとに処理を行い戻り値として結果を返す機能
・必ずしも引数や戻り値がなくても良い
・引数:関数の入力となるもの
・戻り値:関数の出力となあるもの
・関数の種類
・組み込み関数 -> 言語の機能として組み込まれている関数
・ユーザ定義関数 -> ユーザが定義した関数

関数呼び出し
・引数を指定して呼び出す
・引数は変数や式を指定しても良い
・引数が複数ある場合はカンマで区切って指定する
・戻り値がある場合は変数に代入したり式中で使う

組み込み関数
print/println -> 表示を行う
make -> コンポジット型の初期化
new -> 指定した型のメモリの確保
len/cap -> スライスなどの長さ/容量を返す
copy -> スライスのコピーを行う
delete -> マップから指定したキーのエントリを削除
complex -> 複素数型を作成
imag/real -> 複素数の虚部/実数部を取得
panic/recover -> パニックを起こす/回復する

関数の定義
・関数の定義方法
func add(x int, y int) int {
    return x + y
}

・複数の戻り値を返す
func swap(x, y int) (int , int) {
    return y, x
}

多値の受け取り方
・カンマで区切って受け取ることができる
x, y := swap(10, 20)
・省略したい場合は＿(ブランク変数)を用いる
x, _ := swap(10, 20)
＿, y := swap(10, 20) _

関数ん定義
func swap(x, y int) (x2, y2 int ) {
    y2, x2 = x, y
    return
}

値の入れ替え
・一時変数なしで値を入れ替えることができる
・右辺もカンマ区切りで式を書くことができる
x, y = y, x

無名関数
・名前のない関数のこと(クロージャーとも呼ばれる)

関数型
関数はファーストクラスオブジェクト
・変数への代入
・引数に渡す
・戻り値で返す

クロージャとよくあるバグ
定義と実行のタイミングを気をつけるべし
・関数外の変数(自由変数)を参照している場合
・実行のタイミングでは値が変わっている可能性がある

値のコピー
代入ではコピーが発生する
・代入元と同じ値がコピーされる
・コピーのため、代入後の変数に変更を加えても代入前の変数には影響を与えない
・関数の引数や戻り値でも同様のことが起きる

ポインタ
変数の格納先のメモリ番地を表す値
・値で渡される型の値に対して破壊的な操作を加える際に利用する

内部でポインタを使っているデータ型
・コンポジット型の一部
    ・スライス、マップ、チャネル
・これらの型はポインタを用いる必要がない

メソッド
レシーバと紐づけられた関数
・データとそれに対する操作を紐づけるために用いる
・ドットでメソッドにアクセスする

レシーバ
メソッドに関連づけられた変数
・メソッド呼び出し時には通常の引数と同じような扱いになる
・ポインタを用いることでレシーバへの変更を呼び出し元に伝えることができる

メソッド値
メソッドも値として扱える
・レシーバは束縛された状態

メソッド式
・メソッドを表す式
・レシーバを第一引数とした関数になる

