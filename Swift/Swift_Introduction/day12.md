第7章 イニシャライザ・メソッド
---
### イニシャライザ
全てのプロパティは、インスタンス化の完了までに値が代入されていなければならないので、プロパティの宣言時に初期値を持たないプロパティは、イニシャライザ内で初期化する必要がある。

・**失敗可能イニシャライザ**  
引数によって初期化に失敗する可能性のあるイニシャライザは失敗可能なものとして表現することができ、結果を`Optional<Wrapped>`型として返す。  

```Swift
struct Item {
    let id: Int
    let title: String
    
    init?(dictionary: [String: Any]) {
        guard let id = dictionary["id"] as? Int,
              let title = dictionary["title"] as? String else {
                  return nil
              }
        self.id = id
        self.title = title
    }
}
```

### メソッド
・**インスタンスメソッド**  
型のインスタンスに紐づくメソッド  

・**スタティックメソッド**  
型自身に紐づくメソッドであり、インスタンスに依存しない処理に使う。  

スタティックメソッドの利点については下記を参照
- [Swiftの強力な機能であるstaticメソッド制約の紹介と、Kotlin, TypeScript, Java, Scala, C++との比較](https://qiita.com/omochimetaru/items/621f1ef62b9798ee5ff5)

・**オーバーロード**  

異なる引数や戻り値を取る同名のメソッドを複数用意して、引数に渡される型や戻り値の代入先に応じて実行するメソッドを切り替える手法。  



