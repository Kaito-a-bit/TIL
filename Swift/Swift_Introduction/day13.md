第7章　エクステンション
---

既に存在している型に、プロパティやメソッド、イニシャライザなどの**型を構成する要素**を追加することができる。  

・**コンピューテッドプロパティの追加**  
エクスエンションでは、ストアドプロパティを追加することはできないが、コンピューテッドプロパティを追加することはできる。  
アプリケーション内で、既存の型に対して頻繁に行われる処理を型自身に追加することができる。  

```Swift
extension String {
    var enclosedString: String {
        return "【\(self)】"
    }
}

let title = "重要".enclosedString + "今日は休み"
print(title) //【重要】今日は休み
```  

・**イニシャライザの追加**  
```
enum WebAPIError: Error {
    case connectionError(Error)
    case fatalError
    
    var title: String {
        switch self {
        case .connecionError:
            return "通信エラー"
        case .fatalError:
            return "致命的エラー"
            
        }
    }
    
    var message: String {
        switch self {
        case .connectionError(let underlyingError):
            return underlyingError.localizedDescription + "再試行してください"
        case .fatalError:
            return "サポート窓口に連絡してください"
        }
    }
}

extension UIAlertController {
//ここでイニシャライザを追加することでUIAlertControllerを初期化する際の引数（本来は3つ）をまとめて指定することができている。
    convenience init(webAPIError: WebAPIError) {
        self.init(title: webAPIError.title, message: webAPIError.message, preferredStyle: .alert)
    }
}

let error = WebAPIError.fatalError
let alertController = UIAlertController(webAPIError: error)
```

