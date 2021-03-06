# 控制流程

- [For-in 循環](#for)
- [While 循環](#while_loop)
- [條件語句](#condition)
- [可選綁定](#optional_binding)
- [Switch](#switch)
- [控制轉移語句](#control_transfer_statement)
- [提前退出](#guard)
- [斷言](#assertion)
- [檢測 API 可用性](#api)

Swift 提供了可以**循環執行任務**的`for-in`和`while`迴圈，以及**根據條件選擇執行不同程式碼分支**的`if`和`switch`語句，還有控制流程**跳轉到其他程式碼**的`break`和`continue`語句。

<a name="for"></a>
### For-in 循環

使用`for-in`遍歷一個集合內的所有元素，像是一個數字區間、陣列、字典中的值或是字串內的字元，例子如下：

```swift
// 一個一到三的閉區間
for index in 1...3 {
    print(index)
}
// 會依序印出：
// 1
// 2
// 3

```

上述程式內的`index`不用做宣告的動作，在每次遍歷開始時會被自動指派值，預設是一個常數。

另外如果只是要純粹的循環，不需要用到區間內的每一個值，可以用下底線`_`來代替。

```swift
let base = 2
var total = 1
for _ in 1...3 {
    total *= base
}

// 因為循環了三次 所以乘了三次 印出：8
print(total)

```

使用`for-in`遍歷一個陣列(`array`)或是字典(`dictionary`)。遍歷字典時，會使用元組(`tuple`)來分別表示鍵與值，例子如下：

```swift
let arr = ["Apple", "Book", "Cat"]
for n in arr {
    print(n)
}
// 依序印出：
// Apple
// Book
// Cat

let dict = ["Apple":12, "Book":3, "Cat":5]
for (key, values) in dict {
    print("\(key) : \(values)")
}
// 印出：(因為字典沒有順序 所以不一定是這樣的順序)
// Apple : 12
// Book : 3
// Cat : 5

```

<a name="while_loop"></a>
### While 循環

Swift 提供兩種`while`循環方式：`while`及`repeat-while`，兩者都是循環地執行程式直到條件表達式返回`false`，差別在於，後者一開始在檢查條件表達式之前，一定會先執行一次內部程式。

#### While

`while` 循環格式如下：

```swift
while 條件表達式 {
    每次循環執行的程式
}

```

`while` 會循環地執行程式直到條件表達式返回`false`，例子如下：

```swift
var n = 2
while n < 20 {
    n = n * 2
}

// 印出：32
print(n)

```

#### Repeat-while

`repeat-while` 循環格式如下：

```swift
repeat {
    每次循環執行的程式
} while 條件表達式

```

`repeat-while` 會先執行一次程式，再檢查條件表達式，接著循環地執行程式直到條件表達式返回`false`。

```swift
var m = 512
repeat {
    m = m * 2
} while m < 100

// 印出：1024
print(m)
// 因為不論如何 都會先執行一次程式 所以 m 會先乘一次 2 為 1024
// 接著檢查條件表達式 會返回 false 即結束這個循環

```

<a name="condition"></a>
### 條件語句

條件語句為**根據不同特定條件執行不同的程式**。Swift 提供兩種條件語句：`if`與`switch`，如果需要判斷的條件較單純或可能的情況較少時，可以使用`if`，反之使用`switch`。

#### If

最簡單的形式為只有一個條件表達式，而只有當這個條件表達式返回`true`，才執行其內的程式，例子如下：

```swift
let someNumber = 2
if someNumber == 2 {
    print("It is 2 .")
}

```

或是當條件表達式返回`false`時，需要執行另一段程式，則使用`else`，如下：

```swift
let number = 10
if number > 20 {
    print ("Number is larger than 20 .")
} else {
    print ("Number is smaller than 20 or equal to 20 .")
}
// 印出：Number is smaller than 20 or equal to 20 .

```

又或是有多個條件需要判斷，可以將`else`跟`if`連在一起，最後一個`else`會在所有條件都不成立(返回`false`)時被執行，如下：

```swift
let number2 = 100
if number2 < 20 {
    print ("數字小於 20")
} else if number2 < 200 {
    print ("數字不小於 20，但小於 200")
} else if number2 < 1000 {
    print ("數字不小於 200，但小於 1000")
} else {
    print ("數字不小於 1000")
}
// 印出：數字不小於 20，但小於 200

```

上述程式中最後一個`else`不是一定要有，也可以省略，但就可能會沒有返回`true`的條件表達式，例子如下：

```swift
let number3 = 10
if number3 > 50 {
    print("number3 > 50")
} else if number3 > 200 {
    print("number3 > 200")
}
// 這時候不會有東西被印出來

```

<a name="optional_binding"></a>
### 可選綁定

使用**可選綁定**(`optional binding`)來判斷可選型別是否有值，如果有值的話就指派給一個臨時常數或臨時變數，並執行其內部的程式，這個臨時常數或變數只能在其內部使用。`if`跟`while`語句都可以使用可選綁定。格式如下：

```swift
if let 臨時常數 = 可選型別 {
    執行的程式
} else {
    可選型別沒有值 也就是 nil 時 執行的程式
}

```

以下是一個例子：

```swift
// 字串內容是純整數 所以經過轉換後會是一個整數
let str = "123"
if let number = Int(str) {
    print("字串 \"\(str)\" 轉換成一個整數 \(number)")
} else {
    print("字串 \"\(str)\" 不是一個整數")
}

// 如果字串內容不是整數 轉換後會返回 nil 
let str2 = "It is a string ."
if let number = Int(str2) {
    print("字串 \"\(str2)\" 轉換成一個整數 \(number)")
} else {
    print("字串 \"\(str2)\" 不是一個整數")
}

```

<a name="switch"></a>
### Switch

`switch`會**將一個值與多個情況作比對**，根據第一個比對成功的情況，會執行相對應的程式。所有`case`必須涵蓋全部可能的情況，如果有未涵蓋的部份，最後需要補上`default`。最簡單的格式如下：

```swift
switch 值 {
case 比對情況1:
    相對應情況1 執行的程式
case 比對情況2, 比對情況3: // 多個情況可以用逗號 , 隔開
    相對應情況2或情況3 執行的程式
default:
    以上情況比對都不成功時 執行的程式
}

```

每個`case`中，都一定要有相對應執行的程式，如果沒有的話會報錯誤，例子如下：

```swift
let number4 = 2
switch number4 {
case 1:
case 2:
    print("It is 2 .")
case 3:
default:
    print("沒有比對到")
}
// case 1 以及 case 3 內部都沒有執行的程式 所以這邊會報錯誤

```

與其他程式語言不一樣的是，有些程式語言的`switch`需要在每個`case`內的程式最後一行加上`break`來結束，否則會繼續執行底下其他`case`中的程式。

Swift 在遇到第一個情況`case`比對成功後，即會結束`switch`這部份的動作，繼續執行`}`之後的程式。(除非使用`fallthrough`，稍後即會提到。)

#### 區間匹配

`case`中比對的情況也可以是一個區間：

```swift
let number5 = 120
var str3: String
switch number5 {
case 0...10:
    str3 = "幾"
case 11...100:
    str3 = "很多"
case 101...1000:
    str3 = "非常多"
default:
    str3 = "超級多"
}

// 因為 120 在 101...1000 這個區間內
// 印出：我有非常多顆蘋果
print("我有\(str3)顆蘋果")

```

#### 元組

`switch`可以使用元組(`tuple`)來一次比對多個值，元組內可以是值也可以是區間，如果要忽略比對其中一項的話，可以填入下底線`_`：

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("(0, 0) 在原點")
case (_, 0):
    print("(\(somePoint.0), 0) 在 X 軸上")
case (0, _):
    print("(0, \(somePoint.1)) 在 Y 軸上")
case (-2...2, -2...2):
    print("(\(somePoint.0), \(somePoint.1)) 在方形內")
default:
    print("(\(somePoint.0), \(somePoint.1)) 在方形外")
}

// 印出：(1, 1) 在方形內

```

#### 值綁定

`case`可以將比對的值綁定(`value binding`)到一個臨時的常數或變數，以便在其內的程式中使用：

```swift
let onePoint = (2, 0)
switch onePoint {
case (let x, 0):
    print("在 X 軸上, x 的值為 \(x)")
case (0, let y):
    print("在 Y 軸上, y 的值為 \(y)")
case let (x, y):
    print("(\(x), \(y)) 不在 X 軸也不在 Y 軸上")
}

// 印出：在 X 軸上, x 的值為 2

```

另外可以使用`where`來判斷額外的條件：

```swift
let number6 = 20
switch number6 {
case 1...100 where number6 == 50:
    print("在 1...100 區間內 且值為 50")
case 1...100 where number6 == 20:
    print("在 1...100 區間內 且值為 20")
default:
    print("沒有比對到")
}

```

<a name="control_transfer_statement"></a>
### 控制轉移語句

控制轉移語句(`control transfer statement`)可以改變程式的執行順序，或是跳轉執行程式。

#### Continue

`continue`表示在循環流程中，立即**停止本次循環，重新開始此流程的下個循環**。以下是個例子：

```swift
for n in 1...10 {
    // n 除以 2 的餘數為零時(即 n 為偶數時) 
    if n % 2 == 0 {
        // 停止本次循環 重新開始此流程的下個循環
        continue
    }
    print(n)
}
// 因為當 n 為偶數時 都會走到 continue 即立即停止本次循環
// 所以會被依序印出的只有 1, 3, 5, 7, 9

```

#### Break

`break`會立即**停止這個循環流程**，接著繼續執行之後的程式。如果要提早結束`switch`時也可以使用。以下是個例子：

```swift
for n in 1...10 {
    // n 大於 2 時
    if n > 2 {
        // 立即停止這個循環流程
        break
    }
    print(n)
}
// 當迴圈進行到第三圈時 因為 n 為 3 已經大於 2 了
// 即會進到 break 同時立即停止這個循環流程
// 所以這邊只會印出 1, 2

```

#### Fallthrough

Swift 的`switch`中，只要比對到一個`case`即會執行其內的程式，並結束這整個`switch`的動作，如果在特殊情況下需要執行緊接著的下一個`case`內的程式，就要用到`fallthrough`。

```swift
let number7 = 5
var str4 = ""
switch number7 {
case 2,3,5,7,11,13,17,19:
    str4 += "It is a prime number. "
    fallthrough
case 100,200:
    str4 += "Fallthrough once. "
    fallthrough
default:
    str4 += "Fallthrough twice."
}

// 印出：
// It is a prime number. Fallthrough once. Fallthrough twice.
print(str4)
// 雖然只比對到第一個 case 但兩個 case 都有使用 fallthrough
// 所以最後 str4 是將所有字串相加

```

##### Hint

- 加上`fallthrough`後進入到的下一個`case`，不會對其條件做比對，而是直接執行其內的程式。


#### 帶標籤的語句

有時會需要較複雜的混用多個`switch`、`for`或是`while`，當需要對其中一個循環流程使用`continue`或`break`來跳轉或停止時，可以額外地對`continue`或`break`指名是屬於哪個循環流程。格式如下：

```swift
標籤名稱: while 條件 {
    循環執行的程式
}

```

以下是個例子：

```swift
var number8 = 1
gameLoop: while number8 < 10 {
    switch number8 {
    case 1...4:
        number8 += 1
    case 5:
        number8 *= 10
        // break 標註為 gameLoop 的 while 迴圈
        break gameLoop
    default:
        number8 += 1
    }
}
// 印出：50
print(number8)
// 在 1...4 區間內時 會將 number8 加 1
// 直到 n==5 時 會乘以 10 並結束 while 循環
// 因為有將 while 加上名為 gameLoop 的標籤
// 所以可以很明白的了解 case 5 中的 break 是要結束 while
// 因此這個 while 其實只循環 5 次即結束

```

<a name="guard"></a>
### 提前退出

有點類似`if`的用法，`guard`同樣會有一個條件表達式且會返回一個布林值，不同的地方在於，`guard`後面一定要接一個`else`，如果條件表達式返回`false`時，會執行`{}`內的程式。

```swift
guard 條件表達式 else {
    // 條件表達式返回 false 時 執行的程式
    // 可以配合 continue, break 或 return 來控制轉移流程
}

// 條件表達式返回 true 時 則繼續執行接下來的程式

```

以下是一個例子：

```swift
// 建立一個名叫 post() 的函式
// 需要傳入一個型別為 [String: String] 的字典
func post(article: [String: String]) {
    // 首先取得傳入字典中 鍵為 title 的值 並指派給一個常數
    guard let insideTitle = article["title"] else {
        // 如果沒有鍵為 title 的值 這裡面的程式就會被執行
        // 函式中的 return 表示會直接結束這個函式
        return
    }
    
    // 上面的 insideTitle 如果有正確的被指派值 則會繼續進行到這裡
    print("標題是 \(insideTitle) ，")
    
    // 接著取得傳入字典中 鍵為 content 的值 並指派給一個常數
    guard let insideContent = article["content"] else {
        // 如果沒有鍵為 content 的值 這裡面的程式就會被執行
        print("但是沒有內容。")
        return
    }
    
    // 上面的 insideContent 如果有正確的被指派值 則會繼續進行到這裡
    print("內容為 \(insideContent)。")
}

post(["title": "Article_1"])
// 印出：標題是 Article_1 ，
// 印出：但是沒有內容。

post(["title":"Article_2","content":"Article_2_full_content"])
// 印出：標題是 Article_2 ，
// 印出：內容為 Article_2_full_content。

```

##### Hint

- `guard`條件表達式中，使用**可選綁定**而被指派的常數或變數，可以在函式`{}`範圍裡接下來的程式中使用。

雖然`guard`用法與`if`類似，但使用`guard`可以一次專注於一種條件的情況，提高程式的可靠性，也可以讓函式內容更清晰好讀。

後面章節會正式介紹[函式](../ch1/functions.md)。

<a name="assertion"></a>
### 斷言

斷言(`assertion`)會在執行時判斷一個邏輯條件是否為`true`，而如果為`false`的話，程式則會被中止，使用函式`assert()`，格式如下：

```swift
assert(邏輯條件, 返回 false 時會顯示的訊息)

// 或是省略成只有判斷邏輯
assert(邏輯條件)

```

底下是一個例子：

```swift
var age = -25
assert(age > 0, "年齡必須大於零")

```

斷言通常使用在測試階段的程式，你可以使用斷言來保證在執行其他程式碼之前，某些重要的條件已經被滿足。可能適用的情況如下：

- 數字可能過大或過小。
- 需要給函式傳入一個值，但是非法的值可能導致函式不能正常執行。
- 一個可選值為`nil`，但後面需要這個值為一個非`nil`值。

<a name="api"></a>
### 檢測 API 可用性

Swift 可以讓你檢查 API 的預設支持，可以防止不小心使用到了對於當前部屬目標不可用的 API。以下是使用方式：

```swift
if #available(平台名稱 版本號, ..., *) {
    // 在某個平台或版本下使用特別的 API
} else {
    // 而其他的平台或版本則使用其他的 API
}

```

平台名稱可以是`iOS`、`OSX`或`watchOS`。版本號可以是大版本號像是`iOS 9`，或是較小的版本像是`iOS 8.3`或`OSX 10.10.3`，以下是一個例子：

```swift
if #available(iOS 9, OSX 10.10.3, *) {
    // 在 iOS 使用 iOS 9 的 API
    // 在 OSX 使用 OSX 10.10.3 的 API
} else {
    // 使用先前版本的 iOS 和 OSX 的 API
}

```


### 範例

本節範例程式碼放在 [ch1/control_flow.playground](https://github.com/itisjoe/swiftgo_files/tree/master/ch1/control_flow.playground)

