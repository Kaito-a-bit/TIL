第6章　関数とクロージャ (2)
---
### クロージャ

・**定義方法**  
```Swift
  { (引数名: 型, 引数名2: 型) -> 戻り値の型 in 
      クロージャの実行時に実行される文
      必要に応じてreturn文で戻り値を返却する
  }
```

ちないみにクロージャは通常の型と同じように扱うことができるので、変数や定数の型や関数の引数として利用することもできる。  
クロージャの型は、`(引数の型) -> 戻り値の型`で表す。  
```
  let closure: (Int) -> Int
  func someFunction(x: (Int) -> Int) {}
```

・**型推論**  
クロージャの**引数と戻り値の**型宣言はクロージャの代入先から推論することによって省略できるケースがある。  
要はクロージャの型が定まっていることで簡潔な表記が可能になっている。  
```Swift
  var closure: (String) -> Int

  closure = { (string: String) -> Int in
      return string.count
  }

  closure("ABC") //3

  closure = { string in
      return string.count * 2
  }

  closure("ABC") //6
```
  
・**クロージャの簡略引数名**  
定義するクロージャの型が推論できる場合は型を省略することができる。  
こういった場合、加えて引数名の定義を省略して、代わりに簡略引数名を利用することもできる。 
簡略引数名は`$`に引数のインデックスを使用する。  
```Swift
  let isEqual: (Int, Int) -> Bool = {
      return $0 == $1
  }

  isEqual(1,3) //false
```

・**クロージャによるキャプチャ**  
クロージャが参照する変数や定数は、クロージャが実行されるスコープが変数や定数が定義されたローカルスコープ外であっても、実行時に利用することができる。  
```Swift
  let greeting: (String) -> String
  do {
      let symbol = "!"
      greeting = { user in
          return "Hello, \(user)\(symbol)"
      }
  }

  greeting("Ishikawa") //"Hello, Ishikawa!"
```

ここでは、 クロージャの実行時に、ローカルスコープで定義されているはずの定数`symbol`を参照できていることが確認できる。  

### 引数としてのクロージャ  
クロージャを関数や別のクロージャの引数として利用する際に有効な仕様が属性とトレイリングクロージャ  
・**属性の指定**  
→escaping属性  
関数に引数として渡されたクロージャが、関数のスコープ外で保持される可能性があることを示す属性  

```Swift
  var queue = [() -> Void]()

  func enqueue(operation: @escaping () -> Void) {
      queue.append(operation)
  }

  enqueue { print("executed!!") }
  enqueue { print("executed!!") }

  queue.forEach{ $0() }
  //各要素が関数だから()をつける
  /*
  executed!!
  executed!!
  */
  
```

関数の引数として与えられるクロージャは、クロージャの配列に格納される。  
つまりここでは**引数として渡されたクロージャが関数のスコープ外で保持される**ため、引数のクロージャに`@escaping`をつける必要がある。  
`@escaping`が指定されていないクロージャは、関数のスコープ外で保持されない。   







  
  
  
  
  


