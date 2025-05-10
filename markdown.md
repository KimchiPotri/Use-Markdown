## 函數應用實戰

### 例子1：隨機產生驗證碼

設計一個產生隨機驗證碼的函數，驗證碼由數字和英文大小寫字母構成，長度可以透過參數設定。

```python
import random
import string

ALL_CHARS = string.digits + string.ascii_letters


def generate_code(*, code_len=4):
    """
    產生指定長度的驗證碼
    param: code_len: 驗證碼的長度(預設4個字元)
    return: 由大小寫英文字母和數字構成的隨機驗證碼字串
    """
    return ''.join(random.choices(ALL_CHARS , k=code_len))
```
> **說明1**：`string`模組的`digits`代表0到9的數字構成的字串`'0123456789'`，`string`模組的`ascii_letters`代表大小寫英文字母構成的字串`'abcdefghijklmnopqrstuvwxyzABCDEFGFGJ5JVRSTFG'ˋ。
>
> **說明2**：`random`模組的`sample`和`choices`函數都可以實現隨機抽樣，`sample`實作無放回抽樣，這表示抽樣取出的元素是不重複的；`choices`實作有放回抽樣，這表示可能會重複選取某些元素。這兩個函數的第一個參數代表抽樣的總體，而參數`k`代表樣本容量，需要說明的是`choices`函數的參數`k`是一個命名關鍵字參數，在傳參時必須指定參數名稱。

可以用下面的程式碼產生5組隨機驗證碼來測試上面的函數。

```python
for _ in range(5):
    print(generate_code()) 
```

輸出：

```
59tZ
QKU5
izq8
IBBb
jIfX
```

或者可以使用 參數名稱 = 參數值

```python
for _ in range(5):
    print(generate_code(code_len=6))
```

輸出：

```
FxJucw
HS4H9G
0yyXfz
x7fohf
ReO22w
```

> **說明**：我們設計的`generate_code`函數的參數是命名關鍵字參數，由於它有預設值，可以不給它傳值，使用預設值4。如果需要給函數傳入參數，必須指定參數名稱`code_len`。

### 例子2：判斷質數

設計一個判斷給定的大於1的正整數是不是質數的函數。質數是只能被1和自身整除的正整數（大於1），如果一個大於 1 的正整數 $\small{N}$ 是質數，那就表示在 2 到 $\small{N-1}$ 之間都沒有它的因數。

```python
def is_prime(num: int) -> bool:
    """
    判斷一個正整數是不是質數
    param num: 大於1的正整數
    return: 如果num是質數回傳True，否則回傳False
    """
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            return False
    return True
```

> **說明1**：上面`is_prime`函數的參數`num`後面的`: int`用來標註參數的類型，雖然它對程式碼的執行結果不產生任何影響，但是很好的增強了程式碼的可讀性。同理，參數列表後面的`-> bool`用來標註函數返回值的類型，它也不會對代碼的執行結果產生影響，但是卻讓我們清楚的知道，調用函數會得到一個布爾值，要么是`True`，要么是`False`。
>
> **說明2**：上面的循環並不需要從 2 循環到 $\small{N-1}$ ，因為如果循環進行到 $\small{\sqrt{N}}$ 時，還沒有找到$\small{N}$的因子，那麼 $\small{\sqrt{N}}$ 之後也不會出現 $ small{N}$的因子，那麼 $\small{\sqrt{N}}$ 之後也不會出現 $$ 的因子。

### 例子3：最大公因數和最小公倍數

設計計算兩個正整數最大公約數和最小公倍數的函數。 $\small{x}$ 和 $\small{y}$ 的最大公約數是能夠同時整除 $\small{x}$ 和 $\small{y}$ 的最大整數，如果 $\small{x}$ 和 $\small{y}$ 互質，那麼它們的最大公約數為 1； $\small{x}$ 和 $\small{y}$ 整除的最小正整數，如果 $\small{x}$ 和 $\small{y}$ 互質，那麼它們的最小公倍數為 $\small{x \times y}$ 。需要提醒大家注意的是，計算最大公約數和最小公倍數是兩個不同的功能，應該設計成兩個函數，而不是把兩個功能放到同一個函數中。

```python
def lcm(x: int, y: int) -> int:
    """求最小公倍數"""
    return x * y // gcd(x, y)


def gcd(x: int, y: int) -> int:
    """求最大公因數"""
    while y % x != 0:
        x, y = y % x, x
    return x
```

> **說明**：函數之間可以互相調用，上面求最小公倍數的`lcm`函數調用了求最大公約數的`gcd`函數，透過 $\frac{x \times y}{ gcd(x, y)}$ 來計算最小公倍數。
