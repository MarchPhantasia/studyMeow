## 从 `Linux 0.11` 现在的机制看，它的系统调用最多能传递几个参数？

在 `Linux 0.11` 的当前机制中，系统调用最多能直接传递 **三个参数**。这是因为：

1. 系统调用通过软中断 `int 0x80` 进入内核态时，用户程序需要通过寄存器传递参数。
2. `Linux 0.11` 使用了 `ebx`、`ecx` 和 `edx` 三个寄存器来存储参数。
3. 在 `unistd.h` 中，系统调用的宏 `_syscall1`、`_syscall2` 和 `_syscall3` 分别支持传递 1、2 和 3 个参数，这也体现了这一限制。

因此，`Linux 0.11` 系统调用直接传递参数的上限是 **3 个**。

---

## 你能想出办法来扩大这个限制吗？

可以通过以下方法突破 3 个参数的限制：

### 方法一：通过内存结构传递参数

- **思路**：将需要传递的多个参数封装到一个结构体中，用户态程序将结构体的地址作为一个参数传递给内核，内核通过该地址访问所有参数。
- **实现步骤**：
    1. 在用户态定义一个参数结构体，例如：

        ```c
        struct params {
            int arg1;
            char arg2[20];
            long arg3;
            double arg4;
        };
        ```

    2. 在用户程序中填充结构体，并将其地址传递给系统调用：

        ```c
        struct params p = {123, "test", 456789, 3.14};
        syscall(__NR_custom, &p);
        ```

    3. 在内核态使用地址访问结构体内容：

        ```c
        struct params user_params;
        copy_from_user(&user_params, param_addr, sizeof(user_params));
        ```

### 方法二：使用堆栈传递更多参数

- **思路**：在进入内核态时，用户程序将多余参数压入堆栈，内核通过栈指针访问这些参数。
- **实现方式**：
    - 修改系统调用的处理逻辑，使其支持从堆栈中读取参数。
    - 但此方法复杂度较高，且需要对堆栈管理和安全性进行额外考虑。

### 方法三：分批传递参数

- **思路**：将参数分批传递，每次系统调用传递部分参数，并在内核中组合。
- **实现方式**：
    - 用户程序通过多次调用，将参数逐步传递到内核。
    - 内核为此系统调用维护一个状态，用于存储已接收的参数。

方法一（使用内存结构）是最常用的方式，因为其简单易用，同时能够兼容现有的机制。

---

## 用文字简要描述向 `Linux 0.11` 添加一个系统调用 `foo()` 的步骤

向 `Linux 0.11` 添加一个系统调用 `foo()` 的完整步骤如下：

### 步骤 1：编写系统调用函数

在 `kernel/` 目录下创建或编辑 `.c` 文件，例如在 `kernel/sys.c` 中添加：

```c
#include <linux/kernel.h> // 必须包含以使用 printk

int sys_foo(int arg1, const char *arg2) {
    printk("sys_foo called with arg1=%d and arg2=%s\n", arg1, arg2);
    return 0; // 返回结果
}
```

### 步骤 2：声明系统调用函数

在 `include/linux/sys.h` 文件中声明新增的系统调用函数：

```c
extern int sys_foo(int arg1, const char *arg2);
```

### 步骤 3：注册系统调用

在 `include/linux/sys.h` 文件中的 `sys_call_table` 函数指针表中添加新系统调用：

```c
fn_ptr sys_call_table[] = {
    …,
    sys_foo, // 将 sys_foo 添加到表中
};
```

### 步骤 4：定义系统调用编号

在 `include/unistd.h` 文件中为 `foo()` 定义系统调用编号：

```c
#define __NR_foo 74
```

### 步骤 5：修改系统调用总数

在 `kernel/system_call.s` 文件中修改 `nr_system_calls` 的值，将系统调用总数加 1：

```asm
.nr_system_calls = 75
```

### 步骤 6：编写用户态 API

在用户态库中创建对应的 API。例如，在 `lib/foo.c` 文件中：

```c
#define __LIBRARY__
#include <unistd.h> // 包含系统调用号定义
_syscall2(int, foo, int, arg1, const char *, arg2);
```

### 步骤 7：测试系统调用

编写一个测试程序 `test_foo.c`：

```c
#define __LIBRARY__
#include <unistd.h>
#include <stdio.h>

_syscall2(int, foo, int, arg1, const char *, arg2);

int main() {
    int result = foo(123, "hello");
    printf("foo() returned %d\n", result);
    return 0;
}
```

### 步骤 8：重新编译内核

- 修改 `Makefile`，确保新增 `.c` 文件会被编译。
- 编译内核：

    ```bash
    make
    ```

### 步骤 9：运行测试程序

将测试程序复制到虚拟机运行，并验证系统调用是否正确工作：

```bash
gcc -o test_foo test_foo.c
./test_foo
```

完成以上步骤后，新的系统调用 `foo()` 即可在 `Linux 0.11` 中正常使用。
