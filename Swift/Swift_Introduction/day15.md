型の種類（２）
---

・**クラスメソッド・プロパティとスタティックメソッド・プロパティの使い分け**  
基本的にどちらもクラスに紐づく要素を定義することができるが、基準は、**その値がサブクラスで変更される可能性があるかどうか**で決まる。  
```Swift
class A {
    class var className: String {
        return "A"
    }
    
    static var baseClassName: String {
        return "A"
    }
}

class B: A {
    override class var className: String {
        return "B"
    }
    
    //スタティックプロパティはオーバーライドできないのでコンパイルエラー
    override static var baseClassName: String {
        return "A"
    }
}

A.className //"A"
B.className //"B"
A.baseClassName //"A"
```

### イニシャライザの種類と初期化のプロセス  
