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
イニシャライザの役割は型のインスタンス化の完了までに全てのプロパティを初期化して、型の整合性を保つことである。  
クラスには、これに加えて継承関係があり、様々な階層で定義されたプロパティが初期化されることを指定する必要がある。これを実現するためにSwiftは２段階初期化という方法をクラスに対して採用している。  
２段階初期化において、イニシャライザは指定イニシャライザとコンビニエンスイニシャライザに分類される。  
長いので割愛するが、参考記事をまとめておく.
- [Swiftとイニシャライザ](https://qiita.com/shtnkgm/items/8b7979fc84a3cc065238#%E3%82%A4%E3%83%8B%E3%82%B7%E3%83%A3%E3%83%A9%E3%82%A4%E3%82%B6%E3%81%A8%E3%81%AF)

