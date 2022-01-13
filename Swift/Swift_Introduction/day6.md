第5章 制御構文（2)
---
・**whereを使用したswitch文**  
whereでケースにマッチする条件を追加することができる。  
```Swift
  switch optA {
  case .some(let a) where a > 10: //(let aでアンラップされた定数を宣言している)
    print("10より大きい値\(a)が存在します。")
  default:
    print("値が存在しない、もしくは10以下です。")
}
```

・**`ラベルとbreak`**  
ラベルによってswitch文を参照することが可能になる。  
`ラベル名: switch文`で書き、参照したい時には`break ラベル名`とする。  
```Swift
  outerSwitch: switch value {
  case let int as Int:
      let description: String
      switch int {
      case 1,3,5,7,9:
        description = "奇数"
      case 2,4,6,8,10:
        description = "偶数"
      default:
        print("対象外の値です")
        break outerSwitch
      }
      print("値は\(description)です")
  default:
    print("対象外の型の値です。")
  }
```
19行目 `case let(var)` と書くことで判別対象を定数もしくは変数として取ることができる。  
また同時に`case let int as Int`とキャストしている。このように書くと、そのcaseのスコープ内でアンラップする必要がない。  
ここでは「Int型であった場合にキャストして、アンラップした定数として扱う」ことを意味している。  

> _A switch case can name the value or values it matches to temporary constants or variables, for use in the body of the case. This behavior is known as value binding, because the values are bound to temporary constants or variables within the case’s body._
> [the swift programming language](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)


・**Switchとタプル**
Switch文ではタプルを判別対象とすることもできる。  
```Swift
    let somePoint = (1, 1)
    switch somePoint {
    case (0, 0):
        print("\(somePoint) is at the origin")
    case (_, 0):
        print("\(somePoint) is on the x-axis")
    case (0, _):
        print("\(somePoint) is on the y-axis")
    case (-2...2, -2...2):
        print("\(somePoint) is inside the box")
    default:
        print("\(somePoint) is outside of the box")
    }
    // Prints "(1, 1) is inside the box"
```

`_`はワイルドカードと呼ばれる。取り得るどの値にもマッチさせたい時に使用する。  



