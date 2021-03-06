# 下標

- [下標語法](#subscript)
- [下標用法](#usage)

下標(`subscript`)是一個可以快速存取及設置值的方式，單看中文字面上可能不太清楚什麼意思，其實在前面章節介紹[陣列](../ch1/collection_types.md#array)(`array`)及[字典](../ch1/collection_types.md#dictionary)(`dictionary`)時已經有接觸過，在陣列或字典名稱後面緊接著中括號`[]`，括號內填入陣列的索引值(`index`)或是字典的鍵(`key`)，即可存取或設置值，以下是個例子：

```swift
// 宣告一個 [Int] 型別的陣列
var arr = [1,2,3,4,5,6,7]

// 印出其內第三個元素(請記得 陣列的索引值是從 0 開始算起)
print(arr[2])

// 修改第四個元素為 12
arr[3] = 12


// 宣告一個 [String:String] 型別的字典
var dict = ["name":"Kevin","city":"Taipei"]

// 印出鍵為 name 的值
print(dict["name"])

// 修改鍵為 city 的值為 New York
dict["city"] = "New York"

```

<a name="subscript"></a>
### 下標語法

下標也可以定義在類別(`class`)、結構(`structure`)及列舉(`enumeration`)中，在其內的定義方式如下：

```swift
subscript(索引值: 索引值型別) -> 返回值型別 {
    get {
        // 存取值的程式操作
        // 必須返回一個前面定義的型別的值
    }
    set(新設置值的名稱) {
        // 設置值的程式操作
    }
}

```

與前面章節介紹的[計算型屬性](../ch2/properties.md#computed_property)相似，可以定義為讀寫(`getter`及`setter`)，也可以定義為唯讀(`getter`)。`setter`傳入的設置值名稱也可以省略，省略時會有一個內建預設的名稱`newValue`。這兩種方式定義如下：

```swift
// 當下標為唯讀時 可以將 get 關鍵字及大括號 {} 省略掉 如下
subscript(索引值: 索引值型別) -> 返回值型別 {
    // 存取值的程式操作
    // 必須返回一個前面定義的型別的值
}


// 省略 setter 傳入的設置值名稱 會有一個內建預設名稱 newValue
subscript(索引值: 索引值型別) -> 返回值型別 {
    get {
    }
    set{
        // 設置值的程式操作
        // 可使用 newValue 來操作
    }
}

```

<a name="usage"></a>
### 下標用法

以下為在一個類別中定義下標的例子：

```swift
// 定義一個簡單數學算式功能的類別
class SimpleMath {
    // 一個數字屬性預設值
    var num = 500
    
    // 定義一個下標 為乘法
    subscript(times: String) -> Int {
        get {
            // 其內可以使用這個索引值
            print(times)

            // 會返回 數字屬性乘以 2 的數值
            return num * 2
        }
        set {
            // 將數字屬性乘以新的倍數
            num *= newValue
        }
    }

    // 定義另一個下標 為除法
    subscript(divided: Int) -> Int {
        return num / divided
    }
}

// 宣告一個類別 SimpleMath 的常數
let oneMath = SimpleMath()

// 印出：1000
print(oneMath["simple"])

// 傳入值為 3, 會將數字屬性乘以 3
oneMath["star"] = 3

// 這個下標例子中的字串索引值沒有被使用到
// 其實是可以依照傳入的索引值 來做不同的需求及返回值

// 印出：1500
print(oneMath.num)

// 使用到另一個下標 索引值型別為 Int
// 印出：15
print(oneMath[100])

```

下標可以定義多個索引值，可以是任意型別的參數或可變數量參數，返回值也可以是任意型別，但不能使用輸入輸出參數(`inout`)，也不能給參數設置預設值。

如上述程式，類別或結構可以定義多個下標，使用下標時會依據索引值數量及型別，自動推斷使用合適的下標。


### 範例

本節範例程式碼放在 [ch2/subscripts.playground](https://github.com/itisjoe/swiftgo_files/tree/master/ch2/subscripts.playground)

