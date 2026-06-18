# 方案一：C++ 调用仓颉函数：“引入头文件 + 链接库”方案

本仓库演示如何在 C++ 中“像引入一个头文件一样”调用来自仓颉语言的函数。当前通过一个 Windows 下的 shim 静态库（`libcangjie_shim.a`）来承接调用：

- 直接提供一个 C ABI 的 `cj_helloworld()`，效果等同于运行 `helloworld.cj`（打印 `Hello, World!`）。
- 提供 `cj_helloworld_run(interpreter, script, outBuf, outBufSize)`：在 C++ 中启动外部仓颉解释器运行 `.cj` 脚本并捕获标准输出。
- 未来若你把仓颉函数用 `@C` 导出为 DLL（必要时配合 `@CallingConv[CDECL]`），可替换底层实现而无需改动 C/C++ 调用处。

```text
C++ 调用方 (helloworld.cpp / call_cj_from_cpp.cpp)
        │
        │  #include "cj_exports.h"
        ▼
C 接口头 (cj_exports.h) ───▶ 链接目标：libcangjie_shim.a（当前实现）
                                      │
                                      ├─ 运行外部解释器（cj_helloworld_run）
                                      └─ 内置 Hello（cj_helloworld）

[可替换] 未来链接目标：真实的仓颉导出 DLL/静态库（@C / @CallingConv[CDECL]）
```

---

## 目录结构

- `cj_exports.h`：对外头文件（C ABI）。
- `cangjie_shim.cpp`：Windows 下的 shim 实现（静态库建议）。
- `helloworld.cpp`：最小调用示例（只 include 头文件 + 调库）。
- `call_cj_from_cpp.cpp`：同风格示例（可选）。
- `helloworld.cj`：仓颉脚本，打印 “Hello, World!”.
- `default.cjo`：仓颉环境/工程文件（如有）。

---

## 快速开始（PowerShell）

前提：Windows，已安装 MinGW-w64 g++（或 MSVC，见下节）。在仓库根目录（本 README 同级）执行：

1. 构建静态库（当前 shim 实现）

```powershell
g++ -std=c++17 -O2 -c cangjie_shim.cpp -o cangjie_shim.o
ar rcs libcangjie_shim.a cangjie_shim.o
```

1. 构建调用示例

- 方案 A：构建 `helloworld.exe`

```powershell
g++ -std=c++17 -O2 -o helloworld.exe helloworld.cpp -L. -lcangjie_shim
```

- 方案 B：构建 `call_cj_from_cpp.exe`

```powershell
g++ -std=c++17 -O2 -o call_cj_from_cpp.exe call_cj_from_cpp.cpp -L. -lcangjie_shim
```

1. 运行

- 调用内置 Hello：

```powershell
./helloworld.exe
./call_cj_from_cpp.exe
```

- 运行真实仓颉脚本（需要你提供解释器路径）：

```powershell
./helloworld.exe 'C:\path\to\cangjie.exe' 'C:\Users\duck1\Desktop\cangjie\helloworld.cj'
# 或
./call_cj_from_cpp.exe 'C:\path\to\cangjie.exe' 'C:\Users\duck1\Desktop\cangjie\helloworld.cj'
```

---

## 使用 MSVC（可选）

若使用 Visual Studio 开发者命令提示（x64 本机工具），命令为：

```powershell
# 直接编译并链接（不生成 .lib）
cl /EHsc /O2 /std:c++17 helloworld.cpp cangjie_shim.cpp

# 运行
helloworld.exe
```

或先生成静态库（`.lib`），再链接；这需要 `lib.exe` 打包步骤，此处略。

---

## C 接口（cj_exports.h）

```c
// 打印 Hello, World! 到 stdout；返回 0 表示成功。
int cj_helloworld(void);

// 运行解释器 + 脚本，捕获 stdout 到 outBuf（最多 outBufSize-1，结尾 NUL）。
// 返回：>=0 为复制的字节数；<0 为错误：
//  -1: 创建管道失败（保留，当前实现统一返回 -2）
//  -2: 进程启动/运行失败
//  -3: 参数无效
int cj_helloworld_run(const char* interpreterPath,
                      const char* scriptPath,
                      char* outBuf,
                      int outBufSize);
```

---

## 与仓颉 C 互操作文档的映射

- 头文件 + C ABI：与文档中的 “@C 修饰的函数、foreign 函数使用原生 C ABI” 一致；我们在 C/C++ 侧先定义了稳定的 C ABI 符号。
- 调用约定：Windows 上建议使用 `@CallingConv[CDECL]`（默认即可，显式更清晰），以匹配 C/C++ 调用约定。
- `unsafe` 上下文：仓颉侧调用 C 函数/回调需在 `unsafe { ... }` 内；本示例在 C++ 侧不涉及。
- CType 映射：后续当你导出更复杂签名（指针、@C struct、CFunc 回调）时，对应文档里的 `CPointer<T>`、`@C struct`、`CFunc<...>` 规则。
- inout：对应 C 指针传参；仓颉侧 `inout` 等价传递 `CPointer<T>`。

---

## 替换为真实的“仓颉导出库”

当你能把仓颉函数用 `@C` 导出为 DLL/静态库后：

1. 仓颉侧（示意）：

   ```cangjie
   @CallingConv[CDECL]
   @C
   func cj_helloworld(): Unit {
       println("Hello, World!")
   }
   ```
2. 生产 DLL 或静态库，导出符号 `cj_helloworld`；与 `cj_exports.h` 签名一致。
3. C/C++ 侧保持 `#include "cj_exports.h"` 不变，把链接目标从 `libcangjie_shim.a` 换成你的 DLL/静态库（或运行时用 LoadLibrary/GetProcAddress 解析相同符号名）。
4. 对于需要解释器运行脚本的场景，可继续保留 `cj_helloworld_run`（或在仓颉侧提供等效函数）。

---

## 故障排查（FAQ）

- 链接时报 `undefined reference to 'cj_helloworld' / 'cj_helloworld_run'`：

  - 请先构建并链接 `libcangjie_shim.a`，或把 `cangjie_shim.cpp` 与调用方一并编译进目标文件。
- 运行带解释器参数时报错/无输出：

  - 检查解释器路径与脚本路径是否正确；Windows 下路径建议用引号包裹。
  - 某些解释器不会把输出写入 stdout（或需要额外参数），请根据解释器用法调整。
- 路径包含非 ASCII 字符：

  - 当前使用 ANSI 版 WinAPI，建议后续使用宽字符变体（见改进建议）。

---

## 后续改进建议

- 提供宽字符 API：`int cj_helloworld_run_w(const wchar_t*, const wchar_t*, wchar_t*, int)`。
- 更细化的错误码与进程退出码透传；支持超时/取消。
- 扩充 API 示例：基本类型、@C struct 映射、inout/CPointer、CFunc 回调（C 调用仓颉）。
- 提供 MSVC `.lib` 产物与 CMake 示例工程。
- 真·仓颉导出文档化：如何从仓颉编译 DLL、`@C`/`@CallingConv` 细节、名称导出稳定性、跨平台注意事项。

---

## 参考

- 仓颉语言 “C 语言互操作、unsafe、@C、CFunc、CType、@CallingConv” 文档
- 本仓库源码（`cj_exports.h`, `cangjie_shim.cpp`, `helloworld.cpp`, `call_cj_from_cpp.cpp`）
# 方案二：终端控制终端

>我真得控制你了

# 方案三：