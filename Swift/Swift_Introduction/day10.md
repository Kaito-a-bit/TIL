関数とクロージャ　(3)
---
### 引数とクロージャ  

→autoclousure属性
引数をクロージャで包むことで遅延評価を実現する。  
例が長いので詳細は本を参照。   

・**トレイリング　クロージャ**  
関数の最後の引数がクロージャだった場合に、クロージャを()の外に書くことができる記法。  
```Swift
  func excecute(parameter: Int, handler: (String) -> Void) {
      handler("parameter is \(parameter)")
  }

  //トレイリングクロージャを使用しない場合
  excecute(parameter: 1, handler: { string in
      print(string)  //parameter is 1
  })

  //トレイリングクロージャを使用した場合
  excecute(parameter: 2) { string in
      print(string)  //parameter is 2
  }
```

### クロージャとしての関数  
関数はクロージャの一種であるためクロージャとして扱うことができる。  
クロージャとして扱う場合、関数名だけの式で関数を参照する。  
`let 定数名 = 関数名`  
関数をクロージャとして扱うことで、定数、変数への代入や別の関数の引数に渡すことができる。  
例えば以下はその利点が明確な例。  
```Swift 
  func double(_ x: Int) -> Int {
      return x * 2
  }

  let array1 = [1, 2, 3]
  let doubledArray1 = array1.map(double)
```

・**クロージャを利用した変数、定数の初期化**  
```Swift
  var board1 = Array(repeating: Array(repeating: 1, count: 3), count: 3)
  //[1, 1, 1], [1, 1, 1], [1, 1, 1]

  var board2: [[Int]] = {
      let sideLength = 3
      let row = Array(repeating: 1, count: 3)
      let board2 = Array(repeating: row, count: sideLength)
      return board2
  }()

```
