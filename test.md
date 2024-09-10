# Day02-Math.abs()

正式開始第一天就來暖身一下吧！~~伏地挺身 30 下預備~~，今天要介紹的方法是`Math.abs()`，`abs`是從絕對值的英文*absolute value*縮寫而來的，讓我們來看看他可以做什麼吧！

絕對值的概念相信大家都很熟悉～回想一下剛上國中的數學，大家記得一年級的第一章在說什麼嗎？沒錯！就是「數與數線」，`x`的絕對值可以理解成`x`到原點的「距離」，因為是距離，所以一定不可能是負數，結果一定會是非負數！

講完絕對值就來看看這個方法怎麼使用吧：

## 語法

```javascript
Math.abs(x);
```

### 參數

放入一個數字型別

### 回傳值

它會回傳傳入之引數的`x`的絕對值，如果`x`為負數或`-0`，將會回傳相反數`-x`，否則他將回傳`x`本身，因此這個方法永遠會回傳`0`或是正數，也就是非負數。

### 強制參數

`Math.abs()`方法將觸發強制轉型成數值，不能強制轉成數值得就轉成`NaN`讓`Math.abs()`回傳`NaN`。

就這？讓我們來看看規範～

### 規範

![image](https://hackmd.io/_uploads/S1V-DB_nC.png)

這個函式將會回傳`x`的絕對值，結果會跟原本`x`的值一樣但會加上正號。

當呼叫函式時會執行役下步驟：

1. 令一個變數`n`並將`ToNumber(x)`賦值給它
2. 如果`n`是`NaN`那就回傳`NaN`
3. 如果`n`是浮點數`-0`，回傳浮點數`+0`
4. 如果`n`是負無限大的浮點數，回傳正無限大的浮點數
5. 如果`n`是小於浮點數`-0`，回傳`-n`
6. 如果都不是以上，回傳`n`

#### ToNumber(x)???

從第一步就卡住了，`ToNumber(x)`是啥？點進去看看：
![image](https://hackmd.io/_uploads/ryJJU8u2R.png)

1. 如果引數是數字，回傳引數本身。
2. 如果引數是`Symbol`或是`BigInt`就報錯。
3. 如果引數是`undefined`，回傳`NaN`。
4. 如果引數是`null`或`false`，回傳浮點數`+0`。
5. 如果引數是`true`，回傳`1`。
6. 如果引數是一個字串，回傳`StringToNumber(argument)`的結果。
7. 用`Assert`方法確認引數是一個「物件」則繼續執行，否則報錯
8. 會不會跑太遠傻眼，未完待續

簡單來說他是一個抽象操作，判別傳入的`x`是不是數字，如果是就回傳自己，如果不是會做什麼操作等等。

### 應用

絕對值的各種應用不外乎就是計算距離、判斷正數負數或零、限制誤差的範圍等等...

最後就針對「限制誤差範圍」這點來做個結尾，結束漫長的一天吧：

假設今天有很多新籃球準備賣出去，但他的重量必須落在 600g~650g 之間（625g±25g）才能夠上架，我們可以利用絕對值來過濾出落在目標區間的項目：

```javascript
const basketballWeights = [600, 624, 651, 599, 634, 645, 612];
const standardWeight = 625;
const allowedError = 25;

function getError(a, b) {
    return Math.abs(a - b);
}

const validWeights = basketballWeights.filter((basketballWeight) => {
    return getError(standardWeight, basketballWeight) <= allowedError;
});

console.log(validWeights); //[600, 624, 634, 645, 612]
```

定義`getError`來獲取誤差值，然後利用`array.prototype.filter`來過濾出誤差小於`25`的項目，這些籃球就可以開賣啦～

結束。明天見！

### 參考資料：

-   [MDN-Math.abs()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/abs)
-   [ECMAScript-Math.abs(x)](https://tc39.es/ecma262/multipage/numbers-and-dates.html#sec-math.abs)
