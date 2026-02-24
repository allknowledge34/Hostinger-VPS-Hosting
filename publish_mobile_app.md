# 🚀 FitShare Mobile App

![Expo](https://img.shields.io/badge/Expo-000000?style=for-the-badge&logo=expo&logoColor=white)
![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Android](https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![iOS](https://img.shields.io/badge/iOS-000000?style=for-the-badge&logo=apple&logoColor=white)
![EAS Build](https://img.shields.io/badge/EAS-Build-blueviolet?style=for-the-badge)

---

## 📱 Production Builds (APK • AAB • IPA)

This project uses **Expo + EAS Build** to generate signed production builds for Android and iOS.

---

## ⚙️ Prerequisites

- Node.js installed  
- Expo project ready  
- Expo account  
- Apple Developer Account (for iOS production build)

---

## 🔧 Install EAS CLI

```bash
npm install -g eas-cli
```

Login:

```bash
eas login
```

---

## 🏗 Initialize EAS

Run inside project root:

```bash
eas init
```

This creates an `eas.json` file.

---

## 📄 Recommended eas.json

```json
{
  "build": {
    "preview": {
      "distribution": "internal"
    },
    "production": {
      "android": {
        "buildType": "app-bundle"
      },
      "ios": {
        "simulator": false
      }
    }
  }
}
```

---

# 🤖 Android Builds

## 🔹 Generate APK (Testing)

```bash
eas build -p android --profile preview
```

Generates installable `.apk` file.

---

## 🔹 Generate AAB (Play Store)

```bash
eas build -p android --profile production
```

Generates `.aab` file (Required for Google Play Store).

---

# 🍎 iOS Build

⚠ Requires Apple Developer Account ($99/year)

## 🔹 Generate IPA (App Store)

```bash
eas build -p ios --profile production
```

Generates `.ipa` file for App Store submission.

---

# 📦 Check Build Status

```bash
eas build:list
```

Download build from Expo dashboard link shown in terminal.

---

# 📱 app.json Configuration

Make sure your `app.json` includes:

```json
{
  "expo": {
    "name": "FitShare",
    "slug": "fitshare",
    "version": "1.0.0",
    "android": {
      "package": "com.aicodinghub.fitshare"
    },
    "ios": {
      "bundleIdentifier": "com.aicodinghub.fitshare"
    }
  }
}
```

⚠ Package name & bundle identifier cannot be changed after publishing.

---

# 🔐 Signing

EAS automatically:

- Generates signing keys  
- Manages keystore securely  
- Signs Android & iOS builds  
- Handles certificates  

No manual signing required.

---

# 🏪 Publishing

Android → Upload `.aab` to Google Play Console  
iOS → Upload `.ipa` to App Store Connect  

---

# 🚀 Production Workflow

1. Build preview APK  
2. Test application  
3. Build production AAB  
4. Upload to Play Store  
5. Build iOS production IPA  
6. Submit to App Store  

---

# 💎 Tech Stack

- React Native  
- Expo  
- EAS Build  
- REST API Backend  
- JWT Authentication  

---

# 👨‍💻 Developed By

AI Coding Hub  

If you found this project helpful, consider ⭐ starring the repository.

🚀 Your app is production ready!
