## 安装方式：
### 1. 手动方式集成SUDGI SDK
#### 下载 [SUDGI](https://github.com/SUD-GLOBAL/sud-gi-android/releases)
##### SDK: Android-SUDGI-v2.0.0.1301.zip
##### 解压zip包拿到解压后的aar包，将aar包拷贝到项目中，并且在项目中依赖该aar包

### 2. 通过Maven集成SUDGI SDK
```ruby
// 上架Google Play需要替换成此依赖：api 'global.sud.gi:SUDGI-static:2.0.0.1301'
api 'global.sud.gi:SUDGI:2.0.0.1301'

```
---

## 包体增量说明

> [!NOTE]
> 以下体积数据均为近似值，用于依赖选型和 APK 包体评估。

- 实际 APK 体积增量会受到构建配置、代码混淆、资源压缩、So 压缩方式、ABI 配置以及 APK/AAB 打包方式等因素影响。
- 下表中的“近似总体积/增量”指包含全部 ABI 架构时的估算值，不代表单一 ABI APK 的最终体积。
- 若 APK 仅保留单一 ABI，通常仅会包含对应架构的 So 文件，实际包体增量会相应减少。
- 若 APK 同时包含多个 ABI，各架构的 So 文件会同时打入 APK，相关体积将累计。
- 以下依赖名称未携带具体版本号，实际接入时请使用对应版本号。

### 产物体积概览

| 依赖产物 | 是否包含 So | 近似总体积 / 增量 | 说明 |
| --- | :---: | ---: | --- |
| `SUDGI` | 否 | 约 **1.3 MB** | 推荐使用，APK 包体增量较小 |
| `SUDGI-static` | 是 | 约 **16.3 MB** | 包含两种 ABI 架构的 So 文件 |

### 各 ABI So 体积参考

| 依赖产物 | arm64-v8a | armeabi-v7a |
| --- | ---: | ---: |
| `SUDGI-static` | 约 8 MB | 约 6.7 MB |

---

## 系统版本要求

不同 SDK 产物对 Android 系统最低版本要求不同，请在项目中配置对应的 `minSdk`。

| 依赖产物 | 最低 Android 版本 |
| --- | ---: |
| `global.sud.gi:SUDGI` | Android 8.0 (API 26) |
| `global.sud.gi:SUDGI-static` | Android 8.0 (API 26) |

---

## 集成Demo
[QuickStart](https://github.com/SudTechnology/Hello-SUD-OpenPaaS-Android)
