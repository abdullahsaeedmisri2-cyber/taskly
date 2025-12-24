# Firebase Firestore Setup Guide

## ✅ What Has Been Implemented

### 1. **Logout Functionality** ✅
- Added logout confirmation dialog
- Improved logout error handling
- Logout is accessible from the home screen menu (top right account icon)

### 2. **Task Dates** ✅
- Added `startDate` and `endDate` fields to Task model
- Added date pickers in the task form (Add/Edit Task screen)
- Task items now display start and end dates
- Dates are optional (can be left empty)

### 3. **Firebase Firestore Backend** ✅
- Created `TaskDataSourceFirestore` class
- Tasks are now stored in Firebase Firestore instead of SQLite
- Data structure: `users/{userId}/tasks/{taskId}`
- Each task includes:
  - id, title, description, type, status
  - startDate, endDate (optional)
  - createdAt, updatedAt (automatic timestamps)

## 🔧 Firebase Console Setup Required

### Step 1: Enable Firestore Database

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Select your project: **taskly-2675a**
3. Click on **Firestore Database** in the left menu
4. Click **Create database**
5. Choose **Start in test mode** (for development)
6. Select your preferred location (e.g., `us-central1`)
7. Click **Enable**

### Step 2: Set Up Security Rules (IMPORTANT!)

After creating the database, go to the **Rules** tab and update with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can only access their own tasks
    match /users/{userId}/tasks/{taskId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

Click **Publish** to save the rules.

### Step 3: Verify Email/Password Authentication

1. Go to **Authentication** → **Sign-in method**
2. Make sure **Email/Password** is **Enabled**
3. Click **Save** if you made changes

## 📱 Testing the App

1. **Run the app:**
   ```bash
   flutter run
   ```

2. **Test Sign Up/Sign In:**
   - Create a new account
   - Sign in with your credentials

3. **Test Task Creation:**
   - Click the "+" button to add a task
   - Fill in title, description, type, status
   - **Select Start Date** (optional)
   - **Select End Date** (optional)
   - Save the task

4. **Test Logout:**
   - Click the account icon (top right)
   - Click "Logout"
   - Confirm logout in the dialog

5. **Verify Data in Firebase:**
   - Go to Firebase Console → Firestore Database
   - You should see: `users/{userId}/tasks/{taskId}`
   - Check that your tasks are stored there

## 🔄 Switching Back to SQLite (Optional)

If you want to use SQLite instead of Firebase, edit `lib/data/datasource/datasource_provider.dart`:

```dart
final dataSourceProvider = Provider((ref) {
  // Use SQLite instead of Firebase
  return TaskDataSourceAsDatabase();
  // Comment out Firebase:
  // return TaskDataSourceFirestore();
});
```

**Note:** SQLite doesn't sync across devices. Firebase Firestore syncs data across all devices where the user is logged in.

## 📝 Notes

- **Dates are optional:** Users can create tasks without dates
- **End date validation:** End date must be after start date
- **Data sync:** All tasks are synced to Firebase and available on any device where you're logged in
- **User-specific data:** Each user only sees their own tasks

## 🐛 Troubleshooting

### "Permission denied" error
- Check Firestore security rules (Step 2 above)
- Make sure user is authenticated

### Tasks not appearing
- Check Firebase Console → Firestore Database
- Verify the user is logged in
- Check console logs for errors

### Date picker not working
- Make sure `intl` package is installed: `flutter pub get`
- Restart the app

## ✅ Summary

All requested features have been implemented:
- ✅ Logout page/functionality with confirmation
- ✅ Start date and end date for tasks
- ✅ Firebase Firestore backend for task storage

Your app is now ready to use with Firebase Firestore!


