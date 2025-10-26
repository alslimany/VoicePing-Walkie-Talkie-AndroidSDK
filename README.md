# [VoicePing Walkie Talkie Android SDK](https://github.com/SmartWalkieOrg/VoicePing-Walkie-Talkie-AndroidSDK)

<strong>Need to add walkie talkie or push-to-talk functionality to your Android app?</strong>
<br /><br />
Worry no more! You can add it quickly with VoicePing Android SDK that works together with [VoicePing Open Source Router](#voiceping-router).
<br />
Simple integration, customizable, and free! What are you waiting for? 🎉

<br />  
<center><a href="https://www.voicepingapp.com" target="_blank"><img alt="VoicePing Walkie Talkie Android Free SDK Banner" src="https://i.ibb.co/9pKKf4J/Group-2.png" title="VoicePing Walkie Talkie Android Free SDK Banner" /></a></center>
<br /><br />

VoicePing Android SDK is an Android library, provided by
[Smart Walkie Talkie](http://www.smartwalkie.com), for enabling Push-To-Talk (PTT) functionality to
your Android project. It allows you to quickly add group voice broadcast capability to your app. VoicePing Android SDK comes with a reference Android App (with UI) that demonstrates the one button Push-To-Talk interface.

## 🎉 Now Compatible with Gradle 8.4 and Modern Android Development!

The SDK has been upgraded to support:
- ✅ Gradle 8.4
- ✅ Android Gradle Plugin 8.3.2
- ✅ Kotlin 2.0.0
- ✅ Android SDK 34
- ✅ Java 17

**📖 See [QUICK_START.md](QUICK_START.md) for integration with your modern Android project!**

## Get Started

You can test our sample app here: [Download VP Demo app](https://github.com/SmartWalkieOrg/VoicePingAndroidSDK/releases). The sample app allows you to test the Walkie Talkie function. You will need at least two android devices to test properly.  
You can input any user ID and company name. To communicate, devices should have same company name but different user ID.

## Documentation

- **[Quick Start Guide](QUICK_START.md)** - Integration guide for modern Android projects (Gradle 8.4+, Kotlin 2.0)
- **[Gradle Upgrade Details](GRADLE_UPGRADE.md)** - Complete technical details of the Gradle 8.4 upgrade
- **[VoicePing Documentation](https://opensource.voiceping.info)** - Full SDK documentation
- **[Introduction](https://opensource.voiceping.info/docs/introduction)** - Quick review page

## Features of VoicePing Android SDK (Push-To-Talk)

1. Easy to integrate to your app
2. Low data consumption suitable for Mobile Devices: Opus Codec, defined as 16Khz, 60ms Frame size. ~300KB per 1 minute of speech.
3. Works over all network conditions (2G, 3G, 4G or Wifi)
4. Auto-reconnect feature when Internet connection is lost
5. Uses secure WebSocket for transport
6. Works for Android SDK (21 to 34+) and Android OS version 5.0 to 14+
7. Low battery consumption

## Use Cases (Add Group Walkie Talkie)

1. An Uber like application can connect a group of drivers together based on their location or zipcode
2. For Enterprise applications like housekeeping applications, allow a group call to all housekeepers on a certain floor (level) of the hotel
3. For SOS apps, activate voice broadcast if a user is in distress
4. For Chat Apps, allow some users to send instant voice messages that do not need to be manually played.

## Installation

### Requirements
- Gradle 8.4 or higher
- Android Gradle Plugin 8.3.2 (not 8.4.2 - it doesn't exist!)
- Kotlin 2.0.0
- Java 17
- minSdk 21
- compileSdk 34

### Integration Steps

1. Add jitpack to your `settings.gradle` or `settings.gradle.kts`:

    ```groovy
    dependencyResolutionManagement {
        repositories {
            google()
            mavenCentral()
            maven { url = uri("https://jitpack.io") }
        }
    }
    ```

2. Add the module dependency to your module-level gradle file:

    ```groovy
    dependencies {
        implementation 'com.github.SmartWalkieOrg:VoicePing-Walkie-Talkie-AndroidSDK:1.1'
    }
    ```

3. Sync gradle and use it

**📝 Note**: If you're using a version catalog (`libs.version.toml`), see [QUICK_START.md](QUICK_START.md) for detailed configuration.

**⚠️ Important**: The AGP version should be **8.3.2** (not 8.4.2). AGP versions don't match Gradle versions!

<div name="voiceping-router"></div>

## VoicePing Server
VoicePing Walkie Talkie Android SDK needs a VoicePing Router Server to work. You can test with our hosted server.

The public server URL: `wss://router-lite.voiceping.info`

If you need to self-host the server, you can find more documentation on the server repo:

* [VoicePing Push-To-Talk Server](https://github.com/SmartWalkieOrg/voiceping-router)

## Maintainers

* [VoicePing team](https://www.voicepingapp.com/)

## VoicePing Enterprise

VoicePing Enterprise is the full featured closed source version with support. More features available are [https://www.voicepingapp.com](https://www.voicepingapp.com). You can try VoicePing on:

* [VoicePing Web](https://web.voiceoverping.net/)
* [VoicePing Android](https://play.google.com/store/apps/details?id=com.media2359.voiceping.store)
* [VoicePing iOS](https://itunes.apple.com/us/app/voiceping/id1249953303?ls=1&mt=8)

Join the same free channel ID and try PTT from the web to the Android/iOS app and vice versa. You will find VoicePing has very clear audio and low latency<sup>1</sup>.

VoicePing Enterprise has more features than VoicePing Open Source which can be found here: https://www.voicepingapp.com/blog/design-a-stunning-blog


### Multi Platform Support

**[Android Supported](https://play.google.com/store/apps/details?id=com.media2359.voiceping.store):** Android 5 to Android 14+ supported. With or Without Google Services.

**[iPhone Supported](https://itunes.apple.com/us/app/voiceping/id1249953303?ls=1&mt=8):** iPhone version available. Runs in Background to allow for Real Time receiving of PTT.

**[Desktop Version](https://www.voicepingapp.com/blog/voiceping-desktop-web-ptt):** Web Based version to connect office and field workers.


## Consulting/Partnership, Services & Pricing  

If you would like help on server setup, maintenance, customization, please contact us at sales@smartwalkietalkie.com. VoicePing Enterprise is also available for customisation, rebranding and source code purchase. 

## Footnote

[1] Latency: time between someone talks in a device until the other hears the audio on other device
