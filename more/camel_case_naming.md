# 駝峰式命名法

Swift 在命名常數、變數、函式、類別或其他自定義型別時，通常習慣使用**駝峰式命名法**。

這種命名方式是一種習慣，沒有絕對與強制，為的是增加識別與可讀性。

當自定義名稱是由二個或多個單字連結在一起，而構成的唯一識別字時，單字之間不以空格、連結號(`-`)或底線(`_`)隔開，有兩種格式：

##### 小駝峰式命名法(`lower camel case`)

第一個單字以小寫字母開始，第二個及之後的單字的首字母則使用大寫，像是：`firstName`、`somePerson`。

Swift 中通常命名常數、變數、函式、屬性、方法及下標時，會使用小駝峰式命名法。

##### 大駝峰式命名法(`upper camel case`)

每個單字的首字母都使用大寫字母，像是`LastName`、`SomeClass`。

Swift 中通常命名列舉、結構、類別、擴展、協定及其他自定義型別時，會使用大駝峰式命名法。
