# C#引用类型和值类型

在 C# 中，**引用类型**（Reference Types）是指那些在内存中存储的是对象的引用（即内存地址），而不是对象本身的数据。引用类型的变量存储的是指向堆（Heap）中对象的指针，而不是对象本身的值。1. **类（Class）**

类是典型的引用类型。所有用户定义的类、以及 .NET 框架中的许多内置类都是引用类型。

#### 示例

```c#
class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
}

Person p1 = new Person { Name = "Alice", Age = 25 };
Person p2 = p1; // p2 和 p1 指向同一个对象
p2.Name = "Bob";
Console.WriteLine(p1.Name); // 输出: Bob
```

------

### 2. **数组（Array）**

数组是引用类型，即使数组的元素是值类型（如 `int`），数组本身也是引用类型。

#### 示例

```c#
int[] arr1 = new int[] { 1, 2, 3 };
int[] arr2 = arr1; // arr2 和 arr1 指向同一个数组
arr2[0] = 10;
Console.WriteLine(arr1[0]); // 输出: 10
```

------

### 3. **字符串（String）**

`string` 是引用类型，但由于其不可变性（immutable），它的行为有时类似于值类型。

#### 示例

```c#
string s1 = "Hello";
string s2 = s1; // s2 和 s1 指向同一个字符串
s2 = "World"; // 由于字符串不可变，s2 现在指向一个新的字符串
Console.WriteLine(s1); // 输出: Hello
```

------

### 4. **委托（Delegate）**

委托是引用类型，用于存储对方法的引用。

#### 示例

```c#
delegate void MyDelegate(string message);

MyDelegate del = new MyDelegate(Console.WriteLine);
del("Hello, World!"); // 输出: Hello, World!
```

------

### 5. **接口（Interface）**

接口是引用类型，用于定义契约，实现接口的类或结构体必须实现接口中定义的方法。

#### 示例

```c#
interface IAnimal
{
    void Speak();
}

class Dog : IAnimal
{
    public void Speak() => Console.WriteLine("Woof!");
}

IAnimal animal = new Dog(); // 接口变量指向实现类的对象
animal.Speak(); // 输出: Woof!
```

------

### 6. **对象（Object）**

`object` 是所有类型的基类，它是一个引用类型。

#### 示例

```c#
object obj = new Person { Name = "Charlie", Age = 30 };
Console.WriteLine(obj.GetType()); // 输出: Person
```

------

### 7. **动态类型（Dynamic）**

`dynamic` 是引用类型，它在编译时不进行类型检查，而是在运行时解析。

#### 示例

```c#
dynamic value = "Hello";
value = 10; // 可以动态改变类型
Console.WriteLine(value); // 输出: 10
```

------

### 8. **集合类（Collections）**

大多数集合类（如 `List<T>`、`Dictionary<TKey, TValue>` 等）是引用类型。

#### 示例

```c#
List<int> list1 = new List<int> { 1, 2, 3 };
List<int> list2 = list1; // list2 和 list1 指向同一个列表
list2.Add(4);
Console.WriteLine(list1.Count); // 输出: 4
```

------

### 9. **自定义引用类型**

任何用户定义的类、接口、委托等都是引用类型。

------

### 引用类型的特点

1. **存储在堆中**：
   - 引用类型的对象存储在堆（Heap）中，变量存储的是对象的引用（内存地址）。
2. **赋值行为**：
   - 将一个引用类型变量赋值给另一个变量时，复制的是引用，而不是对象本身。
3. **默认值为 `null`**：
   - 引用类型的默认值是 `null`，表示没有指向任何对象。
4. **垃圾回收**：
   - 引用类型的对象由垃圾回收器（Garbage Collector）管理，当对象不再被引用时会被自动回收。

------

### 与值类型的区别

| 特性         | 引用类型                        | 值类型                        |
| :----------- | :------------------------------ | :---------------------------- |
| **存储位置** | 堆（Heap）                      | 栈（Stack）或堆（作为字段时） |
| **赋值行为** | 复制引用                        | 复制值                        |
| **默认值**   | `null`                          | 零值（如 `0`、`false` 等）    |
| **内存管理** | 由垃圾回收器管理                | 由栈自动管理                  |
| **示例**     | `class`、`string`、`List<T>` 等 | `int`、`bool`、`struct` 等    |

------

### 总结

C# 中的引用类型包括：

- 类（`class`）
- 数组（`array`）
- 字符串（`string`）
- 委托（`delegate`）
- 接口（`interface`）
- 对象（`object`）
- 动态类型（`dynamic`）
- 集合类（如 `List<T>`、`Dictionary<TKey, TValue>` 等）
- 自定义引用类型

引用类型的特点是变量存储的是对象的引用，而不是对象本身的值。