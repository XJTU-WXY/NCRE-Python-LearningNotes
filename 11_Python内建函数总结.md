# Python 内建函数

## 数学计算相关函数
| 函数 | 功能 | 参数说明 | 返回值 | 对应的魔法方法 | 注意事项 |
|------|------|---------|------|------------|--------------|
| `abs(x)` | 取绝对值 | `x`（数值或复数） | `x` 的绝对值 | `x.__abs__()` | 用于复数时，返回模 |
| `divmod(a, b)` | 返回商和余数的元组 | `a, b`（数值） | `(商, 余数)` 的元组 | `a.__divmod__(b)` | `b` 不能为 0 |
| `pow(x, y, mod)` | 计算幂 | `x, y, mod`（可选） | `x ** y % mod` | `x.__pow__(y[, mod])` | `mod` 计算更高效 |
| `round(n, d)` | 银行家舍入 | `n`（数值），`d`（可选） | `n` 的四舍五入结果 | `x.__round__(d)` | 遇 `.5` 时，偶数优先 |
| `sum(iter, start)` | 计算总和 | `iter`（可迭代对象），`start`（可选） | 元素总和 | 无 | `sum()` 不能用于字符串拼接 |
| `max(*args, key)` | 返回最大值 | `iter` 或多个值，`key`（可选） | 最大值 | 无 | 空 `iterable` 需 `default` |
| `min(*args, key)` | 返回最小值 | `iter` 或多个值，`key`（可选） | 最小值 | 无 | 空 `iterable` 需 `default` |

### 1. `abs(x)`
**功能**：返回一个数的绝对值。  
**参数**：
- `x`：一个整数或浮点数，或实现了 `__abs__()` 方法的对象。 
   
**返回值**：
- `x` 的绝对值。  
  
**注意事项**：
- `abs()` 也适用于复数，返回的是复数的模。例如：
  ```python
  abs(3 + 4j)  # 5.0
  ```

---

### 2. `divmod(a, b)`
**功能**：返回 `(a // b, a % b)`，即 `a` 除以 `b` 的商和余数组成的元组。  
**参数**：
- `a`：被除数（整数或浮点数）。  
- `b`：除数（非零整数或浮点数）。  
  
**返回值**：
- 一个包含 `(商, 余数)` 的元组。  
  
**注意事项**：
- 对于浮点数，商部分是 `floor(a / b)`（向下取整的商），而余数是 `a - (b * floor(a / b))`：
  ```python
  divmod(10.5, 3)  # (3.0, 1.5)
  ```
- 如果 `b` 为 0，会抛出 `ZeroDivisionError`。

---

### 3. `pow(x, y, mod=None)`
**功能**：计算 `x` 的 `y` 次幂，若提供 `mod` 参数，则返回 `(x ** y) % mod`。  
**参数**：
- `x`：底数（整数、浮点数或实现了 `__pow__()` 的对象）。  
- `y`：指数（整数、浮点数或实现了 `__pow__()` 的对象）。  
- `mod`（可选）：如果提供，则计算 `(x ** y) % mod`，其中 `mod` 必须是正整数。  

**返回值**：
- `x ** y` 的值，或 `(x ** y) % mod`。  

**注意事项**：
- `pow(x, y, mod)` 比 `(x ** y) % mod` 计算更快，推荐使用：
  ```python
  pow(2, 3, 5)  # (2 ** 3) % 5 = 8 % 5 = 3
  ```
- `pow()` 也适用于负指数：
  ```python
  pow(2, -3)  # 1 / (2 ** 3) = 0.125
  ```

---

### 4. `round(number, ndigits=None)`
**功能**：对 `number` 进行四舍五入，保留 `ndigits` 位小数。  
**参数**：
- `number`：要四舍五入的数字（整数或浮点数）。  
- `ndigits`（可选）：保留的小数位数（默认为 `None`，表示返回整数）。  

**返回值**：
- 经过四舍五入的数字，整数或浮点数。  

**注意事项**：
- `round()` 遇到 `.5` 时，默认采用 **"银行家舍入法"**，即**四舍六入，五看前一**：
  ```python
  round(2.5)  # 2（偶数优先）
  round(3.5)  # 4
  ```
- 可以指定 `ndigits`：
  ```python
  round(3.14159, 2)  # 3.14
  ```

---

### 5. `sum(iterable, start=0)`
**功能**：计算 `iterable` 里所有元素的和，并加上 `start`（默认为 0）。  
**参数**：
- `iterable`：可迭代对象，如列表、元组等，元素必须是数值。  
- `start`（可选）：初始值，默认 `0`，可用于累加。  

**返回值**：
- `iterable` 所有元素相加的结果。  

**注意事项**：
- `sum()` 不能用于字符串拼接：
  ```python
  sum(["a", "b", "c"])  # TypeError
  ```
- 可用于初始值累加：
  ```python
  sum([1, 2, 3], 10)  # 16
  ```
- **对于大规模数据，`sum()` 可能比 `math.fsum()` 精度低**：
  ```python
  import math
  math.fsum([0.1, 0.2, 0.3])  # 0.6
  ```

---

### 6. `max(*args, key=None)` / `max(iterable, key=None)`
**功能**：返回最大值。  
**参数**：
- **单个可迭代对象**：`max(iterable, key=None)`。  
- **多个参数**：`max(a, b, c, ..., key=None)`。  
- `key`（可选）：用于比较的函数，默认为 `None`。
  
**返回值**：
- `iterable` 或参数中的最大值。  

**注意事项**：
- 可以使用 `key` 进行自定义比较：
  ```python
  max(["apple", "banana", "cherry"], key=len)  # 'banana'
  ```
- 空 `iterable` 会抛出 `ValueError`，可以使用 `default` 参数：
  ```python
  max([], default="No data")  # "No data"
  ```

---

### 7. `min(*args, key=None)` / `min(iterable, key=None)`
**功能**：返回最小值。  
**参数**：
- **单个可迭代对象**：`min(iterable, key=None)`。  
- **多个参数**：`min(a, b, c, ..., key=None)`。  
- `key`（可选）：用于比较的函数，默认为 `None`。  

**返回值**：
- `iterable` 或参数中的最小值。  

**注意事项**：
- `key` 用于自定义比较：
  ```python
  min(["apple", "banana", "cherry"], key=len)  # 'apple'
  ```
- 空 `iterable` 需指定 `default`：
  ```python
  min([], default="No data")  # "No data"
  ```

---

## 类型转换相关函数
| 函数       | 功能                     | 参数说明 | 返回值 | 对应的魔法方法 | 注意事项 |  
|--------------|------------------------------|----------------|------------------|----------------|-------------------------------|  
| `int(x, base=10)` | 转换为整数 | `x`：数字/字符串；`base`（进制，默认10） | 整数 | `__int__()` | `base` 仅用于字符串转换 |  
| `hex(x)` | 转换为十六进制字符串 | `x`：整数 | 形如 `'0xff'` 的字符串 | 无 | 负数也会转换 |  
| `oct(x)` | 转换为八进制字符串 | `x`：整数 | 形如 `'0o12'` 的字符串 | 无 | 负数也会转换 |  
| `bin(x)` | 转换为二进制字符串 | `x`：整数 | 形如 `'0b101'` 的字符串 | 无 | 负数也会转换 |  
| `float(x)` | 转换为浮点数 | `x`：数字/字符串 | 浮点数 | `__float__()` | 解析失败会抛 `ValueError` |  
| `str(x)` | 转换为字符串 | `x`：任意对象 | `x` 的字符串表示 | `__str__()` | 适用于所有对象 |  
| `bool(x)` | 转换为布尔值 | `x`：任意对象 | `True` 或 `False` | `__bool__()` | `0, '', [], {}, None` 为 `False` |  
| `bytes(x, encoding, errors)` | 转换为字节对象 | `x`：整数/字符串/可迭代对象 | `bytes` 对象 | `__bytes__()` | `x` 为字符串时需指定 `encoding` |  
| `bytearray(x, encoding, errors)` | 转换为字节数组 | `x`：整数/字符串/可迭代对象 | `bytearray` 对象 | 无 | 可变对象，可修改内容 |  
| `complex(real, imag=0.0)` | 转换为复数 | `real`：实部，`imag`：虚部 | 复数 `real + imag*j` | `__complex__()` | 也可解析字符串格式 |  
| `list(iterable)` | 转换为列表 | `iterable`：可迭代对象 | 列表对象 | `__iter__()` | 适用于字符串、元组等 |  
| `tuple(iterable)` | 转换为元组 | `iterable`：可迭代对象 | 元组对象 | `__iter__()` | 适用于生成不可变序列 |  
| `dict(**kwargs)` / `dict(mapping, **kwargs)` | 转换为字典 | `mapping`：键值对；`kwargs`：键值参数 | 字典对象 | `__getitem__()` | 支持 `list of tuples` |  
| `set(iterable)` | 转换为集合 | `iterable`：可迭代对象 | 集合对象 | `__iter__()` | 自动去重 |  
| `frozenset(iterable)` | 转换为不可变集合 | `iterable`：可迭代对象 | `frozenset` 对象 | `__iter__()` | 不可修改 |  
| `memoryview(obj)` | 创建内存视图 | `obj`：必须是 `bytes` 或 `bytearray` | `memoryview` 对象 | 无 | 用于高效处理二进制数据 |

### 1. `int(x, base=10)`
**功能**：将 `x` 转换为整数。  
**参数**：
- `x`：整数、浮点数、字符串、二进制、八进制、十六进制字符串或实现了 `__int__()` 方法的对象。  
- `base`（可选）：进制，默认为 `10`，用于转换字符串格式的数字。  
  
**返回值**：
- 转换后的整数值。  
  
**注意事项**：
- 如果 `x` 是浮点数，直接截断小数部分（**非四舍五入**）：
  ```python
  int(3.99)  # 3
  ```
- `x` 可以是字符串，但 `base` 需匹配：
  ```python
  int("10", 2)  # 2
  ```

---

### 2. `hex(x)`
**功能**：将整数 `x` 转换为十六进制字符串（以 `0x` 开头）。  
**参数**：
- `x`：整数。  
  
**返回值**：
- 以 `0x` 开头的十六进制字符串。  
  
**注意事项**：
- 负数也会转换：
  ```python
  hex(-255)  # '-0xff'
  ```

---

### 3. `oct(x)`
**功能**：将整数 `x` 转换为八进制字符串（以 `0o` 开头）。  
**参数**：
- `x`：整数。  
  
**返回值**：
- 以 `0o` 开头的八进制字符串。  
  
**注意事项**：
- 负数也会转换：
  ```python
  oct(-10)  # '-0o12'
  ```

---

### 4. `bin(x)`
**功能**：将整数 `x` 转换为二进制字符串（以 `0b` 开头）。  
**参数**：
- `x`：整数。  
  
**返回值**：
- 以 `0b` 开头的二进制字符串。  
  
**注意事项**：
- 负数也会转换：
  ```python
  bin(-5)  # '-0b101'
  ```

---

### 5. `float(x)`
**功能**：将 `x` 转换为浮点数。  
**参数**：
- `x`：整数、字符串或实现了 `__float__()` 方法的对象。  
  
**返回值**：
- 转换后的浮点数。  
  
**注意事项**：
- 可以转换科学计数法字符串：
  ```python
  float("1e-3")  # 0.001
  ```
- 对于无效字符串会抛出 `ValueError`：
  ```python
  float("abc")  # ValueError
  ```

---

### 6. `str(x)`
**功能**：将 `x` 转换为字符串。  
**参数**：
- `x`：任意对象，调用其 `__str__()` 方法。  
  
**返回值**：
- `x` 的字符串表示形式。  
  
**注意事项**：
- 适用于任何对象，包括 `None`：
  ```python
  str(None)  # 'None'
  ```

---

### 7. `bool(x)`
**功能**：将 `x` 转换为布尔值。  
**参数**：
- `x`：任意对象。  
  
**返回值**：
- `True` 或 `False`。  
  
**注意事项**：
- 只有以下值被认为是 `False`，其他均为 `True`：
  ```python
  bool(0)  # False
  bool("")  # False
  bool([])  # False
  bool(None)  # False
  ```

---

### 8. `bytes(x, encoding, errors)`
**功能**：将 `x` 转换为字节对象。  
**参数**：
- `x`：整数（生成 `x` 长度的 `b'\x00'`）、字符串（需指定 `encoding`），或可迭代对象。  
- `encoding`：如果 `x` 是字符串，则必须提供。  
- `errors`：错误处理策略，默认为 `strict`。  
  
**返回值**：
- 字节对象（`bytes`）。  
  
**注意事项**：
- 用于字符串时：
  ```python
  bytes("abc", "utf-8")  # b'abc'
  ```
- 用于整数：
  ```python
  bytes(3)  # b'\x00\x00\x00'
  ```

---

### 9. `bytearray(x, encoding, errors)`
**功能**：与 `bytes()` 类似，但返回的是可变字节数组。  
**参数**：
- 参考 `bytes()`。  
  
**返回值**：
- `bytearray` 对象。  
  
**注意事项**：
- 可变，可修改内容：
  ```python
  ba = bytearray(b"abc")
  ba[0] = 100
  print(ba)  # bytearray(b'dbc')
  ```

---

### 10. `complex(real, imag=0.0)`
**功能**：创建复数 `real + imag * j`。  
**参数**：
- `real`：实部（整数或浮点数）。  
- `imag`（可选）：虚部（整数或浮点数）。  
  
**返回值**：
- 复数。  
  
**注意事项**：
- 也可解析字符串：
  ```python
  complex("1+2j")  # (1+2j)
  ```

---

### 11. `list(iterable)`
**功能**：将 `iterable` 转换为列表。  
**参数**：
- `iterable`：可迭代对象。  
  
**返回值**：
- 列表对象。  
  
**注意事项**：
- 可用于字符串：
  ```python
  list("abc")  # ['a', 'b', 'c']
  ```

---

### 12. `tuple(iterable)`
**功能**：将 `iterable` 转换为元组。  
**参数**：
- `iterable`：可迭代对象。  
  
**返回值**：
- 元组对象。  
  
**注意事项**：
- 适用于生成不可变的序列。

---

### 13. `dict(**kwargs)` / `dict(mapping, **kwargs)`
**功能**：创建字典。  
**参数**：
- `kwargs`：键值对参数。  
- `mapping`：可迭代键值对。  
  
**返回值**：
- 字典对象。  
  
**注意事项**：
- 可用 `list of tuples`：
  ```python
  dict([("a", 1), ("b", 2)])  # {'a': 1, 'b': 2}
  ```

---

### 14. `set(iterable)`
**功能**：将 `iterable` 转换为集合（去重）。  
**参数**：
- `iterable`：可迭代对象。  
  
**返回值**：
- 集合对象。  
  
**注意事项**：
- 可用于去重：
  ```python
  set("banana")  # {'a', 'b', 'n'}
  ```

---

### 15. `frozenset(iterable)`
**功能**：创建不可变集合。  
**参数**：
- `iterable`：可迭代对象。  
  
**返回值**：
- `frozenset` 对象。  
  
**注意事项**：
- `frozenset` 不可修改：
  ```python
  fs = frozenset([1, 2, 3])
  fs.add(4)  # AttributeError
  ```

---

### 16. `memoryview(obj)`
**功能**：创建内存视图。  
**参数**：
- `obj`：必须是 `bytes` 或 `bytearray`。  
  
**返回值**：
- `memoryview` 对象。  
  
**注意事项**：
- 适用于高效处理二进制数据。

---

## 序列操作相关函数
| 函数        | 功能                   | 参数说明                                      | 返回值                         | 对应魔法方法    | 注意事项                                              |
|------------|----------------------|----------------------------------|-----------------|----------------|----------------------------------|
| `len(s)`  | 获取序列 `s` 的长度 | `s`：可迭代对象（列表、字符串、字典等）  | `int`（元素个数） | `__len__()`  | 字典 `len(d)` 返回键的个数。 |
| `range(start, stop, step=1)`  | 生成从 `start` 到 `stop`（不含）的等差数列 | `start`（起始值，默认 `0`），`stop`（终点，不含），`step`（步长，默认 `1`） | `range` 对象（可迭代） | 无 | `range` 需用 `list()` 转换才能看到内容。 |
| `iter(iterable)` | 获取可迭代对象的迭代器 | `iterable`：可迭代对象（列表、字符串等） | 迭代器对象 | `__iter__()` | 迭代器只能遍历一次。 |
| `next(iterator, default)` | 获取迭代器的下一个值 | `iterator`：迭代器对象，`default`（可选，迭代结束时返回） | 迭代器的下一个值 | `__next__()` | 若 `default` 未提供且迭代结束，则抛 `StopIteration`。 |
| `sorted(iterable, key=None, reverse=False)` | 返回排序后的列表 | `iterable`（可迭代对象），`key`（排序依据函数，可选），`reverse`（是否降序，默认 `False`） | 排序后的新 `list` | 无 | 原序列不变，`key` 可用于自定义排序。 |
| `reversed(seq)` | 反转序列 | `seq`：支持反转的序列（列表、字符串、元组） | 反转后的迭代器 | `__reversed__()` | 需用 `list()` 转换才能看到内容。 |
| `slice(start, stop, step=1)` | 创建切片对象 | `start`（起始索引），`stop`（结束索引，不含），`step`（步长，默认 `1`） | 切片对象 | `__getitem__()` | 可用于 `[]` 切片操作。 |
| `zip(*iterables)` | 打包多个可迭代对象 | `*iterables`（多个可迭代对象） | 迭代器，每个元素为元组 | 无 | 以最短的可迭代对象长度为准。 |
| `enumerate(iterable, start=0)` | 生成带索引的迭代对象 | `iterable`（可迭代对象），`start`（索引起始值，默认 `0`） | 迭代器，每个元素为 `(index, item)` 元组 | 无 | 适用于 `for` 循环遍历。 |

### 1. `len(s)`
**功能**：获取序列 `s` 的长度（元素个数）。  
**参数**：
- `s`：字符串、列表、元组、集合、字典、range 对象等支持 `__len__()` 方法的对象。  
  
**返回值**：
- 序列的元素个数（整数）。  

**注意事项**：
- 对字典使用时，返回键的个数：
  ```python
  len({"a": 1, "b": 2})  # 2
  ```

---

### 2. `range(start, stop, step=1)`
**功能**：生成从 `start` 到 `stop`（不含）的等差数列。  
**参数**：
- `start`（可选）：起始值，默认 `0`。  
- `stop`：结束值（**不包含**）。  
- `step`（可选）：步长，默认 `1`，可为负数。  

**返回值**：
- `range` 对象，可迭代。  

**注意事项**：
- `range` 需转换为 `list()` 才能看到元素：
  ```python
  list(range(1, 6, 2))  # [1, 3, 5]
  ```

---

### 3. `iter(iterable)`
**功能**：获取 `iterable` 的迭代器。  
**参数**：
- `iterable`：可迭代对象（如列表、字符串、字典等）。  
  
**返回值**：
- 迭代器对象。  
  
**注意事项**：
- 迭代器只能遍历一次：
  ```python
  it = iter([1, 2, 3])
  next(it)  # 1
  next(it)  # 2
  ```

---

### 4. `next(iterator, default)`
**功能**：获取迭代器 `iterator` 的下一个值。  
**参数**：
- `iterator`：必须是一个迭代器。  
- `default`（可选）：如果迭代器结束，返回 `default` 而非抛出 `StopIteration`。  

**返回值**：
- 迭代器的下一个元素。  
  
**注意事项**：
- 如果迭代器结束且无 `default`，抛 `StopIteration`：
  ```python
  it = iter([1])
  next(it)  # 1
  next(it, "No more")  # "No more"
  ```

---

### 5. `sorted(iterable, key=None, reverse=False)`
**功能**：返回 `iterable` 排序后的列表。  
**参数**：
- `iterable`：可迭代对象。  
- `key`（可选）：指定排序依据的函数。  
- `reverse`（可选）：是否降序，默认 `False`（升序）。  
  
**返回值**：
- 排序后的新列表（原序列不变）。  
  
**注意事项**：
- 可按字符串长度排序：
  ```python
  sorted(["apple", "pear", "banana"], key=len)  # ['pear', 'apple', 'banana']
  ```

---

### 6. `reversed(seq)`
**功能**：返回 `seq` 反转后的迭代器。  
**参数**：
- `seq`：支持反转的序列（如列表、字符串、元组）。  
  
**返回值**：
- 反转后的迭代器。  
  
**注意事项**：
- `reversed()` 返回的是迭代器，如需列表可用 `list()`：
  ```python
  list(reversed("abc"))  # ['c', 'b', 'a']
  ```

---

### 7. `slice(start, stop, step=1)`
**功能**：创建一个切片对象。  
**参数**：
- `start`：起始索引。  
- `stop`：结束索引（**不包含**）。  
- `step`（可选）：步长，默认 `1`。  
  
**返回值**：
- 切片对象，可用于 `[]` 操作。  
  
**注意事项**：
- `slice` 适用于多次使用的情况：
  ```python
  s = slice(1, 4)
  [0, 1, 2, 3, 4][s]  # [1, 2, 3]
  ```

---

### 8. `zip(*iterables)`
**功能**：将多个可迭代对象元素按索引组合成元组。  
**参数**：
- `*iterables`：多个可迭代对象。  
  
**返回值**：
- 迭代器，每个元素为元组。  
  
**注意事项**：
- 以最短序列为准：
  ```python
  list(zip([1, 2], ["a", "b", "c"]))  # [(1, 'a'), (2, 'b')]
  ```

---

### 9. `enumerate(iterable, start=0)`
**功能**：生成带索引的 `iterable` 迭代对象。  
**参数**：
- `iterable`：可迭代对象。  
- `start`（可选）：索引起始值，默认 `0`。  
  
**返回值**：
- 迭代器，每个元素为 `(index, item)` 元组。  
  
**注意事项**：
- 适用于 `for` 循环：
  ```python
  list(enumerate("abc", 1))  # [(1, 'a'), (2, 'b'), (3, 'c')]
  ```

---

### 高阶函数
| 函数        | 功能                     | 参数说明                         | 返回值   | 注意事项 |
|------------|----------------------|-----------------|------------------|-----------------------|
| `filter(function, iterable)` | 过滤可迭代对象 | `function`（判断是否保留元素的函数），`iterable`（可迭代对象） | 迭代器，仅包含 `function(item)` 为 `True` 的元素 | 需用 `list()` 转换查看结果。 |
| `map(function, iterable, ...)` | 对可迭代对象应用函数 | `function`（应用的函数），`iterable`（一个或多个可迭代对象） | 迭代器，每个元素为 `function(item)` 的返回值 | `function` 需接受相应参数个数。 |
| `all(iterable)` | 判断是否所有元素为 `True` | `iterable`（可迭代对象） | `bool` | 空 `iterable` 返回 `True`。 |
| `any(iterable)` | 判断是否存在 `True` 元素 | `iterable`（可迭代对象） | `bool` | 空 `iterable` 返回 `False`。 |

### 1. `filter(function, iterable)`
**功能**：筛选 `iterable` 中 `function(item)` 为 `True` 的元素。  
**参数**：
- `function`：返回布尔值的函数。  
- `iterable`：可迭代对象。  
  
**返回值**：
- 迭代器，仅包含 `True` 结果的元素。  

**注意事项**：
- 过滤大于 `2` 的元素：
  ```python
  list(filter(lambda x: x > 2, [1, 2, 3]))  # [3]
  ```

---

### 2. `map(function, iterable, ...)`
**功能**：对 `iterable` 的每个元素应用 `function`。  
**参数**：
- `function`：处理元素的函数。  
- `iterable`：一个或多个可迭代对象。  
  
**返回值**：
- 迭代器，每个元素为 `function(item)` 的返回值。  
  
**注意事项**：
- 多个 `iterable` 时，`function` 需接受相同数量的参数：
  ```python
  list(map(lambda x, y: x + y, [1, 2, 3], [4, 5, 6]))  # [5, 7, 9]
  ```

---

### 3. `all(iterable)`
**功能**：判断 `iterable` 是否所有元素均为 `True`。  
**参数**：
- `iterable`：可迭代对象。  
  
**返回值**：
- `True`（全为真），`False`（存在假）。  
  
**注意事项**：
- 适用于 `bool()` 解析：
  ```python
  all([True, 1, "abc"])  # True
  all([True, 0, "abc"])  # False
  ```

---

### 4. `any(iterable)`
**功能**：判断 `iterable` 是否存在 `True` 的元素。  
**参数**：
- `iterable`：可迭代对象。  
  
**返回值**：
- `True`（存在真），`False`（全为假）。  
  
**注意事项**：
- 适用于检查非空：
  ```python
  any([False, 0, "", "abc"])  # True
  any([False, 0, ""])  # False
  ```

---

### 输入输出相关函数
| 函数名   | 函数功能                     | 示例                         |
|----------|------------------------------|------------------------------|
| print()  | 输出到控制台                 | `print("Hello")`            |
| input()  | 读取用户输入                 | `input("Enter: ")`          |
| open()   | 打开文件                     | `open("file.txt", "r")`     |

### 变量及作用域相关函数
| 函数名       | 函数功能                      | 示例                         |
|--------------|------------------------------|------------------------------|
| globals()    | 获取全局变量                  | `globals()`                  |
| locals()     | 获取局部变量                  | `locals()`                   |
| vars()       | 获取对象的 `__dict__`         | `vars(object)`               |

### 反射与动态执行
| 函数名      | 函数功能                     | 示例                         |
|-------------|------------------------------|------------------------------|
| getattr()   | 获取对象属性                 | `getattr(obj, "attr")`      |
| setattr()   | 设置对象属性                 | `setattr(obj, "attr", 42)`  |
| hasattr()   | 判断对象是否有某属性         | `hasattr(obj, "attr")`      |
| delattr()   | 删除对象属性                 | `delattr(obj, "attr")`      |

### 类型判断和操作
| 函数名        | 函数功能                     | 示例                          |
|--------------|-----------------------------|------------------------------|
| isinstance() | 判断对象是否是某类型         | `isinstance(123, int)`       |
| issubclass() | 判断是否是子类               | `issubclass(bool, int)`      |
| type()       | 获取对象类型                 | `type(123)  # <class 'int'>` |

### 其他杂项函数
| 函数名         | 函数功能                   | 示例                          |
|--------------|---------------------------|------------------------------|
| ascii()      | 返回可打印的 ASCII 字符串 | `ascii("你好")`             |
| chr()        | 返回 Unicode 字符         | `chr(97)  # 'a'`            |
| ord()        | 返回字符的 Unicode 码值   | `ord('a')  # 97`            |
| repr()       | 返回对象的字符串表示      | `repr("abc")  # "'abc'"`    |
| hash()       | 获取哈希值                 | `hash("abc")`               |

### 代码执行与编译
| 函数名       | 函数功能                     | 示例                          |
|-------------|-----------------------------|------------------------------|
| eval()      | 计算字符串表达式             | `eval("1+2")  # 3`          |
| exec()      | 执行字符串代码               | `exec("print(123)")`        |
| compile()   | 编译代码                     | `compile("1+2", "", "eval")` |

### 类与对象相关
| 函数名          | 函数功能                    | 示例                          |
|---------------|---------------------------|------------------------------|
| property()    | 创建属性访问器              | `class A: a = property()`   |
| staticmethod()| 定义静态方法                | `staticmethod(func)`        |
| classmethod() | 定义类方法                  | `classmethod(func)`         |
| super()       | 调用父类方法                | `super().method()`          |
