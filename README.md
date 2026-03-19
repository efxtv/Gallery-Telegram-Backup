# Gallery Telegram Backup

A powerful Android gallery app that displays your photos beautifully while optionally backing them up to Telegram in the background.

[![Platform](https://img.shields.io/badge/Android-11--15-3DDC84?logo=android)](https://www.android.com)
[![API](https://img.shields.io/badge/API-30--35-4caf50)](https://developer.android.com/studio/releases/platforms)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-17-007396?logo=java)](https://www.java.com)
[![Telegram](https://img.shields.io/badge/Telegram-Bot-26A5E4?logo=telegram)](https://t.me/errorfix_tv)
[![Build](https://img.shields.io/badge/build-passing-brightgreen)](https://github.com/)

---

## ✨ Features

### 🖼️ Gallery Core
- **Grid View** - All images displayed in a clean 3-column grid
- **Fast Scrolling** - Smooth performance even with thousands of images
- **Image Loading** - Powered by Glide for optimal memory usage
- **Date Sorting** - Newest images appear first
- **Thumbnail Caching** - Faster loading on subsequent opens

### 👆 Fullscreen Experience
- **Tap to View** - Click any image for immersive viewing
- **Swipe Navigation** - Left/right to browse through photos
- **Image Counter** - Current position indicator (e.g., "5 / 25")
- **Pinch to Zoom** - Zoom in/out on images
- **Easy Exit** - Back button or system back to return

### 📤 Telegram Integration (Optional)
- **Auto Backup** - Automatically sends images to your Telegram bot
- **Background Service** - Runs without interrupting user experience
- **Configurable** - Easy setup with `./changeme.sh` script
- **Notification** - Shows sync progress in status bar
- **Batch Sending** - Optimized for multiple images
- **Retry Logic** - Handles network failures gracefully

### 🔒 Privacy & Security
- **Opt-in Only** - Telegram sync disabled by default
- **No Hidden Data** - Clear what gets sent where
- **Permission Aware** - Requests only necessary permissions
- **Android 15 Ready** - Full support for latest privacy features
- **Open Source** - Full transparency in code
- **No Analytics** - Zero tracking or data collection

---

## 📋 Requirements

### Development Environment
| Requirement | Version |
|-------------|---------|
| Java Development Kit | 17 or higher |
| Android SDK | API level 35 |
| Gradle | 8.0+ (wrapper included) |
| Android Studio | Ladybug+ (2024.1+) |
| Minimum SDK | 30 (Android 11) |
| Target SDK | 35 (Android 15) |

### Target Devices
| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| Android OS | 11.0 (API 30) | 15.0 (API 35) |
| RAM | 2GB | 4GB+ |
| Storage | 50MB | 100MB |
| Internet | Optional | Required for Telegram |
| Permissions | Storage | Storage + Internet |

---

## 🚀 Quick Start Guide

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/gallery-telegram-backup.git
cd gallery-telegram-backup
```

### 2. Set Up Telegram Bot (Optional)

#### Create Bot:
1. Open Telegram and search for [@BotFather](https://t.me/botfather)
2. Send `/newbot` command
3. Choose a name (e.g., `My Gallery Bot`)
4. Choose a username (must end with 'bot', e.g., `my_gallery_bot`)
5. Copy the bot token (format: `123456789:ABCdefGHIjklMNOpqrsTUVwxyz`)

#### Get Chat ID:
1. Start a chat with your new bot
2. Send any message (e.g., "Hello")
3. Visit this URL in browser:
   ```
   https://api.telegram.org/bot<YOUR_BOT_TOKEN>/getUpdates
   ```
4. Find your chat ID in the response: `{"chat":{"id":123456789,...}}`

### 3. Configure Telegram Credentials

```bash
# Make script executable
chmod +x changeme.sh

# Add your credentials
./changeme.sh "YOUR_BOT_TOKEN" "YOUR_CHAT_ID"

# To disable Telegram (restore defaults)
./changeme.sh restore
```

### 4. Build the App

```bash
# Make gradlew executable
chmod +x gradlew

# Check Java version (must be 17+)
java -version

# Clean build (recommended for first time)
./gradlew clean

# Build debug APK
./gradlew assembleDebug

# For faster build (skip tests)
./gradlew assembleDebug -x test

# Build release APK (requires signing)
./gradlew assembleRelease
```

### 5. Install on Device

#### Using ADB (USB debugging enabled):
```bash
# List connected devices
adb devices

# Install APK
adb install -r app/build/outputs/apk/debug/app-debug.apk

# Or install directly via gradle
./gradlew installDebug
```

#### Manual Installation:
1. Find APK at: `app/build/outputs/apk/debug/app-debug.apk`
2. Transfer to your Android device
3. Open file manager and tap the APK
4. Allow installation from unknown sources if prompted

---

## 📁 Project Structure

```
gallery-telegram-backup/
├── app/
│   ├── src/main/
│   │   ├── java/com/androide/galer/
│   │   │   ├── MainActivity.java           # Grid view with permissions
│   │   │   ├── ImageAdapter.java           # Image display and click handling
│   │   │   ├── FullscreenActivity.java     # Fullscreen viewer with ViewPager2
│   │   │   ├── FullscreenPagerAdapter.java # ViewPager2 adapter
│   │   │   └── TelegramService.java        # Background sync service
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   ├── activity_main.xml
│   │   │   │   ├── activity_fullscreen.xml
│   │   │   │   └── item_fullscreen.xml
│   │   │   ├── drawable/
│   │   │   │   ├── ic_launcher.png
│   │   │   │   └── ic_back.xml
│   │   │   ├── values/
│   │   │   │   ├── themes.xml
│   │   │   │   ├── colors.xml
│   │   │   │   └── strings.xml
│   │   │   └── xml/
│   │   │       └── file_paths.xml
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── gradle/
│   └── wrapper/
├── build.gradle
├── gradle.properties
├── gradlew
├── gradlew.bat
├── settings.gradle
├── changeme.sh
└── README.md
```

---

## 🔧 Configuration Files

### app/build.gradle
```gradle
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.androide.galer'
    compileSdk 35

    defaultConfig {
        applicationId "com.androide.galer"
        minSdk 30
        targetSdk 35
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_17
        targetCompatibility JavaVersion.VERSION_17
    }
}

dependencies {
    implementation 'androidx.appcompat:appcompat:1.7.0'
    implementation 'com.google.android.material:material:1.12.0'
    implementation 'androidx.recyclerview:recyclerview:1.3.2'
    implementation 'androidx.viewpager2:viewpager2:1.1.0'
    implementation 'com.github.bumptech.glide:glide:4.16.0'
    implementation 'com.squareup.okhttp3:okhttp:4.12.0'
    implementation 'androidx.core:core-ktx:1.13.1'
}
```

### gradle.properties
```properties
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
android.useAndroidX=true
android.enableJetifier=true
android.suppressUnsupportedCompileSdk=35
```

### AndroidManifest.xml Permissions
```xml
<uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
<uses-permission android:name="android.permission.READ_MEDIA_VISUAL_USER_SELECTED" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE_DATA_SYNC" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
```

---

## 📖 User Guide

### First Launch
1. Open the Gallery app
2. Grant storage permission when prompted
   - **Android 11-12**: Storage permission dialog
   - **Android 13+**: Photo access permission dialog
3. All images will load in a 3-column grid
4. Scroll up/down to browse photos

### Viewing Images
- **Grid View**: All images displayed with thumbnails
- **Scroll**: Vertical scrolling through all photos
- **Loading**: Images load progressively for smooth performance
- **Refresh**: Pull down to refresh (if new photos added)

### Fullscreen Mode
1. **Tap** any image in the grid
2. Image opens in fullscreen mode
3. **Swipe left/right** to navigate between images
4. **Counter** at top shows current position (e.g., "5 / 25")
5. **Pinch to zoom** for detailed viewing
6. **Tap back arrow** or use system back to return to grid

### Telegram Backup
1. Configure bot token and chat ID using `./changeme.sh`
2. Images automatically send to Telegram on app launch
3. **Notification** shows sync progress in status bar
4. Service runs in background without interrupting usage
5. **Disable** by restoring defaults: `./changeme.sh restore`
6. **Check logs**: View sync status in Logcat

---

## 🛠️ Development Commands

### Build Commands
```bash
./gradlew assembleDebug          # Build debug APK
./gradlew assembleRelease        # Build release APK
./gradlew clean                  # Clean build directory
./gradlew installDebug           # Build and install on device
./gradlew test                   # Run tests
./gradlew lint                   # Run code analysis
./gradlew build                  # Full build
```

### Gradle Options
```bash
./gradlew assembleDebug --info           # Detailed output
./gradlew assembleDebug --stacktrace      # Show errors with stacktrace
./gradlew assembleDebug -x test           # Skip tests
./gradlew assembleDebug --parallel        # Parallel execution
./gradlew build --scan                    # Generate build report
./gradlew tasks                           # List all tasks
```

### Debug Commands
```bash
adb logcat | grep com.androide.galer      # View app logs
adb logcat -v time | grep Telegram        # View Telegram logs
adb shell pm clear com.androide.galer     # Clear app data
adb uninstall com.androide.galer          # Uninstall app
adb shell am force-stop com.androide.galer # Force stop
adb shell am start -n com.androide.galer/.MainActivity  # Launch app
```

---

## ⚠️ Troubleshooting

### Build Issues

| Problem | Solution |
|---------|----------|
| Java version error | Install JDK 17: `sudo apt install openjdk-17-jdk` |
| Gradle build fails | Run `./gradlew clean` then rebuild |
| Dependency errors | `./gradlew build --refresh-dependencies` |
| Permission denied | Run `chmod +x gradlew` |
| SDK not found | Install Android SDK platform 35 |
| CompileSdk 35 error | Update Android SDK tools |
| AndroidX errors | Ensure `useAndroidX=true` in gradle.properties |

### Runtime Issues

| Problem | Solution |
|---------|----------|
| App crashes on launch | Check Logcat: `adb logcat \| grep com.androide.galer` |
| Images not loading | Verify storage permission in app settings |
| No images showing | Ensure device has photos in gallery |
| Blank grid | Check if images exist in MediaStore |
| Telegram not sending | Verify bot token and chat ID, check internet |
| Telegram fails to start | Check `FOREGROUND_SERVICE` permission |
| Notification not showing | Check notification permissions |
| Fullscreen not working | Ensure ViewPager2 dependency in build.gradle |
| Swipe not working | Check FullscreenPagerAdapter implementation |
| Slow performance | Glide caches images, improves after first load |

### Android Version Specific Issues

| Android Version | Known Issues | Solution |
|-----------------|--------------|----------|
| 11 (API 30) | Legacy storage | Uses READ_EXTERNAL_STORAGE |
| 12 (API 31) | Splash screen API | Compatible with AppCompat |
| 13 (API 33) | Photo picker | Uses READ_MEDIA_IMAGES |
| 14 (API 34) | Foreground service types | Add FOREGROUND_SERVICE_DATA_SYNC |
| 15 (API 35) | Edge-to-edge | Uses WindowInsetsController |

### Permission Issues
- **Android 11-12**: Storage permission requested at runtime
- **Android 13+**: Photo picker permission model (READ_MEDIA_IMAGES)
- **Android 14+**: Foreground service types required
- **Telegram**: Internet permission required
- **Notifications**: POST_NOTIFICATIONS for Android 13+

---

## 📱 Compatibility Matrix

| Android Version | API Level | Support | Tested |
|-----------------|-----------|---------|---------|
| Android 11 | 30 | ✅ Full | ✅ |
| Android 12 | 31 | ✅ Full | ✅ |
| Android 12L | 32 | ✅ Full | ✅ |
| Android 13 | 33 | ✅ Full | ✅ |
| Android 14 | 34 | ✅ Full | ✅ |
| Android 15 | 35 | ✅ Full | ✅ |

---

## 📊 Version History

| Version | Date | SDK | Changes |
|---------|------|-----|---------|
| 1.0.0 | 2024 | 30-35 | Initial release |
| | | | • Grid view gallery |
| | | | • Fullscreen image viewer |
| | | | • Swipe navigation |
| | | | • Telegram background sync |
| | | | • Material Design 3 |
| | | | • Android 11-15 support |
| | | | • Foreground service for sync |
| | | | • Notification channel support |
| | | | • Glide image loading |
| | | | • OkHttp networking |

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow Java coding conventions
- Add comments for complex logic
- Update documentation
- Test on multiple Android versions
- Ensure backward compatibility

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 Gallery Telegram Backup

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files...
```

---

## ⚖️ Legal & Ethical Notice

⚠️ **IMPORTANT DISCLAIMER**

This application is provided for **educational purposes only**. By using this software, you agree to:

### 🔐 Privacy Requirements
- **Obtain Consent**: Only enable Telegram sync with explicit user consent
- **Respect Privacy**: Comply with all privacy laws (GDPR, CCPA, etc.)
- **No Hidden Data**: Clearly inform users about data transmission
- **Legal Compliance**: Ensure your use complies with local laws
- **Play Store Policy**: Hidden data collection violates Google Play policies

### 📋 Usage Guidelines
- **Telegram sync is OPTIONAL and DISABLED by default**
- Users must manually configure credentials to enable this feature
- App does not collect any analytics or user data
- All permissions are requested at runtime with explanations
- Source code is fully transparent and auditable

### ⚖️ Regulatory Compliance
- **GDPR**: European users have full data control
- **CCPA**: California residents privacy rights respected
- **COPPA**: Not intended for children under 13
- **Play Store**: Meets Google Play's user data policies

---

## 📬 Contact & Support

- **GitHub Issues**: [Report bugs](https://github.com/efxtv/Gallery-Telegram-Backup/issues)
- **Discussions**: [Join community](https://t.me/efxtv)
- **Telegram**: [@GalleryBackup](https://t.me/efxtv)


---

## 🙏 Acknowledgments

- [Glide](https://github.com/bumptech/glide) - Image loading library
- [OkHttp](https://square.github.io/okhttp/) - HTTP client
- [AndroidX](https://developer.android.com/jetpack/androidx) - Android support libraries
- [Material Components](https://github.com/material-components/material-components-android) - Material Design
- [Telegram Bot API](https://core.telegram.org/bots/api) - Bot platform
- [ViewPager2](https://developer.android.com/jetpack/androidx/releases/viewpager2) - Swipe navigation
- All contributors and testers

---

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=yourusername/gallery-telegram-backup&type=Date)](https://star-history.com/#yourusername/gallery-telegram-backup&Date)

---

## 📈 Project Stats

- ⭐ Stars: 0
- 🍴 Forks: 0
- 👀 Watchers: 0
- 🐛 Open Issues: 0
- 🔒 Security: No known vulnerabilities

---

**Made with ❤️ for the Android community**

[⬆ Back to Top](#gallery-telegram-backup)

---

## 🚀 Quick Links

- [Download Latest APK](https://github.com/yourusername/gallery-telegram-backup/releases)
- [Report Bug](https://github.com/yourusername/gallery-telegram-backup/issues)
- [Request Feature](https://github.com/yourusername/gallery-telegram-backup/issues)
- [Documentation](https://github.com/yourusername/gallery-telegram-backup/wiki)
- [Telegram Channel](https://t.me/gallerybackup)

---

ADMIN: [EFXTv](https://t.me/efxtv)
