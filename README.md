[中文文档](./zh_README.md)

## Installation

### 1. Manually Integrate the SUDGI SDK

##### SDK: Android-SUDGI-v2.0.0.1301.zip

Extract the ZIP package to obtain the AAR file, copy the AAR file into your project, and add it as a dependency in your project.

### 2. Integrate the SUDGI SDK via Maven

```ruby
// For apps published on Google Play, use the following dependency instead:
// api 'global.sud.gi:SUDGI-static:2.0.0.1301'

api 'global.sud.gi:SUDGI:2.0.0.1301'
```

---

## Package Size Increase

> [!NOTE]
> The size values below are approximate and are intended for dependency selection and APK size estimation.

- The actual APK size increase may vary depending on build configuration, code obfuscation, resource shrinking, native library compression, ABI configuration, and whether the app is packaged as an APK or AAB.
- The "Approximate Total Size / Increase" values in the table below are estimates when all supported ABIs are included. They do not represent the final size of an APK containing only a single ABI.
- If the APK includes only one ABI, it will typically contain only the native `.so` files for that architecture, and the actual package size increase will be reduced accordingly.
- If the APK includes multiple ABIs, the `.so` files for all included architectures will be packaged into the APK, and their sizes will be cumulative.
- The dependency names below do not include specific version numbers. Please use the corresponding version number when integrating the SDK.

### Artifact Size Overview

| Dependency | Includes `.so` Files | Approximate Total Size / Increase | Description |
| --- | :---: | ---: | --- |
| `SUDGI` | No | Approx. **1.3 MB** | Recommended. Adds less to the APK size. |
| `SUDGI-static` | Yes | Approx. **16.3 MB** | Includes `.so` files for two ABI architectures. |

### `.so` Size by ABI

| Dependency | arm64-v8a | armeabi-v7a |
| --- | ---: | ---: |
| `SUDGI-static` | Approx. 8 MB | Approx. 6.7 MB |

---

## Android Version Requirements

Different SDK artifacts have different minimum Android version requirements. Configure the corresponding `minSdk` value in your project.

| Dependency | Minimum Android Version |
| --- | ---: |
| `global.sud.gi:SUDGI` | Android 8.0 (API 26) |
| `global.sud.gi:SUDGI-static` | Android 8.0 (API 26) |

---

## Integration Demo

[QuickStart](https://github.com/SudTechnology/Hello-SUD-OpenPaaS-Android)
