第8章 型の種類（構造体、クラス、列挙型）
---

### 値の受け渡しによる分類  
上記の三つは**値型か参照型**で分けることができる。両者の最大の違いは、変更を他の定数や変数と共有するかどうかにある。  
値型は変更を共有せず、参照型は共有をする。構造体と列挙型は前者であり、クラスは後者である。  

・**値型**  
インスタンスが値への参照ではなく値そのものを表す。  

・**参照型**  
インスタンスが値への参照を表す。変数や定数への参照型の値の代入は、インスタンスに対する参照の代入を意味する。  
```Swift
class  IntBox {
    var value: Int
    
    init(value: Int) {
        self.value = value
    }
}

extension IntBox {
    func printSelf() {
        print(self.value)
    }
}

var a = IntBox(value: 2) //aはIntBox(value: 1)を参照する。
var b = a //bはaと同じインスタンスを参照する。  

a.printSelf() //2
b.printSelf() //2

a.value = 5

a.printSelf() //5
b.printSelf() //5
```


