# Important in Flutter

## Introduction
Flutter is a powerful framework for building cross-platform applications. This README provides essential commands, important packages, common issues, and their solutions to help you master Flutter development.

---

## 1. Important Commands

### General Commands
```sh
flutter doctor           # Checks Flutter installation and dependencies
flutter create my_app    # Creates a new Flutter project
flutter run              # Runs the app on a connected device or emulator
flutter build apk        # Builds an APK for Android
flutter build ios        # Builds an iOS app
flutter clean            # Clears the build cache
flutter pub get          # Fetches dependencies from pubspec.yaml
flutter pub upgrade      # Updates dependencies to the latest versions
flutter analyze          # Analyzes the project for potential issues
flutter format .         # Formats all Dart files in the project
flutter test             # Runs tests in the project
```

### Dart Commands
```sh
dart --version         # Checks Dart version
dart run file.dart     # Runs a specific Dart file
dart analyze          # Analyzes Dart code for errors and warnings
```

### Build APK for Different Architectures
```sh
flutter build apk --target-platform android-arm,android-arm64,android-x64 --split-per-abi
```
```sh
Explanation:

This command builds separate APKs for different architectures (arm, arm64, x64).

--split-per-abi ensures each APK is optimized for a specific CPU architecture, reducing APK size.

It is useful when deploying to Play Store, as users download only the compatible APK for their device.
```

### Gradle Issues Commands
```sh
cd android && ./gradlew clean        # Cleans the Gradle build cache
cd android && ./gradlew build         # Builds the Android project
cd android && ./gradlew dependencies  # Lists dependencies and resolves conflicts
cd android && ./gradlew --stop        # Stops all Gradle daemons
cd android && ./gradlew --refresh-dependencies  # Forces dependency refresh
cd android && ./gradlew clean assembleDebug  # This compiles the app in debug mode

```
### Basic Git Commands
```sh
git init # Initializes a new Git repository in the current directory.
git clone <repo_url> #Clones an existing Git repository from a remote source.
git status # Shows the current status of your working directory (changes, staged files, etc.).
git add <file> # Adds a specific file to the staging area.
git add . # Adds all changes in the current directory to the staging area.
git commit -m "message" # Commits the staged changes with a descriptive message.
git push origin <branch> # Pushes committed changes to the remote repository.
git pull origin <branch> # Fetches and merges changes from the remote repository.
git branch # Lists all branches in the repository.
git checkout <branch> # Switches to a different branch.
git checkout -b <new_branch> # Creates and switches to a new branch.
git merge <branch> # Merges the specified branch into the current branch.
git log # Displays the commit history.
git diff # Shows differences between changes in working directory and last commit.
git reset --hard <commit> # Resets the repository to a specific commit (removes all changes).
git stash # Temporarily saves changes without committing.
git stash pop # Restores saved changes from stash.
git rebase <branch> # Reapplies commits from the current branch on top of another branch.
git tag <tag_name> # Creates a tag for a specific commit (useful for releases).
git remote -v # Lists remote repositories linked to your project.
git fetch # Fetches changes from the remote without merging them.
git show <commit> # Displays details about a specific commit.
git rm <file> # Removes a file from the repository.
git revert <commit> # Creates a new commit that undoes the changes of a specific commit.
git cherry-pick <commit> # Applies a specific commit from another branch.

```

### Basic Windows Platform Commands
```sh
flutter pub global activate msix
flutter build windows --release
dart pub global run msix:create

```

---

## 2. Important Packages

### State Management
- `provider` - A recommended approach for state management.
- `riverpod` - A powerful alternative to provider.
- `bloc` - Business logic component for structured state management.
- `get` - Simple and efficient state management solution.

### Networking
- `http` - Simple package for REST API requests.
- `dio` - A more advanced HTTP client with interceptors and error handling.
- `graphql_flutter` - For integrating GraphQL in Flutter.

### Database and Storage
- `sqflite` - SQLite plugin for local database storage.
- `hive` - Lightweight and fast key-value database.
- `shared_preferences` - Store small amounts of data persistently.
- `firebase_core` & `cloud_firestore` - Firebase Firestore for cloud database storage.

### UI & Design
- `flutter_svg` - For SVG image support.
- `cached_network_image` - Caches images for performance.
- `lottie` - Adds Lottie animations.
- `flutter_screenutil` - Helps with responsive UI design.

### Authentication
- `firebase_auth` - Firebase authentication support.
- `google_sign_in` - Google login integration.
- `flutter_facebook_auth` - Facebook login integration.
- `sign_in_with_apple` - Apple login support.

### Others
- `flutter_local_notifications` - Local push notifications.
- `geolocator` - Fetch device location.
- `url_launcher` - Open URLs, emails, or phone calls.
- `flutter_native_splash` - Custom splash screens.

---

## 3. Common Issues & Solutions

### Issue: App Stuck on White Screen
**Solution:** Ensure `main()` method calls `WidgetsFlutterBinding.ensureInitialized()` before running `runApp()`.
```dart
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  runApp(MyApp());
}
```

### Issue: Dependencies Not Found
**Solution:** Run `flutter pub get` to fetch the required dependencies.

### Issue: Emulator Not Detecting Changes
**Solution:** Try running `flutter clean` followed by `flutter run`.

### Issue: Gradle Build Failing in Android
**Solution:**
- Ensure `android/gradle/wrapper/gradle-wrapper.properties` has a compatible Gradle version.
- Run `flutter doctor` and resolve any missing dependencies.

### Issue: iOS Build Failing
**Solution:**
- Ensure Xcode is installed and updated.
- Run `pod install` inside `ios/` directory.

### Issue: Firebase Not Working on iOS
**Solution:**
- Make sure `GoogleService-Info.plist` is correctly placed in `ios/Runner/`.
- Add `use_frameworks!` in the `Podfile` and run `pod install`.

### Issue: PlatformException in Camera or Location Plugins
**Solution:**
- Add required permissions in `AndroidManifest.xml` (for Android) and `Info.plist` (for iOS).

## Common Signing Issues & Solutions

### Issue: Keystore Not Found
**Solution:** Ensure that the `keystore.jks` file exists and the path is correct in `key.properties`.

### Issue: Incorrect Keystore Password
**Solution:** Double-check the `storePassword` and `keyPassword` in `key.properties` and ensure they match the actual keystore.

### Issue: Missing Signing Config in `build.gradle`
**Solution:**
```gradle
android {
    signingConfigs {
        release {
            storeFile file("../keystore.jks")
            storePassword "your_password"
            keyAlias "your_key_alias"
            keyPassword "your_key_password"
        }
    }
}
```

### Issue: Invalid Key Alias
**Solution:** Run the following command to list key aliases in your keystore:
```sh
keytool -list -v -keystore your_keystore.jks
```

### Issue: `SHA1` or `SHA256` Mismatch
**Solution:** Get the correct fingerprint using:
```sh
keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
```

### Issue: Play Store Rejecting APK Due to Signing
**Solution:** Ensure your app is signed with the correct `upload key` and matches the Play Console key.

### Issue: `jarsigner` Verification Failed
**Solution:** Run the following command to verify the signature:
```sh
jarsigner -verify -verbose -certs your_app.apk
```



```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

```xml
<key>NSCameraUsageDescription</key>
<string>We need camera access</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>We need your location</string>
```

# How to Change Package Name in Flutter

Changing the package name in a Flutter project can be done easily using the `change_app_package_name` package. Follow the steps below to rename your Flutter package.

## **Method 1: Using `change_app_package_name`**
This is the easiest way to change the package name in Flutter.

### **Step 1: Add Dependency**
Run the following command in the terminal:
```sh
flutter pub add change_app_package_name
```

### **Step 2: Change Package Name**
Run the command below, replacing `com.new.package.name` with your desired package name:
```sh
flutter pub run change_app_package_name:main com.new.package.name
```

This will automatically update the necessary files with the new package name.

### **Step 3: Verify Changes**
After running the command, check that the following files have been updated:
- `android/app/src/main/AndroidManifest.xml`
- `android/app/build.gradle`
- `android/app/src/main/kotlin/com/new/package/name/MainActivity.kt` (if using Kotlin)
- `android/app/src/main/java/com/new/package/name/MainActivity.java` (if using Java)
- `ios/Runner.xcodeproj/project.pbxproj`
- `ios/Runner/Info.plist`

### **Step 4: Clean and Rebuild Project**
Run the following commands to apply the changes:
```sh
flutter clean
flutter pub get
flutter run
```

## **Method 2: Manual Package Name Change**
If you prefer to manually update the package name, follow these steps:

### **Step 1: Update Android Package Name**
1. Open `android/app/src/main/AndroidManifest.xml` and change the `package` attribute:
   ```xml
   <manifest xmlns:android="http://schemas.android.com/apk/res/android"
       package="com.new.package.name">
   ```
2. Update `android/app/build.gradle`:
   ```gradle
   android {
       defaultConfig {
           applicationId "com.new.package.name"
       }
   }
   ```
3. Rename the folder structure inside `android/app/src/main/kotlin/` (or `java/`) to match the new package name.

### **Step 2: Update iOS Bundle Identifier**
1. Open `ios/Runner.xcodeproj` in Xcode.
2. Go to `Runner` > `General` > `Identity` and change the `Bundle Identifier`.
3. Update `ios/Runner/Info.plist`:
   ```xml
   <key>CFBundleIdentifier</key>
   <string>com.new.package.name</string>
   ```

### **Step 3: Clean and Rebuild Project**
After making these changes, run:
```sh
flutter clean
flutter pub get
flutter run
```


# How to Build a Windows App Using Flutter

Flutter allows developers to build high-performance applications for Windows. This guide provides a detailed step-by-step approach to setting up, building, and optimizing a Windows app using Flutter.

---

## **1. System Requirements**
Before you start, ensure your system meets the following requirements:

- Windows 10 or later (64-bit)
- PowerShell 5.0 or later
- Git for Windows
- Visual Studio 2022 (with C++ development tools)
- Flutter SDK (latest stable version)

### **Install Flutter SDK**
Download and extract Flutter from the official site:
```sh
https://flutter.dev/docs/get-started/install/windows
```
Add Flutter to the system path and verify the installation with:
```sh
flutter doctor
```
Ensure there are no missing dependencies.

---

## **2. Enable Windows Desktop Support**
Run the following command to enable Windows development in Flutter:
```sh
flutter config --enable-windows-desktop
```
Check if Windows support is enabled by running:
```sh
flutter doctor
```
If everything is correctly set up, you should see `Windows (desktop)` listed as a supported platform.

---

## **3. Create a New Windows Flutter Project**
Create a new Flutter project with:
```sh
flutter create my_windows_app
cd my_windows_app
```
To confirm Windows support, list available devices:
```sh
flutter devices
```

---

## **4. Run the Windows App**
To run your Windows Flutter app:
```sh
flutter run -d windows
```
If you encounter issues, try:
```sh
flutter clean
flutter pub get
flutter run -d windows
```

---

## **5. Configure Windows-Specific Settings**
### **Modify `windows/runner/main.cpp`**
This is the entry point for the Windows app. You can modify it to adjust behavior or add native functionality.

### **Change the Application Icon**
Replace `windows/runner/resources/app_icon.ico` with your own icon.
Then, modify `windows/CMakeLists.txt` to reference the new icon.

### **Customize the Window Size**
Edit `windows/runner/main.cpp` and modify the `CreateAndShowWindow` function:
```cpp
window.CreateAndShow(L"My Windows App", {100, 100, 800, 600});
```

---

## **6. Build the Windows App for Release**
Once development is complete, build the Windows executable:
```sh
flutter build windows
```
This creates an executable in `build/windows/runner/Release/`.

---

## **7. Distribute the Windows App**
### **Package the App**
You can package the app into an installer using `NSIS` or `Inno Setup`:
- **NSIS:** https://nsis.sourceforge.io/
- **Inno Setup:** https://jrsoftware.org/isinfo.php

### **Zip and Share**
Alternatively, zip the `build/windows/runner/Release/` folder and share it directly.

---

## **8. Common Issues & Solutions**
### **Issue: Windows app fails to launch**
**Solution:**
- Ensure all dependencies are installed (`flutter doctor`)
- Try running `flutter clean` followed by `flutter build windows`

### **Issue: `flutter run -d windows` does not detect Windows**
**Solution:**
- Run `flutter doctor` to check if Windows support is enabled.
- If missing, enable it using `flutter config --enable-windows-desktop`.

### **Issue: Slow performance on Windows**
**Solution:**
- Ensure you are using `release` mode for better performance:
  ```sh
  flutter build windows --release
  ```
- Optimize UI rendering using `const` widgets where possible.

---

## **9. Best Practices for Windows Flutter Apps**
- Use **Platform Channels** to interact with Windows-specific APIs.
- Optimize **state management** with `provider` or `riverpod`.
- Implement **error logging** with `sentry_flutter`.
- Ensure the UI is **responsive** for different window sizes.


---

## 4. Best Practices in Flutter Development
- Use **const** for widgets that don’t change to improve performance.
- Organize code into **separate files** for readability and maintainability.
- Use **Dart extension methods** to simplify repetitive tasks.
- Apply **Flutter hooks** to manage state efficiently.
- Optimize app size by using **Flutter WebP images** instead of PNGs.
- Prefer **lazy loading** for large lists to improve performance.
- Write unit and widget tests using **flutter_test** package.

---

## Conclusion
Flutter is an ever-evolving framework, and mastering its commands, packages, and debugging techniques will help you build efficient, scalable applications. Keep experimenting and stay updated with new features!

