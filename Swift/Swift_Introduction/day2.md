第3章 基本的な型
---
### Bool型  
・**論理演算**  

**否定** …`!`演算子を用いる
```
let a = true //true
let b = !a //false
```

**論理積** …与えられた複数の真理値がいずれも真であれば真 `&&`を用いる  
**論理和** …与えられた複数の真理値の少なくともどれか1つが真であれば真 `||`を用いる  
```
let a = false && false //false
let b = false && true //false
let c = true && true //true 

let d = false || false //fale
let e = false || true //true
```

### String型
・**数値型との相互変換**  
`String`→`Int, Double`などへの変換は、変換したい文字列が必ずしも数値のフォーマットになっているとは限らない。  
その為、例えばInt型のイニシャライザは`Int?`とオプショナルで返ってくる。（失敗した場合には`nil`）
```
let s1 = "123"
let i1 = Int(s1) ///123

let s2 = "abc"
let i2 = Int(s2) ///nil
```
・**文字列の比較と結合**  
文字列の結合には`append(_ :)`　もしくは`+`を用いる。  
```
var a = "abc"
let b = "def"
let c = a.append(b)  //"abcdef"
```

・**Foundationによる操作**
```
import Foundation

//文字列間の順序を比較（大文字・小文字は無視）
let options = String.CompareOptions.caseInsensitive 
let order = "abc".compare("ABC", options: options)
order == ComparisonResult/orderedSame //true
```

### Optional<Wrapped>型  
・**Optional型の生成の注意点**  
以下はコンパイルエラー
```
  let a: Int? = nil //OK
  let b = nil //元の型が決定しないのでエラー
```

・**Optional<Wrapped>型のアンラップ**  
  →オプショナルバインディング  
  `if let`で宣言した定数に値が存在していればスコープ内の処理が実行される  
  ```
  let optionalA = Optioonal("a")
  if let a = optionalA {
    print(type(of: a))
  }
  ```
  →`??`演算子  
  値が存在しなかった場合のデフォルトの値を与える
  ```
  let optionalInt: Int? = nil
  let int = optionalInt ?? 3 // 3
  ```
  →強制アンラップ  
  `!`で強制的に値を取り出す。やらない方が良い。
  
・**map(_:)**,**flatMap(_:)でアンラップを伴わない値の変更を行う**  
どちらのメソッドも引数には値を変換するクロージャを渡す。
`map(_:)`の例
  
```
  let a = Optional(17)
  let b = a.map({ value in value * 2}) //34
  type(of: b) //Optional<Int>.Type
```
別の型へのキャストも可能
```
  let a = Optional(17)
  let b = a.map({ value in String(value)}) //"17"
  type(of: b) //Optional<String>.Type
```
`flatMap(_:)`の例  
```
  let a = Optional(17)
  let b = a.map({ value in Int(value)}) //17
  type(of: b) //Optional<Int>.Type
```
  
`map(_:), flatMap(_:)`の違いは**クロージャの返り値がアンラップが否か**  
例えば`Stirng→Int`に変換するクロージャを各メソッドに渡したとする。  
前提として、`String→Int`に変換を行った場合の返り値は`Int?`となる。
```
  let a = Optional("17")
  let b = a.flatMap({ value in Int(value)}) //この時点でInt(value)がInt?になっている
  let c = a.map({ value in Int(value)})
  
  type(of: b) // Optional<Int>.Type
  type(of: c) //Optional<Optional<Int>>.Type
```
**即ちOptionalを返すクロージャに対してはflatMap使用する場合が多い  
（逆にOptionalでない値を返すクロージャを渡す場合には両者相違は無い？）**  
参考: [SwiftのOptionalの注意点とmap/flatMap](https://scior.hatenablog.com/entry/2020/03/02/230404)  

・**暗示的にアンラップされたOptional<Wrapped型>**  
型の宣言の際にWrapped!と表記する。わかりやすいのは`ViewController`などの宣言。  
注意するべき点は**アクセスする際に毎回強制アンラップが行われる**こと。即ちアクセス時に`nil`の場合は実行時にエラーが発生する。
```
  let a: Int! = 1
  a + 1 //演算可能
  
  var b: Int = nil
  b + 1 //値が無い為エラー
```
  
### Any型
.**Any型に代入すると型は損失される**
```
  let a: Any = 1
  let b: Any = 2
  a + b //コンパイルエラー
```
  
### Tuple型
・**Tuple型とVoid型**  
  タプル型は複数の型の値を保持することができる。要素の型が0個のタプル型をVoid型という。  
  Void型は**値が存在し得ないことを表す**型。  
  nilはあくまで**値が存在し得る場所で値がないことを示すもの**である。
  
day3に続く

  
