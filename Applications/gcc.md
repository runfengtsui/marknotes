---
Title: gcc/g++
Author: 邱彼郑楠
Date: 2023-05-21
---

# g++ 默认标准

如果想要查看在 `g++` 编译且不使用 `-std=` 指定标准的情况下, `g++` 使用的默认标准, 可以通过以下测试文件和脚本文件进行.

测试文件为:

```cpp
#include <iostream>

int main(void) {
#ifdef __cplusplus
    std::cout << "__cplusplus = " << __cplusplus << std::endl;
#endif
#ifdef __STRICT_ANSI__
    std::cout << "__STRICT_ANSI__ = " << __STRICT_ANSI__ << std::endl;
#endif
    return 0;
}
```

脚本文件为 (根据 [【经验】如何查看gcc、g++不加-std时的默认版本](https://blog.csdn.net/u010168781/article/details/105440100) 中的脚本文件改写的 `fish` 脚本文件):

```bash
#!/usr/bin/fish
set STDS c++98 c++11 c++14 c++17 gnu++98 gnu++11 gnu++14 gnu++17
for STD in $STDS
    echo $STD
    g++ -std=$STD -o cpp.out cpp.cpp
    ./cpp.out
    echo
end

echo default
g++ -o cpp.out cpp.cpp
./cpp.out
```

更改脚本文件的可执行权限 `chmod u+x`, 经过运行最后得出目前 `g++` 使用的默认标准为 `gnu++17`.
