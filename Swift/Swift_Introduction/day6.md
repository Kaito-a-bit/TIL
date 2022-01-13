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





