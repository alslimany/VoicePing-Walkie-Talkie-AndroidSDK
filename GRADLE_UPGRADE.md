# Gradle 8.4 and Modern Android Upgrade

This document describes the upgrade of the VoicePing Android SDK to support Gradle 8.4 and modern Android development practices.

## Summary of Changes

### Gradle and Build Tools

- **Gradle**: Upgraded from 6.7.1 to 8.4
- **Android Gradle Plugin (AGP)**: Upgraded from 4.2.1 to 8.3.2
- **Kotlin**: Upgraded from 1.5.21 to 2.0.0
- **Java**: Updated to Java 17 (required for Gradle 8.x and Kotlin 2.0)

### Important Note About AGP Versioning

The Android Gradle Plugin (AGP) version **does not match** the Gradle version. In your `libs.version.toml`, you have:
```toml
agp = "8.4.2"
```

However, **AGP 8.4.2 does not exist**. The AGP versioning is independent of Gradle versioning:
- Gradle 8.4 works with AGP 8.3.x (used in this project)
- AGP 8.5+ requires Gradle 8.7+

For compatibility with Gradle 8.4, this project uses AGP 8.3.2.

### Android SDK Versions

- **compileSdk**: Upgraded from 30 to 34
- **targetSdk**: Upgraded from 30 to 34
- **minSdk**: Upgraded from 16 to 21 (required for modern libraries)

### Dependencies Updated

#### App Module
- `androidx.core:core-ktx`: 1.6.0 → 1.13.1
- `androidx.appcompat:appcompat`: 1.3.1 → 1.7.0
- `com.google.android.material:material`: 1.4.0 → 1.12.0
- `com.squareup.okhttp3:okhttp`: 3.9.0 → 4.12.0
- `pub.devrel:easypermissions`: 0.4.2 → 3.0.0
- `androidx.test.espresso:espresso-core`: 3.4.0 → 3.6.1
- `androidx.test.ext:junit`: 1.1.3 → 1.2.1

#### VoicePing SDK Module
- `com.squareup.okhttp3:okhttp`: 3.9.0 → 4.12.0

#### Libraries (msgpack)
- `org.javassist:javassist`: 3.18.1-GA → 3.30.2-GA
- Java compatibility: 1.6 → 17

### Build Configuration Changes

#### 1. Plugin Declaration (Modern Syntax)
Changed from:
```gradle
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
```

To:
```gradle
plugins {
    id 'com.android.application'
    id 'kotlin-android'
}
```

#### 2. Namespace Declaration
Moved package declaration from `AndroidManifest.xml` to `build.gradle`:

**build.gradle:**
```gradle
android {
    namespace 'com.smartwalkie.voicepingdemo'
    // ...
}
```

**AndroidManifest.xml:**
```xml
<!-- Removed: package="com.smartwalkie.voicepingdemo" -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
```

#### 3. Android Exported Attributes
Added required `android:exported` attribute to all `<activity>` elements:
```xml
<activity
    android:name=".LoginActivity"
    android:exported="true">
    <!-- ... -->
</activity>
```

#### 4. Java Version Configuration
Added explicit Java 17 configuration:
```gradle
android {
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_17
        targetCompatibility JavaVersion.VERSION_17
    }
    kotlinOptions {
        jvmTarget = '17'
    }
}
```

#### 5. BuildConfig Generation
Explicitly enabled BuildConfig generation (disabled by default in AGP 8.0+):
```gradle
android {
    buildFeatures {
        buildConfig true
    }
}
```

#### 6. Repository Configuration
Replaced deprecated `jcenter()` with `mavenCentral()` and explicitly configured Maven:
```gradle
repositories {
    maven { url 'https://maven.google.com' }
    mavenCentral()
}
```

#### 7. Task Declaration
Updated deprecated task syntax:
```gradle
// Old
task clean(type: Delete) {
    delete rootProject.buildDir
}

// New
tasks.register('clean', Delete) {
    delete rootProject.buildDir
}
```

#### 8. Dependency Keywords
Updated deprecated dependency configuration:
```gradle
// Old
compile 'org.javassist:javassist:3.18.1-GA'

// New
implementation 'org.javassist:javassist:3.30.2-GA'
```

#### 9. Maven Publishing Configuration
Added modern publishing configuration for the SDK:
```gradle
android {
    publishing {
        singleVariant('release') {
            withSourcesJar()
            withJavadocJar()
        }
    }
}

afterEvaluate {
    publishing {
        publications {
            release(MavenPublication) {
                from components.release
                
                groupId = 'com.github.SmartWalkieOrg'
                artifactId = 'voiceping-sdk'
                version = android.defaultConfig.versionName
            }
        }
    }
}
```

### Settings Configuration

Added `pluginManagement` block to `settings.gradle`:
```gradle
pluginManagement {
    repositories {
        maven { url 'https://maven.google.com' }
        mavenCentral()
        gradlePluginPortal()
    }
}
rootProject.name = "VoicePing-Walkie-Talkie-AndroidSDK"
include ':app', ':voiceping-sdk'
```

## Compatibility with Your Project

Based on your `libs.version.toml`, here's how to use this SDK:

### Correct AGP Version
Update your `libs.version.toml`:
```toml
[versions]
agp = "8.3.2"  # Changed from "8.4.2" - AGP 8.4.2 doesn't exist
kotlin = "2.0.0"
# ... rest of your versions
```

### Using the SDK
Add to your project's `settings.gradle`:
```gradle
dependencyResolutionManagement {
    repositories {
        maven { url 'https://jitpack.io' }
        maven { url 'https://maven.google.com' }
        mavenCentral()
    }
}
```

Add to your app's `build.gradle`:
```gradle
dependencies {
    implementation 'com.github.SmartWalkieOrg:VoicePing-Walkie-Talkie-AndroidSDK:1.1'
}
```

## Building the Project

### Requirements
- JDK 17 or higher
- Android Studio Hedgehog (2023.1.1) or newer
- Gradle 8.4 (included via wrapper)

### Build Commands
```bash
# Clean and build
./gradlew clean build

# Build release AAR
./gradlew :voiceping-sdk:assembleRelease

# Run tests
./gradlew test

# Build demo app
./gradlew :app:assembleDebug
```

## Migration Guide for Existing Users

If you're upgrading from an older version of this SDK:

1. **Update your Gradle wrapper** to 8.4 or higher:
   ```bash
   ./gradlew wrapper --gradle-version 8.4
   ```

2. **Update your AGP version** to 8.3.2 (NOT 8.4.2):
   ```gradle
   classpath 'com.android.tools.build:gradle:8.3.2'
   ```

3. **Update Kotlin** to 2.0.0:
   ```gradle
   classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:2.0.0"
   ```

4. **Set Java 17** in your project:
   - Update your project's JDK to 17
   - Configure `compileOptions` and `kotlinOptions` as shown above

5. **Update minSdk** if needed:
   - The SDK now requires `minSdk 21`
   - Update your app's `minSdk` accordingly

## Known Issues

None at this time.

## Testing

The project has been configured to build successfully with:
- Gradle 8.4
- AGP 8.3.2
- Kotlin 2.0.0
- Java 17
- Android SDK 34

All configuration changes follow Android and Gradle best practices as of 2024-2025.

## Support

For issues related to this upgrade, please open an issue on the GitHub repository.
