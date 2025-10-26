# Quick Start: Using VoicePing SDK with Your Project

This guide helps you integrate the upgraded VoicePing SDK into your Android project.

## Important: AGP Version Clarification

Your `libs.version.toml` shows:
```toml
agp = "8.4.2"
```

**This version does not exist.** You need to update it to:
```toml
agp = "8.3.2"
```

Android Gradle Plugin (AGP) versions are independent of Gradle versions:
- ✅ Gradle 8.4 + AGP 8.3.2 = Compatible
- ❌ AGP 8.4.2 = Does not exist
- AGP 8.5+ requires Gradle 8.7+

## Updated libs.version.toml

Update your `libs.version.toml` file:

```toml
[versions]
agp = "8.3.2"              # Changed from "8.4.2"
kotlin = "2.0.0"           # Compatible
coreKtx = "1.17.0"         # Compatible
junit = "4.13.2"           # Compatible
junitVersion = "1.3.0"     # Compatible
espressoCore = "3.7.0"     # Compatible
lifecycleRuntimeKtx = "2.9.4"  # Compatible
activityCompose = "1.11.0"     # Compatible
composeBom = "2024.09.00"      # Compatible
retrofit = "2.9.0"             # Compatible
okhttp = "4.12.0"              # Compatible ✅ (SDK uses this)
room = "2.6.1"                 # Compatible
lifecycleViewmodel = "2.9.4"   # Compatible
navigationCompose = "2.8.0"    # Compatible
hilt = "2.51"                  # Compatible
hiltNavigationCompose = "1.2.0"  # Compatible
playServicesLocation = "21.3.0"  # Compatible
accompanistPermissions = "0.34.0"  # Compatible
voicepingSdk = "1.1"           # Use this version

[libraries]
androidx-core-ktx = { group = "androidx.core", name = "core-ktx", version.ref = "coreKtx" }
junit = { group = "junit", name = "junit", version.ref = "junit" }
androidx-junit = { group = "androidx.test.ext", name = "junit", version.ref = "junitVersion" }
androidx-espresso-core = { group = "androidx.test.espresso", name = "espresso-core", version.ref = "espressoCore" }
androidx-lifecycle-runtime-ktx = { group = "androidx.lifecycle", name = "lifecycle-runtime-ktx", version.ref = "lifecycleRuntimeKtx" }
androidx-lifecycle-viewmodel-ktx = { group = "androidx.lifecycle", name = "lifecycle-viewmodel-ktx", version.ref = "lifecycleViewmodel" }
androidx-lifecycle-viewmodel-compose = { group = "androidx.lifecycle", name = "lifecycle-viewmodel-compose", version.ref = "lifecycleViewmodel" }
androidx-activity-compose = { group = "androidx.activity", name = "activity-compose", version.ref = "activityCompose" }
androidx-compose-bom = { group = "androidx.compose", name = "compose-bom", version.ref = "composeBom" }
androidx-ui = { group = "androidx.compose.ui", name = "ui" }
androidx-ui-graphics = { group = "androidx.compose.ui", name = "ui-graphics" }
androidx-ui-tooling = { group = "androidx.compose.ui", name = "ui-tooling" }
androidx-ui-tooling-preview = { group = "androidx.compose.ui", name = "ui-tooling-preview" }
androidx-ui-test-manifest = { group = "androidx.compose.ui", name = "ui-test-manifest" }
androidx-ui-test-junit4 = { group = "androidx.compose.ui", name = "ui-test-junit4" }
androidx-material3 = { group = "androidx.compose.material3", name = "material3" }
androidx-navigation-compose = { group = "androidx.navigation", name = "navigation-compose", version.ref = "navigationCompose" }
androidx-room-runtime = { group = "androidx.room", name = "room-runtime", version.ref = "room" }
androidx-room-ktx = { group = "androidx.room", name = "room-ktx", version.ref = "room" }
androidx-room-compiler = { group = "androidx.room", name = "room-compiler", version.ref = "room" }
retrofit = { group = "com.squareup.retrofit2", name = "retrofit", version.ref = "retrofit" }
retrofit-gson = { group = "com.squareup.retrofit2", name = "converter-gson", version.ref = "retrofit" }
okhttp = { group = "com.squareup.okhttp3", name = "okhttp", version.ref = "okhttp" }
okhttp-logging = { group = "com.squareup.okhttp3", name = "logging-interceptor", version.ref = "okhttp" }
hilt-android = { group = "com.google.dagger", name = "hilt-android", version.ref = "hilt" }
hilt-compiler = { group = "com.google.dagger", name = "hilt-compiler", version.ref = "hilt" }
hilt-navigation-compose = { group = "androidx.hilt", name = "hilt-navigation-compose", version.ref = "hiltNavigationCompose" }
play-services-location = { group = "com.google.android.gms", name = "play-services-location", version.ref = "playServicesLocation" }
accompanist-permissions = { group = "com.google.accompanist", name = "accompanist-permissions", version.ref = "accompanistPermissions" }
voiceping-sdk = { group = "com.github.SmartWalkieOrg", name = "VoicePing-Walkie-Talkie-AndroidSDK", version.ref = "voicepingSdk" }

[plugins]
android-application = { id = "com.android.application", version.ref = "agp" }
kotlin-android = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }
kotlin-compose = { id = "org.jetbrains.kotlin.plugin.compose", version.ref = "kotlin" }
kotlin-kapt = { id = "org.jetbrains.kotlin.kapt", version.ref = "kotlin" }
hilt-android = { id = "com.google.dagger.hilt.android", version.ref = "hilt" }
```

## Integration Steps

### 1. Update Your Project's Build Configuration

**settings.gradle.kts** or **settings.gradle**:
```groovy
pluginManagement {
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url = uri("https://jitpack.io") }  // Required for VoicePing SDK
    }
}

rootProject.name = "YourProjectName"
include(":app")
```

### 2. Add the VoicePing SDK Dependency

**app/build.gradle.kts** or **app/build.gradle**:
```groovy
dependencies {
    // Your other dependencies from libs.version.toml
    implementation(libs.voiceping.sdk)
    
    // Or directly:
    // implementation("com.github.SmartWalkieOrg:VoicePing-Walkie-Talkie-AndroidSDK:1.1")
}
```

### 3. SDK Requirements

Your app needs to meet these minimum requirements to use the VoicePing SDK:

```groovy
android {
    compileSdk = 34  // Or higher
    
    defaultConfig {
        minSdk = 21       // SDK requires minimum API 21
        targetSdk = 34    // Or higher
    }
    
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }
    
    kotlinOptions {
        jvmTarget = "17"
    }
}
```

### 4. Required Permissions

Add these permissions to your **AndroidManifest.xml**:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

### 5. Gradle Wrapper

Ensure your project uses Gradle 8.4 or higher:
```bash
./gradlew wrapper --gradle-version 8.4
```

## Compatibility Matrix

| Component | Your Project | VoicePing SDK | Compatible? |
|-----------|--------------|---------------|-------------|
| Gradle | 8.4+ | 8.4 | ✅ |
| AGP | 8.3.2 (not 8.4.2) | 8.3.2 | ✅ |
| Kotlin | 2.0.0 | 2.0.0 | ✅ |
| Java | 17+ | 17 | ✅ |
| compileSdk | 34+ | 34 | ✅ |
| minSdk | 21+ | 21 | ✅ |
| OkHttp | 4.12.0 | 4.12.0 | ✅ |

## Build Commands

```bash
# Sync Gradle
./gradlew --refresh-dependencies

# Clean and build
./gradlew clean build

# Run app
./gradlew installDebug
```

## Troubleshooting

### Issue: "Could not resolve com.github.SmartWalkieOrg:VoicePing-Walkie-Talkie-AndroidSDK"

**Solution**: Ensure JitPack repository is added to `settings.gradle`:
```groovy
repositories {
    maven { url = uri("https://jitpack.io") }
}
```

### Issue: "Unsupported class file major version"

**Solution**: Update your JDK to version 17 or higher. In Android Studio:
- File → Project Structure → SDK Location → Gradle Settings → Gradle JDK → 17

### Issue: AGP version 8.4.2 not found

**Solution**: Update `libs.version.toml`:
```toml
agp = "8.3.2"  # AGP 8.4.2 doesn't exist
```

### Issue: "Minimum SDK version is lower than SDK requirement"

**Solution**: Update your app's `minSdk` to 21 or higher:
```groovy
defaultConfig {
    minSdk = 21
}
```

## Example Usage

```kotlin
import com.smartwalkie.voicepingsdk.VoicePing

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        // Initialize VoicePing SDK
        // (Refer to SDK documentation for specific API usage)
    }
}
```

## Support

- **SDK Repository**: https://github.com/SmartWalkieOrg/VoicePing-Walkie-Talkie-AndroidSDK
- **Documentation**: See [GRADLE_UPGRADE.md](GRADLE_UPGRADE.md) for detailed upgrade information
- **Issues**: Report issues on the GitHub repository

## Summary

**Key Changes Required**:
1. ✅ Update AGP version from "8.4.2" to "8.3.2" in your `libs.version.toml`
2. ✅ Ensure Gradle 8.4 or higher
3. ✅ Ensure Java 17 or higher
4. ✅ Add JitPack repository
5. ✅ Ensure minSdk 21 or higher

After these changes, the VoicePing SDK will integrate seamlessly with your project!
