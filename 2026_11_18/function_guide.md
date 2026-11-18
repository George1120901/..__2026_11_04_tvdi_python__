# Code Documentation: `2026_11_18/function.ipynb`

> This guide provides a complete explanation of the Python function examples in [`function.ipynb`](./function.ipynb) in three languages: **English**, **繁體中文 (Traditional Chinese)**, and **日本語 (Japanese)**.

---

## 1. English Guide

### Overview
[`function.ipynb`](./function.ipynb) demonstrates how Python functions receive and process arguments. It walks step-by-step from basic positional and keyword arguments to default values, parameter restrictions (`/` and `*`), variable-length packing (`*args` and `**kwargs`), and real-world built-in functions (`print` and `sorted`).

---

### Topic 1: Parameters vs. Arguments (`greet`)
- **Parameter**: The placeholder variable name written inside parentheses when defining a function (`name` in `def greet(name):`).
- **Argument**: The actual value passed into the function when calling it (`"小明"` in `greet("小明")`).

```python
def greet(name):
    print(f"哈囉,{name}!")

greet("小明")
```

**Output:**
```text
哈囉,小明!
```

---

### Topic 2: Positional Arguments (`describe_pet`)
When calling a function without parameter names, Python matches each argument to parameters **by position from left to right**.
- `describe_pet("貓", "小橘")` assigns `"貓"` to `animal` and `"小橘"` to `name`.
- Swapping the order (`describe_pet("小橘", "貓")`) assigns `"小橘"` to `animal` and `"貓"` to `name`, producing an unintended sentence.
- Passing too few arguments (`describe_pet("貓")`) or too many (`describe_pet("貓", "小橘", 3)`) raises a `TypeError`.

```python
def describe_pet(animal, name):
    print(f"我養了一隻{animal}，牠叫做{name}。")

describe_pet("貓", "小橘")
describe_pet("小橘", "貓")
```

**Output:**
```text
我養了一隻貓，牠叫做小橘。
我養了一隻小橘，牠叫做貓。
```

---

### Topic 3: Keyword Arguments & Mixing Rules (`describe_pet`)
You can pass arguments explicitly using `parameter_name=value`.
- **Order independence**: `describe_pet(name="小橘", animal="貓")` produces the exact same result as `describe_pet(animal="貓", name="小橘")`.
- **Mixing rule**: When mixing positional and keyword arguments, **positional arguments must come before keyword arguments**. Writing `describe_pet(animal="狗", "旺財")` causes a `SyntaxError`.

```python
describe_pet("狗", name="旺財")
```

**Output:**
```text
我養了一隻狗，牠叫做旺財。
```

---

### Topic 4: Default Arguments (`order_drink`)
Parameters can have default values (e.g., `ice="正常冰"`, `sugar="半糖"`):
- `order_drink("紅茶")` uses both defaults.
- `order_drink("紅茶", "去冰")` overrides `ice` positionally.
- `order_drink("紅茶", sugar="無糖")` skips `ice` (keeping its default) and overrides `sugar` by keyword.
- `order_drink("綠茶", sugar="微糖", ice="少冰")` overrides both defaults by keyword in any order.

**Output:**
```text
點餐：紅茶（正常冰 / 半糖）
點餐：紅茶（去冰 / 半糖）
點餐：紅茶（正常冰 / 無糖）
點餐：綠茶（少冰 / 微糖）
```

---

### Topic 5: Special Separators `/` and `*` (`calc_bmi`, `send_email`, `register`)
1. **`/` (Positional-Only)**: Parameters to the **left** of `/` can only be passed by position, not by keyword name.
   - Example: `def calc_bmi(weight, height, /):` → `calc_bmi(65, 1.75)` outputs `BMI 為：21.2`.
2. **`*` (Keyword-Only)**: Parameters to the **right** of a standalone `*` must be passed using keyword names (`name=value`).
   - Example: `def send_email(to, *, subject, urgent=False):` → `send_email("student@example.com", subject="課堂通知", urgent=True)` outputs `寄給：student@example.com｜主旨：課堂通知｜急件：True`.
3. **Combining `/` and `*` (`register`)**:
   - `def register(id_no, /, name, *, role="student"):` divides parameters into three zones:
     - `id_no`: positional-only
     - `name`: positional or keyword
     - `role`: keyword-only (defaults to `"student"`)
   - `register("A01", "小明", role="leader")` outputs `編號：A01｜姓名：小明｜身分：leader`.

---

### Topic 6: Packing Arbitrary Arguments with `*args` and `**kwargs` (`sum_scores`, `build_profile`)
- **`*scores` (`*args`)**: Collects any number of positional arguments into a **`tuple`**.
  - `sum_scores(80, 90, 85)` receives `(80, 90, 85)` and returns `255`.
  - `sum_scores()` receives `()` and returns `0`.
- **`**info` (`**kwargs`)**: Collects any number of extra keyword arguments into a **`dict`**.
  - `build_profile("小華", city="台北", course="Python")` packs `{'city': '台北', 'course': 'Python'}` into `info`.

---

### Topic 7: Built-in Function `print`
Signature: `print(*objects, sep=' ', end='\n', file=None, flush=False)`
- `*objects` accepts any number of positional arguments.
- Because `sep` and `end` appear after `*objects`, they must be passed by keyword name:
  - `print('a', 'b', 1, 67, 89)` → `a b 1 67 89`
  - `print('a', 'b', 1, 67, 89, sep='-')` → `a-b-1-67-89`
  - `print('a', 'b', 1, 67, 89, end='讚啦!\n')` → `a b 1 67 89讚啦!`

---

### Topic 8: Built-in Function `sorted`
Signature in notebook: `sorted(iterable, *, key=None, reverse=False)` (note: in Python's standard signature `iterable` is also positional-only).
- `reverse=True` is passed as a keyword argument to sort in descending order:
  - `sorted([8, 92, 63, 75], reverse=True)` returns `[92, 75, 63, 8]`.

---

## 2. 繁體中文說明

### 程式總覽
[`function.ipynb`](./function.ipynb) 透過 8 個循序漸進的實作範例，示範 Python 函式的定義與各種呼叫方式，涵蓋參數與引數的差別、位置引數、引數名稱、預設值、特殊限制符號 `/` 與 `*`、不定數量引數 `*args` 與 `**kwargs`，以及內建函式 `print` 和 `sorted` 的實際應用。

---

### 主題 1：參數（Parameter）與引數（Argument）—— `greet`
- **參數（Parameter）**：定義函式時，括號中用來接資料的變數名稱（像表格上的欄位，例如 `def greet(name):` 中的 `name`）。
- **引數（Argument）**：呼叫函式時，實際傳進去的資料值（例如 `greet("小明")` 中的 `"小明"`）。

```python
# 定義函式：name 是參數（Parameter）
def greet(name):
    print(f"哈囉,{name}!")

# 呼叫函式："小明" 是引數（Argument）
greet("小明")
```

**執行結果：**
```text
哈囉,小明!
```

---

### 主題 2：引數位置（Positional Argument）—— `describe_pet`
直接把值放進括號時，Python 會**依照順序從左到右**一對一對應：
- `describe_pet("貓", "小橘")`：`"貓"` 給 `animal`，`"小橘"` 給 `name`。
- `describe_pet("小橘", "貓")`：順序對調後，印出來的句子語意就會變錯。
- 若少傳（`describe_pet("貓")`）或多傳（`describe_pet("貓", "小橘", 3)`），都會因為數量不符而產生 `TypeError`。

**執行結果：**
```text
我養了一隻貓，牠叫做小橘。
我養了一隻小橘，牠叫做貓。
```

---

### 主題 3：引數名稱（Keyword Argument）與混用規則 —— `describe_pet`
呼叫時明確寫出 `參數名稱=值`，好處是**不必死記順序**且程式碼更清楚：
- `describe_pet(animal="貓", name="小橘")` 與 `describe_pet(name="小橘", animal="貓",)` 輸出完全相同。
- **混用重要規則**：同時使用位置引數與引數名稱時，**位置引數一定要寫在前面**。
  - 正確：`describe_pet("狗", name="旺財")` → `我養了一隻狗，牠叫做旺財。`
  - 錯誤：`describe_pet(animal="狗", "旺財")` → 位置引數放在引數名稱後面，會直接觸發語法錯誤（`SyntaxError`）。

---

### 主題 4：搭配預設值（Default Arguments）—— `order_drink`
```python
# ice 與 sugar 設有預設值，呼叫時可省略或單獨修改
def order_drink(drink, ice="正常冰", sugar="半糖"):
    print(f"點餐：{drink}（{ice} / {sugar}）")
```

- `order_drink("紅茶")`：全部套用預設值 → `點餐：紅茶（正常冰 / 半糖）`
- `order_drink("紅茶", "去冰")`：用位置改掉第 2 個參數 `ice` → `點餐：紅茶（去冰 / 半糖）`
- `order_drink("紅茶", sugar="無糖")`：跳過 `ice`，直接用引數名稱改 `sugar` → `點餐：紅茶（正常冰 / 無糖）`
- `order_drink("綠茶", sugar="微糖", ice="少冰")`：用引數名稱自由順序調整 → `點餐：綠茶（少冰 / 微糖）`

---

### 主題 5：特殊符號 `/` 與 `*` —— 限制呼叫方式（`calc_bmi`、`send_email`、`register`）
1. **`/`（僅限位置引數 Positional-Only）**：寫在 `/` **左邊**的參數，只能依位置傳入，不能寫引數名稱。
   - 範例 `calc_bmi(weight, height, /)`：呼叫 `calc_bmi(65, 1.75)` → 輸出 `BMI 為：21.2`。
2. **`*`（僅限關鍵字引數 Keyword-Only）**：寫在單獨一個 `*` **右邊**的參數，必須寫出引數名稱。
   - 範例 `send_email(to, *, subject, urgent=False)`：呼叫 `send_email("student@example.com", subject="課堂通知", urgent=True)` → 輸出 `寄給：student@example.com｜主旨：課堂通知｜急件：True`。
3. **`/` 與 `*` 同時使用（`register`）**：
   - `def register(id_no, /, name, *, role="student"):`
   - `id_no`（`/` 左邊）：僅限位置；`name`（`/` 與 `*` 中間）：位置或名稱皆可；`role`（`*` 右邊）：僅限名稱。
   - 呼叫 `register("A01", "小明", role="leader")` → 輸出 `編號：A01｜姓名：小明｜身分：leader`。

---

### 主題 6：`*args` 與 `**kwargs` —— 打包任意數量引數（`sum_scores`、`build_profile`）
- **`*scores`（一個星號）**：把傳入的 0 個或多個**位置引數**打包成一個 **`tuple`（元組）**。
  - `sum_scores(80, 90, 85)` → 收到 `(80, 90, 85) <class 'tuple'>`，回傳 `255`。
  - `sum_scores(80, 90)` → 收到 `(80, 90) <class 'tuple'>`，回傳 `170`。
  - `sum_scores()` → 收到 `() <class 'tuple'>`，回傳 `0`。
- **`**info`（兩個星號）**：把額外傳入的**引數名稱（`key=value`）**打包成一個 **`dict`（字典）**。
  - `build_profile("小華", city="台北", course="Python")` → `name` 為 `"小華"`，`info` 為 `{'city': '台北', 'course': 'Python'} <class 'dict'>`。

---

### 主題 7：內建函式實戰 —— `print`
函式定義：`print(*objects, sep=' ', end='\n', file=None, flush=False)`
- `*objects` 讓 `print()` 可以一次接收任意多個值。
- `sep` 和 `end` 在 `*objects` 後面，因此修改時必須寫引數名稱：
  - `print('a', 'b', 1, 67, 89)` → `a b 1 67 89`（預設用空白隔開、結尾換行）
  - `print('a', 'b', 1, 67, 89, sep='-')` → `a-b-1-67-89`（改用 `-` 連接）
  - `print('a', 'b', 1, 67, 89, end='讚啦!\n')` → `a b 1 67 89讚啦!`（改變結尾字串）

---

### 主題 8：內建函式實戰 —— `sorted`
Notebook 中標示：`sorted(iterable, *, key=None, reverse=False)`（標準 Python 中 `iterable` 也是僅限位置引數）。
- 必須使用引數名稱 `reverse=True` 才能改成由大到小排序：
  - `sorted([8, 92, 63, 75], reverse=True)` → 回傳 `[92, 75, 63, 8]`。

---

## 3. 日本語解説

### 概要
[`function.ipynb`](./function.ipynb) は、Python における関数の定義と呼び出し方を段階的に学ぶためのノートブックです。仮引数と実引数の違い、位置引数、キーワード引数、デフォルト引数、特殊記号 `/` と `*` による制限、可変長引数 `*args` と `**kwargs`、さらに組み込み関数 `print` と `sorted` の実例を扱っています。

---

### トピック 1：仮引数（Parameter）と実引数（Argument）—— `greet`
- **仮引数（Parameter）**：関数を定義するときに `def greet(name):` の括弧内に書く変数名です。
- **実引数（Argument）**：関数を呼び出すときに `greet("小明")` のように実際に渡す値です。

```python
def greet(name):
    print(f"哈囉,{name}!")

greet("小明")
```

**実行結果：**
```text
哈囉,小明!
```

---

### トピック 2：位置引数（Positional Argument）—— `describe_pet`
引数名を指定せずに値を渡すと、**左から順番に 1 対 1 で対応**します。
- `describe_pet("貓", "小橘")` では `animal="貓"`、`name="小橘"` になります。
- 順番を逆にした `describe_pet("小橘", "貓")` では意味が逆転してしまいます。
- 引数の数が足りない場合（`describe_pet("貓")`）や多すぎる場合（`describe_pet("貓", "小橘", 3)`）は `TypeError` が発生します。

**実行結果：**
```text
我養了一隻貓，牠叫做小橘。
我養了一隻小橘，牠叫做貓。
```

---

### トピック 3：キーワード引数（Keyword Argument）と混在のルール —— `describe_pet`
`パラメータ名=値` の形式で渡す方法をキーワード引数と呼びます。
- **順番を問わない**：`describe_pet(animal="貓", name="小橘")` と `describe_pet(name="小橘", animal="貓",)` は同じ結果になります。
- **混在時のルール**：位置引数とキーワード引数を同時に使う場合、**必ず位置引数を先に書く**必要があります。
  - 正しい例：`describe_pet("狗", name="旺財")` → `我養了一隻狗，牠叫做旺財。`
  - 誤った例：`describe_pet(animal="狗", "旺財")` → キーワード引数の後ろに位置引数を置いているため `SyntaxError` になります。

---

### トピック 4：デフォルト引数（Default Arguments）—— `order_drink`
`def order_drink(drink, ice="正常冰", sugar="半糖"):` のように既定値を設定すると、変更したい項目だけを指定できます。
- `order_drink("紅茶")` → `點餐：紅茶（正常冰 / 半糖）`
- `order_drink("紅茶", "去冰")` → `點餐：紅茶（去冰 / 半糖）`
- `order_drink("紅茶", sugar="無糖")` → `ice` を飛ばして `sugar` のみ変更：`點餐：紅茶（正常冰 / 無糖）`
- `order_drink("綠茶", sugar="微糖", ice="少冰")` → `點餐：綠茶（少冰 / 微糖）`

---

### トピック 5：特殊記号 `/` と `*` による呼び出し制限（`calc_bmi`、`send_email`、`register`）
1. **`/`（位置専用引数 Positional-Only）**：`/` より**左側**の引数は位置でのみ渡せます（キーワード指定不可）。
   - `calc_bmi(65, 1.75)` → `BMI 為：21.2`
2. **`*`（キーワード専用引数 Keyword-Only）**：単独の `*` より**右側**の引数は必ずキーワード名を指定して渡す必要があります。
   - `send_email("student@example.com", subject="課堂通知", urgent=True)` → `寄給：student@example.com｜主旨：課堂通知｜急件：True`
3. **`/` と `*` の併用（`register`）**：
   - `def register(id_no, /, name, *, role="student"):`
   - `id_no` は位置専用、`name` は位置・キーワードの両方に対応、`role` はキーワード専用です。
   - `register("A01", "小明", role="leader")` → `編號：A01｜姓名：小明｜身分：leader`

---

### トピック 6：可変長引数 `*args` と `**kwargs`（`sum_scores`、`build_profile`）
- **`*scores`（`*args`）**：任意個数の位置引数を **`tuple`（タプル）** にまとめます。
  - `sum_scores(80, 90, 85)` → `(80, 90, 85) <class 'tuple'>` を受け取り、`255` を返します。
  - `sum_scores(80, 90)` → `170`、`sum_scores()` → `0` を返します。
- **`**info`（`**kwargs`）**：任意個数の追加キーワード引数を **`dict`（辞書）** にまとめます。
  - `build_profile("小華", city="台北", course="Python")` → `name` は `"小華"`、`info` は `{'city': '台北', 'course': 'Python'} <class 'dict'>` になります。

---

### トピック 7：組み込み関数 `print` の解説
定義：`print(*objects, sep=' ', end='\n', file=None, flush=False)`
- `*objects` により任意の数の値を渡せます。
- `sep` と `end` は `*objects` の後ろにあるため、キーワード引数として指定します。
  - `print('a', 'b', 1, 67, 89)` → `a b 1 67 89`
  - `print('a', 'b', 1, 67, 89, sep='-')` → `a-b-1-67-89`
  - `print('a', 'b', 1, 67, 89, end='讚啦!\n')` → `a b 1 67 89讚啦!`

---

### トピック 8：組み込み関数 `sorted` の解説
ノートブック内の表記：`sorted(iterable, *, key=None, reverse=False)`（実際の Python では `iterable` も位置専用引数です）。
- `reverse=True` をキーワード引数として渡すことで降順に並べ替えます。
  - `sorted([8, 92, 63, 75], reverse=True)` → `[92, 75, 63, 8]`
