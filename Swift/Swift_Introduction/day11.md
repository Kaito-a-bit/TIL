第7章 型の構成要素
---
Swiftの型は、クラス、構造体、列挙型として定義できる。  
インスタンス→**型を実体化したものである**   
インスタンス化する際には、型名に`()`をつけてイニシャライザを呼び出す。

・**型の持つプロパティについて**  
プロパティの型の整合性を保つために、インスタンス化の完了までに全てのプロパティに値が代入されていなければいけない。  
従って、全てのプロパティが  
- 宣言時に初期値を保っている
- イニシャライザ内で初期化される  

上記のいずれかの方法で値を持つ必要がある。  

・**紐付け対象による分類**  
**インスタンスプロパティ**  
型のインスタンスに紐づくプロパティである。つまり、インスタンスごとに異なる値を持たせることができる。  
```Swift
struct Greeting {
    var to = "Yosuke Ishikawa"
    var body = "hello"
}

let greeting1 = Greeting()
var greeting2 = Greeting()
greeting2.to = "Yusei Nishiyama"

let to1 = greeting1.to //Yosuke Ishikawa
let to2 = greeting2.to //Yusei Nishiyama

```

**スタティックプロパティ**  
**型自身に紐づく**プロパティである。インスタンス間で共通する値の保持などに用いられる。  
`型名.プロパティ名`でアクセス
```Swift
struct Greeting {
    static let signature = "Sent from iPhone"
    
    var to = "Yosuke Ishikawa"
    var body = "Hello"
}
```
上記の例では、インスタンスを複数生成してもsignatureプロパティの持つ値は共通して保持される。  

**ストアドプロパティ（上記の分類とは別として）**  
値を代入して　保持するのがストアドプロパティである。

**プロパティオブザーバ**  
ストアドプロパティの値の変更を関しし、変更前と変更後に文を実行するのがプロパティオブザーバである。  
`willSet`, `didSet`を用いて定義する。  
```Swift
struct Greeting {
    var to = "Yosuke Ishikawa" {
        willSet {
            print("willSet: (to: \(self.to), newValue: \(newValue))")
        }
        
        didSet {
            print("didSet: (to: \(self.to))")
        }
    }
}

var greeting = Greeting()
greeting.to = "Yosuke Nishiyama"

```

プロパティの値が変更されるタイミングで処理が実行される。  

**レイジーストアドプロパティ**  
アクセスされるまで初期化を遅延させることができるプロパティである。  
🚨`let`による再代入不可能なプロパティには使用できない。  
```Swift
struct SomeStruct {
    var value: Int = {
        print("valueの値を生成します。")
        return 1
    }()

    lazy var lazyValue: Int = {
        print("lazyValueの値を生成します。")
        return 2
    }()
}

var someStruct = SomeStruct()
print("SomeStructをインスタンス化しました。")
print("valueの値は\(someStruct.value)です。")
print("lazyValueの値は\(someStruct.lazyValue)です。")

//実行結果
valueの値を生成します。
SomeStructをインスタンス化しました。
valueの値は1です。
lazyValueの値を生成します。
lazyValueの値は2です。

```
このプロパティを用いることで、初期化コストの高いプロパティの初期化をアクセス時まで伸ばし、アプリのパフォーマンスを向上させることができる。  

**コンピューテッドプロパティ**  

プロパティ自身では、値を保持せず、既に存在するストアドプロパティなどから計算して値を返す。  
ゲッターとセッターを指定する。前者は、プロパティの値を返す処理、後者はプロパティの値を更新する処理。  

・**ゲッター**  
他のストアドプロパティなどから値を取得して、コンピューテッドプロパティの値として返す。  
値の返却には`return`を用いる。  
```Swift
struct Greeting {
    var to = "Yosuke Ishikawa"
    var body: String {
        get {
            return "hello, \(to)!"
        }
    }
}

let greeting = Greeting()
greeting.body //"Hello, Yosuke Ishikawa!"

```

・**セッター**  
プロパティに代入された値を使用して、他のストアドプロパティなどを更新する。  
セッター内では暗黙的に宣言された`newValueという定数を通じて代入された値にアクセスできる。  
この値を使用して、セッターの実行後に、ゲッターがnewValueを同じ値を返せるようにインスタンスを更新する。  
```Swift
struct Temperature {
    var celsius: Double = 0.0
    
    var fahrenheit: Double {
        get {
            return (9.0 / 5.0) * celsius + 32.0
        }
        
        set {
            celsius = (5.0 / 9.0) * (newValue - 32.0)
        }
    }
}

temperature.celsius = 20
temperature.fahrenheit //68。値を返却

tempetature.fahrenheit = 40 //値を更新
temperature.celsius //10。
```
`get`の定義は必須である。`set`を使用しない場合には、`get`と`{}`を省略してゲッターを記述することが出来る（下記例）。  
セッターの定義の無いコンピューテッドプロパティでは代入による値の変更はできない。プロパティの更新をしようとするとエラーになるので注意。  

```Swift
struct Greeting {
    var to = "Yusuke Ishikawa"
    var body: String {
        return "hello, \(to)!"
    }
}
```







