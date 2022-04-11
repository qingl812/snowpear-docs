# 二级制

- 将 n 二进制表示的最低位 1 移除 `n & (n - 1)`
- 获取 n 二进制表示的最低位的 1 `n & (-n)`

> 通过这两个方法，可以解决该问题
> 判断该整数是否是 2 的幂次方？
> `return n > 0 && (n & (n - 1)) == 0;`
> `return n > 0 && (n & -n) == n;`

- 输入二进制数

```c++
#include <bitset>

std::bitset<32> bits("1011");
auto i = bits.to_ulong();
// EXPECT_EQ(11, i);
```