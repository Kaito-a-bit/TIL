第4章　コレクションを表す型
---
### Dictionary型
・**辞書型の基本**  
キーと値のペアを持つコレクションであり、キーを元に値にアクセスする。**キーと値のペア同士に順序関係はない**点に注意。   
→つまり、辞書型のデータに順番に処理をしたいときには工夫する必要がある。  

・**キーと値にできる型**  
`Dictionary<Key, value>`型は正式には`Dictionary<Key: Hashable, value>`型である。  
つまり`Key`は`Hashable`プロトコルに準拠している必要がある。  
Keyがこれに準拠する必要があるのは、それによって生成されるハッシュ値がキーの一意性の保証や探索などに必須であるため。

・**KeyValuePairs**  
`KeyValuePairs`を使用すると、その要素の順番が保証される。厳密にいうと辞書型とはその性質が少し異なる。  
その特徴としては以下が挙げられる。    
- Keyが`Hashable`に準拠している必要がない  
- 同一のKeyで要素を追加できる  
- 要素の順番が保証される  

参照: [https://www.hackingwithswift.com/example-code/language/what-are-keyvaluepairs](https://www.hackingwithswift.com/example-code/language/what-are-keyvaluepairs)

・**値の取り出しと注意点**  
値の取り出しにはサブスクリプトを使用する  
```
  let dictionary = ["key": 1] //[String: Int]型
  let value = dictionary["key"]  /1（Int?型）
```
配列とは異なり、サブスクリプトで存在しない値にアクセスしようとした時には**エラーではなく`nil`が返ってくる。**   
その為辞書型で返却される値の型は**Optional**であることに注意。  

### Range型  
```
  ..<  末尾の値を含まない
  ...  末尾の値を含む
```

### シーケンスとコレクションを扱うためのプロトコル  
シーケンスとは、その要素に一方向から順次アクセス可能なデータ構造のことを言う。（ex: 配列）  
シーケンスを汎用的に扱うため`Sequence`プロコトルが用意されている。  
コレクションは、正確には「一方向からの順次アクセスと特定のインデックスの値への直接アクセスが可能」なデータ構造であり、シーケンスを包含する概念である。  
`Collection`プロトコルが用意されている。  

```
  forEach(_:)     要素に対して順次アクセス
  filter(_:)      要素を絞り込む
  map(_:)　　　　　　　　　    　要素を変換する
  flatMap(_:)    　　要素をシーケンスに変換して、それらを一つのシーケンスに連結する
  compactmap(_:)　　　　要素を、失敗する可能性のある処理を用いて変換する
  reduce(_:_:)    要素を一つの値にまとめる
```
```
  ・flatMap(_:)
  
    let a = [1, 4, 7]
    let b = a.flatMap({ value in [value in [value, value +1] })
    b //[1, 2, 4, 5, 7, 8]
    
    シーケンスを連結した上でフラットにしている。
  
  ・map(_:)を用いると…
  
    let a = [1, 4, 7]
    let b = a.map({ value in [value in [value, value +1] })
    b //[[1, 2], [4, 5], [7, 8]]
```

```
  ・compactMap(_:)
    let strings = ["abc", "123", "def", "456"]
    let integers = strings.compactMap({ value in Int(value) })
    integers //[]123, 456]
    
    map(_:)との相違点は、変換できない値を無視する点。  
    引数のクロージャの戻り値はOptional<Wrapped型>にすることで値を無視することができる。  
```


