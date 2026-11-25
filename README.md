# OpenFilm Android App

An Android WebView wrapper for [OpenFilm Studio](https://openfilm.dev) — the open-source AI video agent.

## Features
- Full OpenFilm Studio experience in a native Android app
- File picker support for media uploads
- Camera & microphone permissions for recording
- Pull-to-refresh
- Hardware-accelerated WebView

## Build via GitHub Actions (recommended)

### 1. Fork or push this folder to a new GitHub repository

```bash
git init
git add .
git commit -m "Initial OpenFilm Android app"
git remote add origin https://github.com/YOUR_USERNAME/openfilm-android.git
git push -u origin main
```

### 2. Trigger the workflow

Go to your repo → **Actions** → **Build OpenFilm APK** → **Run workflow**.

A debug APK (`OpenFilm-debug`) will be generated and available as a workflow artifact — **no signing needed**.

### 3. Download the APK

1. Click the finished workflow run.
2. Scroll to **Artifacts** and download **OpenFilm-debug**.
3. Unzip and install `app-debug.apk` on your Android device.

> Enable **Install Unknown Apps** in Android Settings first.

---

## Optional: Release (signed) APK

To produce a signed release APK, add these **repository secrets** in Settings → Secrets:

| Secret | Value |
|---|---|
| `KEYSTORE_B64` | Base64-encoded `.jks` keystore file |
| `KEY_ALIAS` | Key alias in the keystore |
| `KEY_PASSWORD` | Key password |
| `STORE_PASSWORD` | Keystore password |

### Generate a keystore (run on any PC/Mac with JDK):
```bash
keytool -genkey -v -keystore openfilm.jks -alias openfilm -keyalg RSA \
  -keysize 2048 -validity 10000
# Then base64-encode it:
base64 openfilm.jks
```
Paste the base64 output as the `KEYSTORE_B64` secret.

---

## Local Build (requires Android Studio / SDK on a PC)

```bash
./gradlew assembleDebug
# APK at: app/build/outputs/apk/debug/app-debug.apk
```
