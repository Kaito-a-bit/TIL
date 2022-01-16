第5章 制御構文(3)
---
・**defer文によって遅延実行する**  
defer文において、{}内のコードはdefer文が記述されているスコープの退出時に実行される。  
スコープの退出時に確実に実行されてほしい処理を記述する。  
```Swift 
  var count = 0
  func someFunction() -> Int {
      defer {
          count += 1
      }
      return count
  }
  
  someFunction() //0
  count //1
```

### パターンマッチ  
・**バリューバインディング**  
値を変数や定数に代入するためのパターン。  
`var`もしくは`let`と他のパターンを組み合わせて使用し、組み合わせたパターンがマッチすれば値の代入を行う。  
```Swift
  let value = 3
  
  switch value {
  case let matchedValue:
      print(matchedValue)
  }
```

・**オプショナルパターン**  
Optional型の値の有無を評価する。`識別子?`と記述。  
通常、Optional型の評価式からWrapped型の値を取り出すために、バリューバインディングと組み合わせて使用する。  

```Swift
  let optA = 4?
  switch optA {
  case let a?:
      print(a)  //アンラップされている
  default: 
      print("nil")
  }
```
・**列挙型のパターンと連想値のパターンマッチング**  
列挙型ケースでは、`ケース名(パターン、パターン、...)`という形式で、連想値のパターンマッチングが可能になる。  
連想値とは、列挙型のケースに紐づいた深情報であり、同一のケースでも異なる連想値を持つことができる。 
よくみるのは、連想値のパターンにバリューバインディングを用いた形式。  
```Swift
  enum Color {
    case rgb(Int, Int, Int)
    case cmyk(Int, Int, Int, Int)
  }

  let color = Color.rgb(100, 200, 255)

  switch color {
  case .rgb(let r, let g, let b):
      print(".rgb: (\(r), \(g), \(b)")

  case .cmyk(let c, let m, let y, let k):
      print(".cmyk: (\(c), \(m), \(y), \(k)")
  }
```

### パターンマッチを使用できる場所  
→色々ある。   
・**if**  
条件を網羅したいのであれば`switch`、網羅する必要がないのであれば`if`  
```Swift
  if case 1...10 = value {
      print("1以上10以下の値です。")
  }
```

・**guard**
```Swift
  func someFunction() {
      let value = 9
      guard case 1...10 = value else {
          return
      }
      print("1以上10以下の値です。")
  }

  someFunction()
```

・**for-in**   
```Swift
  let array = [1, 2, 3, 4]

  for case 2...3 in array {
      print("2以上3以下の値です。")
  }
```

・**while**  
```Swift
  var nextValue: Int? = Optional(1)

  while case let value? = nextValue {
      print("value: \(value)")

      if value >= 3 {
          nextValue = nil
      } else {
          nextValue = value + 1
      }
  }

```




