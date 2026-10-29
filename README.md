[中文文档](./zh_README.md)

## Installation

### 1. Integrating the SUDGI SDK Manually

#### Download [SUDGI](https://github.com/SUD-GLOBAL/sud-gi-android/releases)

##### SDK: Android-SUDGI-v2.2.0.zip

Extract the ZIP archive, copy `SUDGI-v2.2.0.aar`, `SUDCoreKit-v2.2.0.aar`, and `SUD-report-v2.2.0.aar` into your project, and add them as dependencies. Include each shared library only once.

Add optional extensions as needed:

| Feature | AAR File | Artifact Directory |
| --- | --- | --- |
| MP3 encoding for the game runtime | `SUDGI-shine-v2.2.0.aar` | `Android-SUDGI-shine-v2.2.0` |
| AdMob ad source | `SUDM-adapter-admob-v2.2.0.aar` | `Android-SUDM-core-v2.2.0` |
| Carty ad source | `SUDM-adapter-carty-v2.2.0.aar` | `Android-SUDM-core-v2.2.0` |
| TopOn ad source | `SUDM-adapter-topon-v2.2.0.aar` | `Android-SUDM-core-v2.2.0` |
| MAX ad source | `SUDM-adapter-max-v2.2.0.aar` | `Android-SUDM-core-v2.2.0` |
| Taku ad source | `SUDM-adapter-taku-v2.2.0.aar` | `Android-SUDM-core-v2.2.0` |

When integrating an ad adapter manually, also add `SUDM-core`, `SUDCoreKit`, and `SUD-report` of the same version, along with the third-party SDKs and dependencies specified in the corresponding Maven POM and ad source integration guide. Copying the adapter AAR alone does not automatically include its dependencies.

### 2. Integrating the SUDGI SDK via Maven

The following example uses the Gradle Groovy DSL (`build.gradle`). All SUD libraries use version `2.2.0`.

```groovy
dependencies {
    // Choose either SUDGI or SUDGI-static; use SUDGI-static when publishing on Google Play
    api "global.sud.gi:SUDGI:2.2.0"
    // api "global.sud.gi:SUDGI-static:2.2.0"

    // Optional: provide MP3 encoding for the game runtime
    // implementation "global.sud.gi:SUDGI-shine:2.2.0"
}
```

To integrate ads, add at least one of the following ad sources to the `dependencies` block above, according to your requirements. You do not need to include all of them:

```groovy
implementation "global.sud.gi:SUDM-adapter-admob:2.2.0"
implementation "global.sud.gi:SUDM-adapter-carty:2.2.0"
implementation "global.sud.gi:SUDM-adapter-topon:2.2.0"
implementation "global.sud.gi:SUDM-adapter-max:2.2.0"
implementation "global.sud.gi:SUDM-adapter-taku:2.2.0"
```

Maven automatically includes dependencies based on the POM: `SUDGI` / `SUDGI-static` depends on `SUDCoreKit` and `SUD-report` of the same version; each ad adapter depends on `SUDM-core` of the same version. The AdMob, Carty, TopOn, and MAX adapters also include their platform SDK dependencies automatically. For Taku, configure its platform SDK and repositories according to the [Android integration guide](https://developer.sud.tech/en/openpaas/app/guide/guide-dev/quick-integration/client/android-quick-start.html). You must still configure the repositories, application identifiers, and initialization settings required by each ad source, as described in its integration guide.

---

## App Size Impact

> [!NOTE]
> The figures below are based on version 2.2.0 artifacts. AAR file sizes and uncompressed native shared library (.so) sizes are measured separately and do not represent the final increase in APK size. Units are calculated as 1 MB = 1,000,000 bytes and 1 KB = 1,000 bytes.

- The actual increase in APK size depends on libraries, build configuration, code obfuscation, resource shrinking, native library compression, ABI configuration, and APK/AAB packaging, among other factors.
- The AAR file sizes below include all ABIs bundled in each AAR, but exclude Maven transitive dependencies.
- Ad adapters do not contain native shared libraries themselves. However, their third-party ad SDK dependencies may include native libraries, resources, and other dependencies, which must also be evaluated.
- An APK that retains only one ABI generally includes only the native libraries for that architecture. If multiple ABIs are included, the native library sizes for those architectures add up.

### Artifact Size Overview

| Artifact | Contains Native Shared Libraries | AAR File Size | Notes |
| --- | :---: | ---: | --- |
| `SUDGI` | No | Approx. **1.58 MB** | Excludes transitive dependencies such as shared libraries |
| `SUDGI-static` | Yes | Approx. **34.98 MB** | Includes native libraries for four ABIs; excludes transitive dependencies such as shared libraries |
| `SUDGI-shine` | Yes | Approx. **83.3 KB** | Optional MP3 encoding extension; includes native libraries for four ABIs |
| `SUDM-adapter-admob` | No | Approx. **91.4 KB** | AdMob adapter; excludes SUDM-core and third-party ad SDKs |
| `SUDM-adapter-carty` | No | Approx. **38.5 KB** | Carty adapter; excludes SUDM-core and third-party ad SDKs |
| `SUDM-adapter-topon` | No | Approx. **53.9 KB** | TopOn adapter; excludes SUDM-core and third-party ad SDKs |
| `SUDM-adapter-max` | No | Approx. **51.8 KB** | MAX adapter; excludes SUDM-core and third-party ad SDKs |
| `SUDM-adapter-taku` | No | Approx. **55.5 KB** | Taku adapter; excludes SUDM-core and third-party ad SDKs |

### Native Library Sizes by ABI

The following figures show the total uncompressed size of all native shared libraries for each ABI in the AAR.

| Artifact | arm64-v8a | armeabi-v7a | x86 | x86_64 |
| --- | ---: | ---: | ---: | ---: |
| `SUDGI-static` | Approx. 24.33 MB | Approx. 15.17 MB | Approx. 22.48 MB | Approx. 22.79 MB |
| `SUDGI-shine` | Approx. 39.4 KB | Approx. 31.6 KB | Approx. 36.9 KB | Approx. 39.0 KB |

---

## Android Version Requirements

The table below lists the minimum Android version declared in each version 2.2.0 AAR's own manifest. Your project's `minSdk` must satisfy the requirements of all selected modules and their transitive dependencies. When integrating with `SUDGI` / `SUDGI-static`, the minimum is at least Android 8.0 (API 26).

| Artifact | Minimum Android Version Declared by the AAR |
| --- | ---: |
| `global.sud.gi:SUDGI` | Android 8.0 (API 26) |
| `global.sud.gi:SUDGI-static` | Android 8.0 (API 26) |
| `global.sud.gi:SUDGI-shine` | Android 5.0 (API 21) |
| `global.sud.gi:SUDM-adapter-admob` | Android 6.0 (API 23) |
| `global.sud.gi:SUDM-adapter-carty` | Android 5.1 (API 22) |
| `global.sud.gi:SUDM-adapter-topon` | Android 5.1 (API 22) |
| `global.sud.gi:SUDM-adapter-max` | Android 5.1 (API 22) |
| `global.sud.gi:SUDM-adapter-taku` | Android 5.1 (API 22) |

---

## Integration Demo

[QuickStart](https://github.com/SudTechnology/Hello-SUD-OpenPaaS-Android)

