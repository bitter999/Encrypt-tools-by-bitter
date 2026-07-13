# Encrypt-Tool (Cybersecurity Learning Project)

这是一个用于网络安全学习与测试的轻量级文件加密/解密工具。本仓库**仅提供编译完成的二进制可执行程序**，不开放源代码。

## 📁 目录文件说明

*   `encrypt-bitter.exe` : 适用于 Windows 系统的可执行程序。
*   `tools` : 适用于 Linux 系统的可执行程序（基于 ELF 架构，图中编译名为 `tools`）。

---

## 🚀 如何使用 (Usage)

本工具为命令行（CLI）交互工具，请通过终端或命令提示符运行。

### 💻 Windows 系统运行方法

1. 按下 `Win + R` 键，输入 `cmd` 或 `powershell` 打开终端。
2. 使用 `cd` 命令切换到工具所在的目录：
   ```cmd
   比如cd D:\Desktop\admin\learning-cyber\learning-c
   ```
3. 输入程序名称并回车运行：
   ```powershell
   .\encrypt-bitter.exe
   ```
4. 根据屏幕上的提示，输入你需要加密/解密的文件路径。
   * *示例输入*：`D:\test\flag.txt`

### 🐧 Linux (以 Kali Linux 为例) 系统运行与实战步骤

在 Linux 系统下，工具不仅支持普通的文本加密，还支持图片、音乐、视频甚至可执行程序等任意文件类型的二进制层加密。以下是完整的操作指南与执行效果流程：

#### 1. 准备测试文件
在终端中或通过文本编辑器创建一个用于测试的明文文件（例如 `av.txt`），写入需要保护的私密内容。
* *示例文件内容*：

  ![明文内容样例]<img width="2536" height="392" alt="2" src="https://github.com/user-attachments/assets/61061bc1-109c-4a67-bf3e-b7806eee4c8c" />



#### 2. 编译或确认可执行程序
若获取了源码可使用 `gcc encrypt-new.c -o tools` 编译生成名为 `tools` 的程序，并通过 `ls` 命令确认程序已成功存在于当前目录。
* *示例文件内容*：

  ![明文内容样例]<img width="2842" height="362" alt="1" src="https://github.com/user-attachments/assets/3c1c6add-e2d8-4e87-8a2e-e05f9da4412e" />

* *编译与列表查看*：
#### 3. 运行程序并执行文件加密
在运行前，请确保文件拥有可执行权限（`chmod +x tools`）。接着执行 `./tools` 启动程序：
1. 第一次输入一个不存在的路径时，程序会贴心提示 `文件不存在或无法打开`。
2. 重新运行程序，输入正确的绝对路径（如 `/root/av.txt`），程序识别成功后会提示：`文件存在。你好请你输入密码，如:123456`。
3. 输入您的自定义密码（例如 `123456`），终端打印 `恭喜你加密或解密成功`。
* *加密运行过程*：

  ![加密操作流程](<img width="1346" height="898" alt="3" src="https://github.com/user-attachments/assets/1de6422f-0b20-4736-bd59-20e95384c9aa" />

)

#### 4. 查看加密后的密文效果
文件加密成功后，原有的明文数据在底层已被彻底打乱。
* **通过终端查看**：使用 `cat av.txt` 命令，终端将输出一连串无法解析的乱码。

  ![终端密文乱码](<img width="2863" height="1038" alt="4" src="https://github.com/user-attachments/assets/39742756-e540-4e2c-b1e5-0780f20cdd73" />

)
* **通过文本编辑器查看**：使用 Mousepad 等编辑器打开该文件，内容已变成完全无法阅读的十六进制与特殊乱码字符。

  ![编辑器密文乱码](<img width="1804" height="998" alt="5" src="https://github.com/user-attachments/assets/0f7c7cb0-14fc-4582-a5a7-e924cc132a8b" />

)

#### 5. 再次运行程序执行解密还原
当需要恢复原文件时，**再次运行相同的加密程序**（`./tools`），输入相同的文件路径（`/root/av.txt`）以及**完全一致的密码**（`123456`）。
* 解密成功后，再次使用 `cat av.txt` 查看，可以看到文件内容已被完美还原，明文信息完好无损。
* *解密还原流程*：
  ![解密还原流程](<img width="2603" height="999" alt="6" src="https://github.com/user-attachments/assets/c0695de6-ef6d-4511-aa2d-3c84f2dc7f0c" />
)

---

## ❓ 常见问题与坑点 (FAQ)

### 🚨 为什么在 Windows 终端打开程序，显示的是“瀹夂芰...璇疯糹”等奇怪的乱码？

**原因解释**：这是 Windows 系统的经典文本编码不匹配现象。本程序的中文提示采用的是国际通用的 **UTF-8** 编码，而部分 Windows 系统的 CMD 或 PowerShell 终端默认使用的是老旧的 **GBK (代码页 936)** 编码。当终端用 GBK 去硬套解密 UTF-8 的中文字符时，就会产生这种生僻字乱码。

**三种解决方案（任选其一即可）：**

#### 💡 方案一：在终端输入修复命令（最快）
在运行 `.\encrypt-bitter.exe` 之前，在你的 PowerShell 或 CMD 窗口中先输入以下命令并回车，将终端临时切换为 UTF-8 编码模式：
```powershell
chcp 65001
```
执行后终端可能会闪烁一下，此时重新输入 `.\encrypt-bitter.exe` 运行，中文即可恢复正常。

#### 💡 方案二：使用 VS Code 内置终端运行
VS Code 自带的集成终端（Terminal）对 UTF-8 编码的兼容性极好。直接在 VS Code 底部终端中输入命令运行，通常不会出现任何乱码。

#### 💡 方案三：【开发小贴士】在代码层彻底根治
虽然本工具不开放源码，但如果你在独立开发类似的 C/C++ 命令行工具，可以在主函数 `main()` 的开头引入 `<windows.h>` 头文件，并添加以下两行代码。这样今后编译出来的程序在任何 Windows 环境下双击运行都不会再有乱码：
```c
#include <windows.h>

int main() {
    SetConsoleOutputCP(65001); // 强制输出 UTF-8
    SetConsoleCP(65001);       // 强制输入 UTF-8
    // ... 原有代码 ...
}
```

---

## ⚠️ 免责声明 (Disclaimer)

* 本工具仅用于网络安全教学、C语言实践以及个人技术研究。
* 请勿将本工具用于任何非法加密、勒索或破坏他人计算机系统的行为。
* 由使用本工具造成的任何直接或间接损失，由使用者自行承担，作者不承担任何法律责任。
---

## ⚠️ 免责声明 (Disclaimer)

* 本工具仅用于网络安全教学、C语言实践以及个人技术研究。
* 请勿将本工具用于任何非法加密、勒索或破坏他人计算机系统的行为。
* 由使用本工具造成的任何直接或间接损失，由使用者自行承担，作者不承担任何法律责任。
