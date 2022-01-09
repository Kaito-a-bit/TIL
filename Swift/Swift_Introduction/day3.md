第3章 基本的な型（2）
---
### 型のキャスト
・**アップキャスト, ダウンキャスト**  
→アップキャスト  
階層関係がある型同士において、階層の下位となる具体的な型を上位の抽象的な型として扱う。  
　`as`演算子を用いる  
→ダウンキャスト  
階層関係のある型同士において階層の上位となる抽象的な型を下位の具体的な型として扱う。  

アップキャストとは異なり、コンパイルはできても失敗する可能性がある。その為、演算子は`as?`もしくは`as!`となる。  
`as?`演算子は失敗時には`nil`, 成功時には`Optional<Wrapped>型`を返す。   
強制ダウンキャスティング(`as!`)は失敗時にはエラー。

`as?`**はエラーの可能性がなく安全だが**`nil`**の可能性を考慮する必要がある。**  
`as!`**は簡潔だが、エラーを起こす可能性を孕んでいる為、なるべく避ける。**  

・**実践例にみるas?・as!の使い分け**  
よく見るのは`TableView`をカスタムクラスで実装したい場合。 

```
・as!

  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
      let cell = feedTableView.dequeueReusableCell(withIdentifier: "FeedArticleCell", for: indexPath) as! FeedArticleTableViewCell
      let article = articleArr[indexPath.row]
      cell.configure(from: article)
      return cell
  }
  
・as?

  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
      guard let cell = feedTableView.dequeueReusableCell(withIdentifier: "FeedArticleCell", for: indexPath) as? FeedArticleTableViewCell else {
        fatalError() //ここでエラー処理を行う。
      }
      let article = articleArr[indexPath.row]
      cell.configure(from: article)
      return cell
  }
```
参照: [is force cast really bad and should i avoid this?](https://stackoverflow.com/questions/36024543/is-force-cast-really-bad-and-should-always-avoid-it)  
→`map`を用いて確実にキャストしたいサブクラスに変更する方法が紹介されていた。確実にキャストしたいサブクラスにできていれば、強制キャスティングも良いのでは。的な。

・**型の判定**
`is`演算子を用いる  
```
  let a: Any = 1
  let isInt = a is Int //true
```

・**そもそもプロトコルとは**  
プロトコルとは「それに準拠する型が持つべき性質を定義したもの」。（後で扱う）
