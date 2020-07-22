[toc]

## Task 1  变量、运算符与数据类型

## 1. 注释

`''' '''` 或者 `""" """` 表示区间注释，在三引号之间的所有内容被注释

## 2. 运算符

| 操作符 | 名称           | 示例          |
| ------ | -------------- | ------------- |
| `+`    | 加             | `1 + 1`       |
| `-`    | 减             | `2 - 1`       |
| `*`    | 乘             | `3 * 4`       |
| `/`    | 除             | `3 / 4` =0.75 |
| `//`   | 整除（地板除） | `3 // 4` =0   |
| `%`    | 取余           | `3 % 4` = 3   |
| `**`   | 幂             | `2 ** 3`      |

**位运算符**

| 操作符 | 名称     | 示例     |
| ------ | -------- | -------- |
| `~`    | 按位取反 | `~4`     |
| `&`    | 按位与   | `4 & 5`  |
| `|`    | 按位或   | `4 | 5`  |
| `^`    | 按位异或 | `4 ^ 5`  |
| `<<`   | 左移     | `4 << 2` |
| `>>`   | 右移     | `4 >> 2` |

**三元运算符**

```python
x, y = 4, 5
if x < y:
    small = x
else:
    small = y

print(small)  # 4
```

有了这个三元操作符的条件表达式，你可以使用一条语句来完成以上的条件判断和赋值操作。

```python
x, y = 4, 5
small = x if x < y else y
print(small)  # 4
```

**其他运算符**

| 操作符   | 名称   | 示例                         |
| -------- | ------ | ---------------------------- |
| `in`     | 存在   | `'A' in ['A', 'B', 'C']`     |
| `not in` | 不存在 | `'h' not in ['A', 'B', 'C']` |
| `is`     | 是     | `"hello" is "hello"`         |
| `is not` | 不是   | `"hello" is not "hello"`     |

当比较的两个变量均指向不可变类型：

```python
a = "hello"
b = "hello"
print(a is b, a == b)  # True True
print(a is not b, a != b)  # False False
```

当比较的两个变量均指向可变类型：

```python
a = ["hello"]
b = ["hello"]
print(a is b, a == b)  # False True
print(a is not b, a != b)  # True False
```

注意：

- is, is not 对比的是两个变量的**内存地址**
- ==, != 对比的是两个变量的**值**
- 比较的两个变量，指向的都是**地址不可变的类型（str等），那么is，is not 和 ==，！= 是完全等价的**。
- 对比的两个变量，指向的是**地址可变的类型（list，dict等），则两者是有区别的**。

**运算符的优先级**

- 一元运算符优于二元运算符。例如`3 ** -2`等价于`3 ** (-2)`。
- 先算术运算，后移位运算，最后位运算。例如 `1 << 3 + 2 & 7`等价于 `(1 << (3 + 2)) & 7`。
- 逻辑运算最后结合。例如`3 < 4 and 4 < 5`等价于`(3 < 4) and (4 < 5)`。

## 3. 变量和赋值

## 4. 数据类型与转换

Python 里面万物皆对象（object），整型也不例外，只要是对象，就有相应的属性 （attributes） 和方法（methods）。

有时候我们想保留浮点型的小数点后 `n` 位。可以用 `decimal` 包里的 `Decimal` 对象和 `getcontext()` 方法来实现。

```
import decimal
from decimal import Decimal
```

Python 里面有很多用途广泛的包 (package)，用什么你就引进 (import) 什么。包也是对象，也可以用上面提到的`dir(decimal)` 来看其属性和方法。

【例子】`getcontext()` 显示了 `Decimal` 对象的默认精度值是 28 位 (`prec=28`)。

```python
a = decimal.getcontext()
print(a)

# Context(prec=28, rounding=ROUND_HALF_EVEN, Emin=-999999, Emax=999999,
# capitals=1, clamp=0, flags=[], 
# traps=[InvalidOperation, DivisionByZero, Overflow])
b = Decimal(1) / Decimal(3)
print(b)

# 0.3333333333333333333333333333
```

【例子】使 1/3 保留 4 位，用 `getcontext().prec` 来调整精度。

```python
decimal.getcontext().prec = 4
c = Decimal(1) / Decimal(3)
print(c)

# 0.3333
```

**布尔型**

布尔 (boolean) 型变量只能取两个值，`True` 和 `False`。当把布尔型变量用在数字运算中，用 `1` 和 `0` 代表 `True` 和 `False`。

除了直接给变量赋值 `True` 和 `False`，还可以用 `bool(X)` 来创建变量，其中 `X` 可以是

- 基本类型：整型、浮点型、布尔型
- 容器类型：字符串、元组、列表、字典和集合

【例子】`bool` 作用在基本类型变量：`X` 只要不是整型 `0`、浮点型 `0.0`，`bool(X)` 就是 `True`，其余就是 `False`。

```python
print(type(0), bool(0), bool(1))
# <class 'int'> False True

print(type(10.31), bool(0.00), bool(10.31))
# <class 'float'> False True

print(type(True), bool(False), bool(True))
# <class 'bool'> False True
```

【例子】`bool` 作用在容器类型变量：`X` 只要不是空的变量，`bool(X)` 就是 `True`，其余就是 `False`。

```python
print(type(''), bool(''), bool('python'))
# <class 'str'> False True

print(type(()), bool(()), bool((10,)))
# <class 'tuple'> False True

print(type([]), bool([]), bool([1, 2]))
# <class 'list'> False True

print(type({}), bool({}), bool({'a': 1, 'b': 2}))
# <class 'dict'> False True

print(type(set()), bool(set()), bool({1, 2}))
# <class 'set'> False True
```

确定`bool(X)` 的值是 `True` 还是 `False`，就看 `X` 是不是空，空的话就是 `False`，不空的话就是 `True`。

- 对于数值变量，`0`, `0.0` 都可认为是空的。
- 对于容器变量，里面没元素就是空的。

**获取类型信息**

- `type(object)` 获取类型信息

- `isinstance(object, classinfo)` 判断一个对象是否是一个已知的类型。

【例子】

```python
print(isinstance(1, int))  # True
print(isinstance(5.2, float))  # True
print(isinstance(True, bool))  # True
print(isinstance('5.2', str))  # True
```

注：

- `type()` 不会认为子类是一种父类类型，不考虑继承关系。
- `isinstance()` 会认为子类是一种父类类型，考虑继承关系。

如果要判断两个类型是否相同推荐使用 `isinstance()`。

> 什么是继承？

**类型转换**

- 转换为整型 `int(x, base=10)`
- 转换为字符串 `str(object='')`
- 转换为浮点型 `float(x)`

```python
print(int('520'))  # 520
print(int(520.52))  # 520
print(float('520.52'))  # 520.52
print(float(520))  # 520.0
print(str(10 + 10))  # 20
print(str(10.1 + 5.2))  # 15.3
```

## 5. print() 函数

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

- 将对象以字符串表示的方式格式化输出到流文件对象file里。其中所有非关键字参数都按`str()`方式进行转换为字符串输出；
- 关键字参数`sep`是实现分隔符，比如多个参数输出时想要输出中间的分隔字符；
- 关键字参数`end`是输出结束时的字符，默认是换行符`\n`；
- 关键字参数`file`是定义流输出的文件，可以是标准的系统输出`sys.stdout`，也可以重定义为别的文件；
- 关键字参数`flush`是立即把内容输出到流文件，不作缓存。

【例子】没有参数时，每次输出后都会换行。

```python
shoplist = ['apple', 'mango', 'carrot', 'banana']
print("This is printed without 'end'and 'sep'.")
for item in shoplist:
    print(item)

# This is printed without 'end'and 'sep'.
# apple
# mango
# carrot
# banana
```

【例子】每次输出结束都用`end`设置的参数`&`结尾，并没有默认换行。

```python
shoplist = ['apple', 'mango', 'carrot', 'banana']
print("This is printed with 'end='&''.")
for item in shoplist:
    print(item, end='&')
print('hello world')

# This is printed with 'end='&''.
# apple&mango&carrot&banana&hello world
```

【例子】`item`值与`'another string'`两个值之间用`sep`设置的参数`&`分割。由于`end`参数没有设置，因此默认是输出解释后换行，即`end`参数的默认值为`\n`。

```python
shoplist = ['apple', 'mango', 'carrot', 'banana']
print("This is printed with 'sep='&''.")
for item in shoplist:
    print(item, 'another string', sep='&')

# This is printed with 'sep='&''.
# apple&another string
# mango&another string
# carrot&another string
# banana&another string
```

## 6. 位运算

**原码、反码和补码**

二进制有三种不同的表示形式：原码、反码和补码，计算机内部使用补码来表示。

**原码**：就是其二进制表示（注意，最高位是符号位）。

```
00 00 00 11 -> 3
10 00 00 11 -> -3
```

**反码**：正数的反码就是原码，负数的反码是符号位不变，其余位取反（对应正数按位取反）。

```
00 00 00 11 -> 3
11 11 11 00 -> -3
```

**补码**：正数的补码就是原码，负数的补码是反码+1。

```
00 00 00 11 -> 3
11 11 11 01 -> -3
```

**符号位**：最高位为符号位，0表示正数，1表示负数。**在位运算中符号位也参与运算。**

**按位非操作 ~**

```
~ 1 = 0
~ 0 = 1
```

`~` 把`num`的补码中的 0 和 1 全部取反（0 变为 1，1 变为 0）有符号整数的符号位在 `~` 运算中同样会取反。

```
00 00 01 01 -> 5
~
---
11 11 10 10 -> -6

11 11 10 11 -> -5
~
---
00 00 01 00 -> 4
```

**按位与操作 &**

```
1 & 1 = 1
1 & 0 = 0
0 & 1 = 0
0 & 0 = 0
```

只有两个对应位都为 1 时才为 1

```
00 00 01 01 -> 5
&
00 00 01 10 -> 6
---
00 00 01 00 -> 4
```

**按位或操作 |**

```
1 | 1 = 1
1 | 0 = 1
0 | 1 = 1
0 | 0 = 0
```

只要两个对应位中有一个 1 时就为 1

```
00 00 01 01 -> 5
|
00 00 01 10 -> 6
---
00 00 01 11 -> 7
```

**按位异或操作 ^**

```
1 ^ 1 = 0
1 ^ 0 = 1
0 ^ 1 = 1
0 ^ 0 = 0
```

只有两个对应位不同时才为 1

```
00 00 01 01 -> 5
^
00 00 01 10 -> 6
---
00 00 00 11 -> 3
```

异或操作的性质：满足交换律和结合律

```
A: 00 00 11 00
B: 00 00 01 11

A^B: 00 00 10 11
B^A: 00 00 10 11

A^A: 00 00 00 00
A^0: 00 00 11 00

A^B^A: = A^A^B = B = 00 00 01 11
```

**按位左移操作 <<**

`num << i` 将`num`的二进制表示向左移动`i`位所得的值。

```
00 00 10 11 -> 11
11 << 3
---
01 01 10 00 -> 88 
```

**按位右移操作 >>**

`num >> i` 将`num`的二进制表示向右移动`i`位所得的值。

```
00 00 10 11 -> 11
11 >> 2
---
00 00 00 10 -> 2 
```

**利用位运算实现快速计算**

通过 `<<`，`>>` 快速计算2的倍数问题。

```
n << 1 -> 计算 n*2
n >> 1 -> 计算 n/2，负奇数的运算不可用
n << m -> 计算 n*(2^m)，即乘以 2 的 m 次方
n >> m -> 计算 n/(2^m)，即除以 2 的 m 次方
1 << n -> 2^n
```

通过 `^` 快速交换两个整数。

```
a ^= b
b ^= a
a ^= b
```

通过 `a & (-a)` 快速获取`a`的最后为 1 位置的整数。

```
00 00 01 01 -> 5
&
11 11 10 11 -> -5
---
00 00 00 01 -> 1

00 00 11 10 -> 14
&
11 11 00 10 -> -14
---
00 00 00 10 -> 2
```

**利用位运算实现整数集合**

一个数的二进制表示可以看作是一个集合（0 表示不在集合中，1 表示在集合中）。

比如集合 `{1, 3, 4, 8}`，可以表示成 `01 00 01 10 10` 而对应的位运算也就可以看作是对集合进行的操作。

元素与集合的操作：

```
a | (1<<i)  -> 把 i 插入到集合中
a & ~(1<<i) -> 把 i 从集合中删除
a & (1<<i)  -> 判断 i 是否属于该集合（零不属于，非零属于）
```

集合之间的操作：

```
a 补   -> ~a
a 交 b -> a & b
a 并 b -> a | b
a 差 b -> a & (~b)
```

注意：整数在内存中是以补码的形式存在的，输出自然也是按照补码输出。

【例子】C#语言输出负数。

```
class Program
{
    static void Main(string[] args)
    {
        string s1 = Convert.ToString(-3, 2);
        Console.WriteLine(s1); 
        // 11111111111111111111111111111101
        
        string s2 = Convert.ToString(-3, 16);
        Console.WriteLine(s2); 
        // fffffffd
    }
}
```

【例子】 Python 的`bin()` 输出。

```
print(bin(3))  # 0b11
print(bin(-3))  # -0b11

print(bin(-3 & 0xffffffff))  
# 0b11111111111111111111111111111101

print(bin(0xfffffffd))       
# 0b11111111111111111111111111111101

print(0xfffffffd)  # 4294967293
```

是不是很颠覆认知，我们从结果可以看出：

- Python中`bin`一个负数（十进制表示），输出的是它的原码的二进制表示加上个负号，巨坑。
- Python中的整型是补码形式存储的。
- Python中整型是不限制长度的不会超范围溢出。

所以为了获得负数（十进制表示）的补码，需要手动将其和十六进制数`0xffffffff`进行按位与操作，再交给`bin()`进行输出，得到的才是负数的补码表示。

