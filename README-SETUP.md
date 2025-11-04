# Setup Instructions

## Required Configuration Files

Before building and running the app, you need to configure the following files with your own credentials:

### 1. GoogleService-Info.plist (Firebase Configuration)

**Location:** Required in both:
- Root directory: `GoogleService-Info.plist`
- `Liquid Pay/GoogleService-Info.plist`

**How to get it:**
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project (or create a new one)
3. Click the gear icon → Project Settings
4. Scroll down to "Your apps" section
5. Select your iOS app (or add a new iOS app)
6. Download the `GoogleService-Info.plist` file
7. Copy it to both locations mentioned above

**Template file:** See `GoogleService-Info.plist.template` for reference structure

### 2. Liquid-Pay-Info.plist (AdMob Configuration)

**Location:** Root directory: `Liquid-Pay-Info.plist`

**How to configure:**
1. Go to [AdMob Console](https://apps.admob.com/)
2. Create or select your app
3. Get your AdMob App ID (format: `ca-app-pub-XXXXXXXXXXXXXXXX~XXXXXXXXXX`)
4. Update the `GADApplicationIdentifier` value in `Liquid-Pay-Info.plist`
5. Optionally add your Interstitial Ad Unit ID if using ads

**Template file:** See `Liquid-Pay-Info.plist.template` for reference structure

### 3. Firebase Functions Secrets

The backend functions require Razorpay credentials. Configure them via Firebase CLI:

```bash
cd functions
firebase functions:secrets:set RAZORPAY_KEY_ID
firebase functions:secrets:set RAZORPAY_KEY_SECRET
firebase functions:secrets:set RAZORPAY_WEBHOOK_SECRET
```

Or set them as environment variables when deploying.

### 4. AdMob Test Device ID (Optional)

If you're testing ads during development, you can add your test device ID in `Liquid Pay/AppDelegate.swift`:

```swift
MobileAds.shared.requestConfiguration.testDeviceIdentifiers = ["YOUR_TEST_DEVICE_ID"]
```

## Building the Project

1. Install CocoaPods dependencies:
   ```bash
   pod install
   ```

2. Open the workspace (not the project):
   ```bash
   open "Liquid Pay.xcworkspace"
   ```

3. Build and run in Xcode

## Important Notes

- **Never commit** the actual `GoogleService-Info.plist` or `Liquid-Pay-Info.plist` files with real credentials
- These files are excluded via `.gitignore`
- Always use template files for reference
- Keep your Firebase and AdMob credentials secure

