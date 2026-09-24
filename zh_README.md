## 安装方式：

### 1. 手动方式集成SUDGI SDK

#### 下载 [SUDGI](https://github.com/SUD-GLOBAL/sud-gi-android/releases)

##### SDK: Android-SUDGI-v2.1.0.zip

解压 ZIP 包，将其中的 `SUDGI-v2.1.0.aar`、`SUDCoreKit-v2.1.0.aar` 和 `SUD-report-v2.1.0.aar` 拷贝到项目中，并依赖这些 AAR。同一公共库只需引入一次。

可选扩展按业务需要添加：

| 功能 | AAR 文件 | 所在产物目录 |
| --- | --- | --- |
| 游戏运行时 MP3 编码 | `SUDGI-shine-v2.1.0.aar` | `Android-SUDGI-shine-v2.1.0` |
| AdMob 广告源 | `SUDM-adapter-admob-v2.1.0.aar` | `Android-SUDM-core-v2.1.0` |
| Carty 广告源 | `SUDM-adapter-carty-v2.1.0.aar` | `Android-SUDM-core-v2.1.0` |
| TopOn 广告源 | `SUDM-adapter-topon-v2.1.0.aar` | `Android-SUDM-core-v2.1.0` |

手动集成广告 Adapter 时，还需添加同版本的 `SUDM-core`、`SUDCoreKit`、`SUD-report`，并根据对应 Maven POM 补齐第三方依赖；仅复制 Adapter AAR 不会自动引入其依赖。

### 2. 通过Maven集成SUDGI SDK

以下示例使用 Gradle Groovy DSL（`build.gradle`），SUD 库版本统一为 `2.1.0`。

```groovy
dependencies {
    // SUDGI 与 SUDGI-static 二选一；上架 Google Play 时替换为 SUDGI-static
    api "global.sud.gi:SUDGI:2.1.0"
    // api "global.sud.gi:SUDGI-static:2.1.0"

    // 可选：为游戏运行时提供 MP3 编码能力
    // implementation "global.sud.gi:SUDGI-shine:2.1.0"
}
```

需要接入广告时，在上述 `dependencies` 中按实际业务选择至少一个广告源，无需全部引入：

```groovy
implementation "global.sud.gi:SUDM-adapter-admob:2.1.0"
implementation "global.sud.gi:SUDM-adapter-carty:2.1.0"
implementation "global.sud.gi:SUDM-adapter-topon:2.1.0"
```

Maven 会根据 POM 自动引入依赖：`SUDGI` / `SUDGI-static` 依赖同版本的 `SUDCoreKit` 和 `SUD-report`；广告 Adapter 依赖同版本的 `SUDM-core` 及对应第三方库。广告源所需的仓库、应用标识和初始化配置仍需按对应接入说明完成。

---

## 包体增量说明

> [!NOTE]
> 以下数据来自 2.1.0 产物，AAR 文件大小与 So 解压后大小分别统计，不等于最终 APK 包体增量。单位按 1 MB = 1,000,000 字节、1 KB = 1,000 字节计算。

- 实际 APK 体积增量会受到依赖库、构建配置、代码混淆、资源压缩、So 压缩方式、ABI 配置以及 APK/AAB 打包方式等因素影响。
- 下表中的 AAR 文件大小包含该 AAR 自带的全部 ABI，不包含 Maven 传递依赖。
- 广告 Adapter 自身不包含 So，但其依赖的第三方广告 SDK 可能包含 So、资源和其他依赖，需一并评估。
- 若 APK 仅保留单一 ABI，通常仅会包含对应架构的 So 文件；若同时包含多个 ABI，各架构的 So 文件体积将累计。

### 产物体积概览

| 依赖产物 | AAR 自身是否包含 So | AAR 文件大小 | 说明 |
| --- | :---: | ---: | --- |
| `SUDGI` | 否 | 约 **1.52 MB** | 不含公共库等传递依赖 |
| `SUDGI-static` | 是 | 约 **17.49 MB** | 包含两种 ABI 架构的 So 文件，不含公共库等传递依赖 |
| `SUDGI-shine` | 是 | 约 **83.3 KB** | 可选 MP3 编码扩展，包含四种 ABI 架构的 So 文件 |
| `SUDM-adapter-admob` | 否 | 约 **88.1 KB** | AdMob 适配层，不含 SUDM-core 和第三方广告 SDK |
| `SUDM-adapter-carty` | 否 | 约 **35.5 KB** | Carty 适配层，不含 SUDM-core 和第三方广告 SDK |
| `SUDM-adapter-topon` | 否 | 约 **51.4 KB** | TopOn 适配层，不含 SUDM-core 和第三方广告 SDK |

### 各 ABI So 体积参考

以下为 AAR 中对应 ABI 的全部 So 文件解压后的大小合计。

| 依赖产物 | arm64-v8a | armeabi-v7a | x86 | x86_64 |
| --- | ---: | ---: | ---: | ---: |
| `SUDGI-static` | 约 24.12 MB | 约 14.97 MB | — | — |
| `SUDGI-shine` | 约 39.4 KB | 约 31.6 KB | 约 36.9 KB | 约 39.0 KB |

---

## 系统版本要求

下表为 2.1.0 各 AAR 自身 Manifest 声明的最低版本。实际项目的 `minSdk` 需满足所有已选模块及其传递依赖的要求；与 `SUDGI` / `SUDGI-static` 一起集成时，最低至少为 Android 8.0 (API 26)。

| 依赖产物 | AAR 声明的最低 Android 版本 |
| --- | ---: |
| `global.sud.gi:SUDGI` | Android 8.0 (API 26) |
| `global.sud.gi:SUDGI-static` | Android 8.0 (API 26) |
| `global.sud.gi:SUDGI-shine` | Android 5.0 (API 21) |
| `global.sud.gi:SUDM-adapter-admob` | Android 6.0 (API 23) |
| `global.sud.gi:SUDM-adapter-carty` | Android 5.1 (API 22) |
| `global.sud.gi:SUDM-adapter-topon` | Android 8.0 (API 26) |

---

## 集成Demo

[QuickStart](https://github.com/SudTechnology/Hello-SUD-OpenPaaS-Android)
