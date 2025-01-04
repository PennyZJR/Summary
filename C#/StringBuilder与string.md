### `StringBuilder` 的特点

1. **可变性**：
   - 与 `string` 类型不同，`StringBuilder` 是可变的（mutable）。这意味着你可以在不创建新对象的情况下修改它的内容。
2. **高效性**：
   - 对于频繁的字符串拼接操作，`StringBuilder` 比 `string` 更高效，因为它避免了每次拼接时创建新字符串对象的开销。
3. **引用类型**：
   - `StringBuilder` 是引用类型，它的对象存储在堆（Heap）中，变量存储的是对象的引用。

### `StringBuilder` 的常用方法

| 方法       | 说明                                                  |
| :--------- | :---------------------------------------------------- |
| `Append`   | 在末尾追加字符串或对象。                              |
| `Insert`   | 在指定位置插入字符串或对象。                          |
| `Remove`   | 从指定位置移除指定数量的字符。                        |
| `Replace`  | 替换字符串中的字符或子字符串。                        |
| `ToString` | 将 `StringBuilder` 的内容转换为 `string`。            |
| `Clear`    | 清空 `StringBuilder` 的内容。                         |
| `Length`   | 获取或设置 `StringBuilder` 中字符的数量。             |
| `Capacity` | 获取或设置 `StringBuilder` 的容量（可存储的字符数）。 |

------

### `StringBuilder` 与 `string` 的区别

| 特性         | `StringBuilder`                                       | `string`                     |
| :----------- | :---------------------------------------------------- | :--------------------------- |
| **可变性**   | 可变（mutable）                                       | 不可变（immutable）          |
| **性能**     | 高效，适合频繁修改字符串                              | 低效，每次修改都会创建新对象 |
| **存储位置** | 堆（Heap）                                            | 堆（Heap）                   |
| **默认值**   | `null`                                                | `null`                       |
| **线程安全** | 非线程安全（除非使用 `StringBuilder` 的线程安全版本） | 线程安全（因为不可变）       |