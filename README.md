# Liquid Pay

A modern iOS payment app built with SwiftUI, featuring UPI payments, bill management, rewards system, and real-time currency tracking.

## 📱 Project Overview

Liquid Pay is a comprehensive payment application that enables users to make UPI payments, manage bills, track transactions, and earn rewards through a gamified experience. The app features a clean, intuitive interface with real-time currency rate tracking and a robust payment consistency index (PCI) system.

## 🏗️ Architecture

The app follows the **MVVM (Model-View-ViewModel)** architecture pattern:

- **Models**: Data structures (`Bill`, `Payment`, `CurrencyRate`, etc.)
- **Views**: SwiftUI views organized by feature (`HomeView`, `PayView`, `TransactionsView`, etc.)
- **ViewModels**: Business logic and state management (`AuthViewModel`, `PaymentViewModel`, `HomeViewModel`, etc.)
- **Services**: Reusable service layers (`PaymentsService`, `BillsService`, `CurrencyService`, etc.)

### Backend Architecture

- **Firebase Functions**: Serverless backend using TypeScript/Express
- **Firestore**: NoSQL database for user data, payments, and bills
- **Firebase Authentication**: Phone-based authentication with OTP

## 🛠️ Tech Stack

### Frontend (iOS)
- **SwiftUI** - Modern declarative UI framework
- **Combine** - Reactive programming
- **Firebase SDK** - Authentication, Firestore, Cloud Functions
- **Razorpay SDK** - Payment processing
- **Google Mobile Ads SDK** - Ad monetization
- **CocoaPods** - Dependency management

### Backend
- **Firebase Functions** - Serverless functions
- **TypeScript** - Type-safe JavaScript
- **Express.js** - Web framework
- **Node.js 20** - Runtime environment
- **Razorpay API** - Payment gateway integration

### Key Features
- Phone number authentication via Firebase
- UPI payment processing
- Bill reminders and management
- Transaction history
- Rewards and gamification system
- Real-time currency rate tracking
- Payment Consistency Index (PCI) scoring
- QR code scanning for payments

## 📋 Prerequisites

- Xcode 15.0 or later
- iOS 16.0 or later
- CocoaPods installed (`sudo gem install cocoapods`)
- Node.js 20+ (for backend functions)
- Firebase CLI (for deploying functions)
- Active accounts for:
  - Firebase (create project at [console.firebase.google.com](https://console.firebase.google.com))
  - Razorpay (create account at [razorpay.com](https://razorpay.com))
  - AdMob (create account at [admob.google.com](https://admob.google.com))

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/Rishi-Selarka/Liquid-Pay.git
cd Liquid-Pay
```

### 2. Install Dependencies

```bash
# Install CocoaPods dependencies
pod install
```

### 3. Firebase Setup

1. Create a new Firebase project at [Firebase Console](https://console.firebase.google.com/)
2. Add an iOS app to your project with Bundle ID: `com.rishiselarka.Liquid-Pay`
3. Download `GoogleService-Info.plist`
4. Place the file in **two locations**:
   - Root directory: `GoogleService-Info.plist`
   - `Liquid Pay/GoogleService-Info.plist`
5. Enable the following Firebase services:
   - Authentication (Phone provider)
   - Firestore Database
   - Cloud Functions

**Template file:** See `GoogleService-Info.plist.template` for reference structure

### 4. Razorpay Setup

1. Create a Razorpay account at [Razorpay Dashboard](https://dashboard.razorpay.com/)
2. Navigate to **Settings** → **API Keys**
3. Copy your **Key ID** and **Key Secret** (test keys for development)
4. Configure Razorpay secrets in Firebase Functions:

```bash
cd functions
firebase functions:secrets:set RAZORPAY_KEY_ID
firebase functions:secrets:set RAZORPAY_KEY_SECRET
firebase functions:secrets:set RAZORPAY_WEBHOOK_SECRET
```

5. Set up webhook in Razorpay dashboard:
   - Webhook URL: `https://your-firebase-function-url/webhook`
   - Enable events: `payment.captured`, `payment.failed`, `order.paid`

### 5. AdMob Setup

1. Create an AdMob account at [AdMob Console](https://apps.admob.com/)
2. Create a new app (iOS platform)
3. Get your **App ID** (format: `ca-app-pub-XXXXXXXXXXXXXXXX~XXXXXXXXXX`)
4. Create an **Interstitial Ad Unit** (optional)
5. Update `Liquid-Pay-Info.plist`:
   - Add `GADApplicationIdentifier` with your App ID
   - Optionally add `GADInterstitialAdUnitID` with your Ad Unit ID

**Template file:** See `Liquid-Pay-Info.plist.template` for reference structure

**Location:** Place `Liquid-Pay-Info.plist` in the root directory

### 6. Build and Run

1. Open the workspace (not the project):
   ```bash
   open "Liquid Pay.xcworkspace"
   ```

2. Select your development team in Xcode:
   - **Signing & Capabilities** → Select your team
   - Ensure Bundle Identifier matches: `com.rishiselarka.Liquid-Pay`

3. Build and run on simulator or device (⌘R)

## 📁 Project Structure

```
Liquid Pay/
├── Liquid Pay/
│   ├── Models/          # Data models
│   ├── Views/           # SwiftUI views
│   ├── ViewModels/      # ViewModels (MVVM)
│   ├── Services/        # Service layers
│   └── Utilities/       # Helper utilities
├── functions/           # Firebase Cloud Functions
│   └── src/
│       ├── index.ts    # Main functions file
│       └── pci.ts      # PCI calculation logic
├── GoogleService-Info.plist.template
├── Liquid-Pay-Info.plist.template
└── README.md
```

## 🔐 Security Notes

- **Never commit** `GoogleService-Info.plist` or `Liquid-Pay-Info.plist` files
- These files are excluded via `.gitignore`
- Always use template files for reference
- Keep your API keys and secrets secure
- Use Firebase Functions secrets for sensitive backend credentials

## 🚀 Deployment

### Deploy Firebase Functions

```bash
cd functions
npm install
firebase deploy --only functions
```

### Build for Production

1. In Xcode, select **Product** → **Archive**
2. Upload to App Store Connect
3. Submit for review

## 📝 Configuration Files

All configuration files should be placed in the root directory:
- `GoogleService-Info.plist` (also in `Liquid Pay/` directory)
- `Liquid-Pay-Info.plist`

Use the `.template` files as reference for the required structure.

## 🎯 Features

- **Authentication**: Phone number-based OTP verification
- **Payments**: UPI payments via Razorpay integration
- **Bills**: Create, manage, and pay bills with reminders
- **Transactions**: Complete transaction history with search
- **Rewards**: Gamified rewards system with Liquid Coins
- **Currency Tracking**: Real-time currency exchange rates
- **PCI Score**: Payment Consistency Index tracking
- **QR Scanner**: Scan QR codes for quick payments
- **Notifications**: Bill reminders and payment updates

## 📄 License

This project is developed for educational/demonstration purposes.

---

**Developed with ❤️ by Rishi Selarka**
