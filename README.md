# APK Shell

企业级 APK 加壳加固系统，提供 DEX 加密、SO 保护、代码混淆、改包名、防报毒、反调试、完整性校验等多层安全防护，有效防止应用被逆向分析、反编译、二次打包、动态调试及应用市场报毒。支持 Android 7.0 - 17，覆盖主流设备。

## 核心防护能力

### DEX 加密保护
对应用的 DEX 文件进行整体加密，运行时在 Native 层动态解密并通过 InMemoryDexClassLoader 加载，全程不落地明文 DEX，防止静态反编译与内存 dump。

### SO 库保护
对 Native 库文件进行自定义格式加密打包，运行时由壳 SO 负责解密并手动链接加载，支持 SO 名称随机化，防止 SO 文件被提取、篡改和逆向分析。

### 字符串加密
对代码中的敏感字符串（API Key、URL、加密密钥等）进行编译期加密，运行时按需解密，防止通过字符串搜索定位关键代码逻辑。

### 代码混淆
基于 OLLVM 的编译器级混淆，支持控制流平坦化、虚假控制流、指令替换、常量替换、字符串混淆等 5 种混淆技术，多层次打乱代码逻辑结构。

### 组件混淆
对 Activity、Service、BroadcastReceiver、ContentProvider 四大组件进行混淆保护，并自动生成大量虚假组件注入 Manifest，干扰逆向分析人员判断。

### 反调试与反篡改
多维度运行时环境检测，包括调试器检测、Root 检测、Xposed/Frida 框架检测、模拟器检测、签名校验、APK 完整性校验，防止动态调试与二次打包。

### VMP 虚拟化保护
将关键 Java/Kotlin 方法的字节码抽取并转换为自定义指令集，运行时由内置虚拟机解释执行。原始字节码从 DEX 中彻底抹除，无法通过 dump 还原，即使脱壳也只能看到空方法体。支持方法级粒度配置，可针对核心业务逻辑（支付、验签、加密等）进行重点保护，兼顾安全性与性能。

### 改包名与防报毒
支持一键修改应用包名、签名信息、资源标识等特征，绕过应用市场和杀毒引擎的特征检测。通过清除已知特征码、随机化类名与资源 ID、修改 Manifest 指纹、剥离调试信息等手段，有效避免 Google Play Protect、各大手机管家及国内应用市场的报毒误报，保障应用正常分发上架。

### 资源保护
对 assets 和 res 目录中的敏感资源文件进行加密，运行时透明解密，防止资源文件被直接提取。

## 功能矩阵

| 功能模块 | 功能项 | 状态 |
|---------|--------|------|
| **DEX 保护** | DEX 整体加密 | ✅ 已实现 |
| | DEX 内存动态加载（不落地） | ✅ 已实现 |
| | 多 DEX 支持 | ✅ 已实现 |
| | DEX VMP 虚拟化保护 | ✅ 已实现 |
| **VMP 防护** | Java/Kotlin 方法字节码抽取 | ✅ 已实现 |
| | 自定义指令集转换 | ✅ 已实现 |
| | 内置虚拟机解释执行 | ✅ 已实现 |
| | 方法级粒度保护配置 | ✅ 已实现 |
| | 原始字节码抹除（防 dump） | ✅ 已实现 |
| **SO 保护** | SO 加密打包 | ✅ 已实现 |
| | SO 动态加载 | ✅ 已实现 |
| | SO 名称随机化 | ✅ 已实现 |
| | SO 节区加密 | ✅ 已实现 |
| | 自定义 ELF Loader | ✅ 已实现 |
| **代码混淆** | 字符串加密 | ✅ 已实现 |
| | 控制流平坦化 | ✅ 已实现 |
| | 虚假控制流 | ✅ 已实现 |
| | 指令替换 | ✅ 已实现 |
| | 常量替换 | ✅ 已实现 |
| | 四大组件混淆 | ✅ 已实现 |
| | 假组件生成 | ✅ 已实现 |
| | Native OLLVM 混淆 | ✅ 已实现 |
| **反调试** | 调试器检测（ptrace / TracerPid） | ✅ 已实现 |
| | Frida 检测 | ✅ 已实现 |
| | Xposed 框架检测 | ✅ 已实现 |
| | Root 环境检测 | ✅ 已实现 |
| | 模拟器检测 | ✅ 已实现 |
| **完整性校验** | APK 签名校验 | ✅ 已实现 |
| | DEX 文件哈希校验 | ✅ 已实现 |
| | SO 文件完整性校验 | ✅ 已实现 |
| **改包名** | 包名一键替换 | ✅ 已实现 |
| | 签名信息修改 | ✅ 已实现 |
| | 资源 ID 随机化 | ✅ 已实现 |
| | Manifest 指纹修改 | ✅ 已实现 |
| **防报毒** | 特征码清除 | ✅ 已实现 |
| | 类名随机化混淆 | ✅ 已实现 |
| | 调试信息剥离 | ✅ 已实现 |
| | Google Play Protect 绕过 | ✅ 已实现 |
| | 国内杀毒引擎免杀 | ✅ 已实现 |
| **资源保护** | Assets 资源加密 | ✅ 已实现 |
| | Res 资源混淆 | ✅ 已实现 |
| **运行环境** | 系统兼容处理（API 24-37） | ✅ 已实现 |
| | Application 替换 | ✅ 已实现 |
| | ContentProvider 兼容 | ✅ 已实现 |
| | 多架构支持（ARMv7/ARM64） | ✅ 已实现 |
| | MultiDex 兼容 | ✅ 已实现 |

## 技术架构

```
┌──────────────────────────────────────────────────────────┐
│               应用层 Application Layer                    │
│          壳 Application · ClassLoader 替换                │
├──────────────────────────────────────────────────────────┤
│           Java/Kotlin 层防护（字节码级别）                  │
│   DEX 加密 · 字符串加密 · 代码混淆 · 组件混淆              │
├──────────────────────────────────────────────────────────┤
│             VMP 虚拟化防护（指令级别）                      │
│  字节码抽取 · 自定义指令集 · 内置 VM 执行 · 原始码抹除      │
├──────────────────────────────────────────────────────────┤
│             Native 层防护（二进制级别）                     │
│    SO 加密 · OLLVM 混淆 · 自定义 ELF Loader · 节区加密     │
├──────────────────────────────────────────────────────────┤
│            改包名与防报毒（分发级别）                        │
│  包名替换 · 特征码清除 · 类名随机化 · 指纹修改 · 免杀处理    │
├──────────────────────────────────────────────────────────┤
│               运行时保护（动态防护）                        │
│   防脱壳 · 反调试 · 反 Hook · 完整性校验 · 环境检测         │
└──────────────────────────────────────────────────────────┘
```

## 技术栈

- **Kotlin** — Gradle 构建脚本 / 自定义 Gradle Plugin / APK 重打包工具链
- **C++ 17** — Native 加壳核心库 / DEX 解密引擎 / 自定义 Linker
- **Dobby** — 轻量级内联 Hook 框架 / SO 加载拦截 / 系统 API Hook
- **OLLVM** — 编译器级混淆 / 5 种混淆技术 / 多级混淆强度可调
- **CMake** — Native 构建系统 / 交叉编译工具链配置
- **Python** — 辅助脚本 / DEX 解析与处理 / 自动化构建流程

## 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/your-repo/apk_shell.git
cd apk_shell
```

### 2. 配置环境

```bash
# 安装 NDK（推荐 r26+）
# 配置 OLLVM 工具链
export ANDROID_NDK_HOME=/path/to/ndk
export OLLVM_HOME=/path/to/ollvm
```

### 3. 加固 APK

```bash
# 基础加固（DEX 加密 + SO 保护）
python3 shell.py --input app-release.apk --output app-protected.apk

# 完整加固（全部防护开启）
python3 shell.py --input app-release.apk --output app-protected.apk \
    --dex-encrypt \
    --so-protect \
    --string-encrypt \
    --ollvm-obfuscate \
    --component-obfuscate \
    --anti-debug \
    --integrity-check \
    --rename-pkg com.new.package.name \
    --anti-virus
```

### 4. 重新签名

```bash
# 使用 apksigner 签名
apksigner sign --ks your-keystore.jks \
    --ks-key-alias your-alias \
    --out app-signed.apk \
    app-protected.apk
```

## 版本兼容

| 项目 | 支持范围 |
|------|---------|
| Android 版本 | 7.0 - 17（API 24 - 37） |
| CPU 架构 | armeabi-v7a / arm64-v8a |
| 编译 SDK | SDK 37（Android 17） |
| NDK 版本 | r26+ |
| Gradle | 8.0+ |

## OLLVM 混淆等级

| 等级 | 混淆技术 | 适用场景 |
|------|---------|---------|
| Level 1 | 字符串加密 | 轻度保护，性能影响最小 |
| Level 2 | 字符串加密 + 指令替换 | 基础保护 |
| Level 3 | Level 2 + 控制流平坦化 | 标准保护，推荐使用 |
| Level 4 | Level 3 + 虚假控制流 | 高强度保护 |
| Level 5 | Level 4 + 常量替换 | 最高强度，性能有一定影响 |

## 项目结构

```
apk_shell/
├── plugin/              # Gradle 加固插件
│   └── shell-plugin/    # 自定义 Gradle Plugin
├── native/              # Native 层核心代码
│   ├── dex_loader/      # DEX 解密与加载引擎
│   ├── so_loader/       # SO 解密与自定义 Linker
│   ├── anti_debug/      # 反调试模块
│   └── integrity/       # 完整性校验模块
├── tools/               # 辅助工具
│   ├── dex_encrypt.py   # DEX 加密工具
│   ├── so_encrypt.py    # SO 加密工具
│   └── manifest_obf.py  # Manifest 混淆工具
├── ollvm/               # OLLVM 混淆配置
├── scripts/             # 构建与签名脚本
└── sample/              # 示例应用
```

## 定制与私有部署

支持根据企业需求进行功能定制与私有化部署：

- **功能定制** — 按需定制加固策略、混淆规则、检测模块，适配特定业务场景
- **私有部署** — 支持内网环境独立部署，数据不出企业，满足安全合规要求
- **专属工具链** — 提供定制化 Gradle 插件与命令行工具，无缝集成 CI/CD 流水线
- **技术支持** — 提供一对一技术对接，协助完成集成与调优

如有定制或私有部署需求，请通过 Telegram 联系。

## 联系方式

- Telegram: [https://t.me/dsfddsxsasd](https://t.me/dsfddsxsasd)

## License

[MIT](LICENSE)
