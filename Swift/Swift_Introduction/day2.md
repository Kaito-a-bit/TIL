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
  →強制アンラップ
  
