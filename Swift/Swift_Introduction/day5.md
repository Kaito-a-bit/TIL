第5章 制御構文
---
### 条件分岐
・**if let文も条件分岐**  
`if-let`文もやっていることは条件分岐であり、optionalな値の有無により分岐を行っている。  
値が存在した場合に処理が行われる。値を同時に取り出すことも可能  
```Swift
  let optionalA = optional("a")
  let optionalB = optional("b")
  
  if let a = optionalA, let b = optionalB {
      print("値は\(a)と\(b)です")
  } else {
      print("どちらの値も存在しません。")
  }
  
  //値はaとbです
```

・**if letを用いた、型の安全なダウンキャスト**  
`if let`の右辺で`as?`による型のダウンキャストを行うことができる。  
型による条件分岐を安全に行うことができる。  
```Swift
  let a: Any = 1
  
  //as?演算子は失敗時にはnil, 成功時にはOptional<Wrapped>型を返す。
  if let int = a as? Int { 
      print("値はInt型の\(int)です")
  }
  
  //値はInt型の1です
```

if let文で宣言された定数はスコープ内でのみで使用できる。  

・**guard文**  
`guard`文は条件不成立時に早期退出を行うための条件分岐文。  
`if`文と同様に条件式の評価結果となるBool型の値に応じた処理を行うが、後続の処理を行うにあたってtrueとなっているべき条件を指定する必要がある。  
スコープの中には**guard文が含まれるスコープの外に**退出する処理を記載する必要がある。  
```Swift
  func someFunction() {
      let value = -1
      
      guard value >= 0 else {
          print("0未満の値です")
          return //退出
      }
  }
  
  //0未満の値です
```

・**スコープからの退出の強制**  
guard文のelse節以降では、guard文の条件式が必ず成立していることがコンパイラによって保証される。  
```Swift
  func printIfPositive(_ a: Int) {
      guard a > 0 else {
          return
      }
      
      //guard文以降では a >0 が成立することが保証される
      print(a)
  }
```

・**guard let文**  
if文と同様にguard let文を使用することができる。  
if let文と異なるのは、guard let文で宣言した定数や変数にそれ以降でアクセスすることができる点にある。（guard文以降では、定数や変数の値の存在が保証されているから）  
```Swift
  func someFunction() {
      let a: Any = 1
      
      guard let int = a as? Int else {
          print("aはInt型ではありません")
          return 
      }
      
      print("値は Int型の\(int)です ")
  }
```







