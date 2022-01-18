第6章 関数とクロージャ
---

### 関数
・**外部引数名と内部引数名**  
引数名は呼び出し時に使用する外部引数名と、関数内で使用される内部引数名の二つを持つことができる。  
両者を分けるには、`外部引数名 内部引数名: 型`という形式で引数を定義する。  

```Swift
    func configure(from model: ArticleModel) {
        articleTitle.text = model.title
        articleDate.text = "投稿日:\(model.createdAt.convertToJapaneseFormat)"
        userID.text = "@\(model.user.id)"
        self.cachingPics(url: model.user.profileImageUrl)
    }
```

・**外部引数名の省略**  
省略したい場合は外部引数名に`_`を使用する。  
```Swift
    func sum(_ int1: Int, _ int2: Int) -> Int {
        return int1 + int2
    }

    let result = sum(1, 3)  //内部引数は関数内で使用する  
```

・**デフォルト引数の使用ケース** 
デフォルト引数は`引数名: 型 = 値`で指定できる。  
**全ての引数の指定が必須という訳ではない場合に使用する**  
```Swift
    func search(byQuery query: String,
            sortkey: String = "id",
            ascending: Bool = false) -> [Int] {
    return [1, 2, 3]
    }

    search(byQuery: "query") //[1, 2, 3]
```

・**インアウト引数の使用ケース**  
関数内での引数への再代入を関数外へ反映させる為に使用する。  
インアウト引数の先頭に`&`をつける。　　
```Swift
    func greet(user: inout String) {
        if user.isEmpty {
            user = "Anonymous"
        }
        print("hello, \(user)")
    }
    var user: String = ""
    greet(user: &user) // "Hello, Anonymous"
```
