# ManyMind AI — native installer build project

Website: https://manymind-ai-tsklne.v2.appdeploy.ai/

This project packages the live ManyMind website in lightweight native webview shells. It intentionally loads the deployed HTTPS site, so updates to the website can appear in the wrappers without rebuilding the wrapper. Internet access is required. This wrapper does not itself bundle or run model weights locally.

## Important: what this ZIP provides

This is the source project and a GitHub Actions workflow to create **an installable Android debug APK** and **a Windows EXE installer**. I could not compile those binary files in this environment because Android SDK/Gradle and a Windows build runner are not available here, and package downloads are network-restricted. Do not treat this project ZIP as an APK or EXE binary.

## Build both binaries with GitHub Actions

1. Create a new private GitHub repository.
2. Extract this ZIP and upload its contents to the repository root (keep `.github/workflows/build-native.yml`).
3. Open the repository's **Actions** tab.
4. Select **Build ManyMind APK and EXE**, choose **Run workflow**, and start it.
5. When both jobs finish, open the run and download these artifacts:
   - `manymind-android-apk` — `app-debug.apk` (debug-signed; suitable for sideload testing).
   - `manymind-windows-exe` — `ManyMind-AI-Setup-1.0.0.exe` (unsigned installer; Windows SmartScreen may show a warning).

These are build artifacts for personal testing, not store-published or publisher-signed releases. For Google Play or broad Windows distribution, configure a private Android signing key and a trusted Windows code-signing certificate in secure CI secrets.

## Android direct build

Install Android Studio, JDK 17+, Android SDK Platform 35, Build Tools 35+, and Gradle 8.9. From `android-shell/`, run:

```sh
gradle --no-daemon assembleDebug
```

Output: `android-shell/app/build/outputs/apk/debug/app-debug.apk`.

## Windows direct build

Install Node.js 22+. From `windows-shell/`, run:

```powershell
npm install
npm run build:win
```

Output: `windows-shell/dist/ManyMind-AI-Setup-1.0.0.exe`.

## Security and scope

- The native wrapper opens only the ManyMind app URL by default.
- External links are handed off to the system browser in the Windows wrapper.
- API credentials are not embedded in these wrappers; enter provider keys in ManyMind's Connections page. They remain in the current browser tab's memory only.
- Android APK is debug-signed in CI. No production signing credentials are included.
