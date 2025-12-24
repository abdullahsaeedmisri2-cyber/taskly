# Firebase Authentication Setup Guide

This guide will help you set up Firebase Authentication for the Taskly app.

## Prerequisites

1. A Firebase account (create one at https://firebase.google.com/)
2. Flutter SDK installed
3. Firebase CLI (optional, for easier setup)

## Setup Steps

### 1. Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" or select an existing project
3. Follow the setup wizard

### 2. Enable Email/Password Authentication

1. In Firebase Console, go to **Authentication**
2. Click **Get Started**
3. Go to the **Sign-in method** tab
4. Click on **Email/Password**
5. Enable **Email/Password** authentication
6. Click **Save**

### 3. Add Firebase to Your Flutter App

#### For Android:

1. In Firebase Console, click the Android icon to add an Android app
2. Register your app with package name: `com.example.taskly` (or your package name)
3. Download `google-services.json`
4. Place it in `android/app/` directory
5. Update `android/build.gradle`:
   ```gradle
   buildscript {
       dependencies {
           classpath 'com.google.gms:google-services:4.4.0'
       }
   }
   ```
6. Update `android/app/build.gradle`:
   ```gradle
   apply plugin: 'com.google.gms.google-services'
   ```

#### For iOS:

1. In Firebase Console, click the iOS icon to add an iOS app
2. Register your app with bundle ID: `com.example.taskly` (or your bundle ID)
3. Download `GoogleService-Info.plist`
4. Place it in `ios/Runner/` directory
5. Open `ios/Runner.xcworkspace` in Xcode
6. Right-click `Runner` folder → Add Files to "Runner"
7. Select `GoogleService-Info.plist` and ensure "Copy items if needed" is checked

#### For Web:

1. In Firebase Console, click the Web icon to add a Web app
2. Register your app
3. Copy the Firebase configuration
4. Update `web/index.html` with your Firebase config (if needed)

### 4. Install FlutterFire CLI (Recommended)

```bash
dart pub global activate flutterfire_cli
flutterfire configure
```

This will automatically configure Firebase for all platforms.

### 5. Verify Setup

Run the app:
```bash
flutter pub get
flutter run
```

## Testing Authentication

1. Launch the app
2. You should see the login screen
3. Click "Sign Up" to create a new account
4. Enter email and password
5. After signup, you'll be redirected to the home screen
6. You can logout from the menu in the top right

## Troubleshooting

### Firebase not initialized error

If you see "Firebase initialization error", make sure:
- `google-services.json` is in `android/app/` (Android)
- `GoogleService-Info.plist` is in `ios/Runner/` (iOS)
- Firebase project is created and Email/Password auth is enabled

### Authentication not working

1. Check Firebase Console → Authentication → Sign-in method
2. Ensure Email/Password is enabled
3. Check that your app's package name/bundle ID matches Firebase configuration

## Security Rules

For production, configure Firebase Security Rules:
- Go to Firebase Console → Firestore Database → Rules
- Set appropriate rules for your data

## Additional Resources

- [Firebase Flutter Documentation](https://firebase.flutter.dev/)
- [Firebase Authentication Documentation](https://firebase.google.com/docs/auth)
- [FlutterFire Documentation](https://firebase.flutter.dev/docs/overview)



