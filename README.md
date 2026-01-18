# UNC Marketplace (Mobile App)

A mobile-first marketplace built with **Expo + React Native (TypeScript)**, designed for the UNC community. The app enables users to discover listings through a swipe-based feed, create and manage listings, message other users, and participate in community chat — all backed by Firebase.

> Currently run locally via Expo (screenshots taken from Expo Go).

---

## Features

- **UNC-only authentication**
  - Email-based sign up restricted to `@unc.edu`
  - Email verification and secure authentication via Firebase Auth

- **Discover (Swipe) Feed**
  - Swipe left/right on public listings
  - Save interest, increment engagement counters
  - Quick-compose modal to message sellers directly from the feed

- **Listings**
  - Create listings with images, price, category, condition, and description
  - Firebase Storage for image uploads
  - Firestore-backed listing persistence
  - View detailed listing pages and seller info

- **Messaging**
  - One-to-one direct messaging between buyers and sellers
  - Community-wide chat
  - Push notification support with deep-link routing into chats

- **Wishlist / Saves**
  - Save listings for later
  - Firestore-backed tracking for views and saves

---

## Tech Stack

### Frontend
- Expo SDK
- React Native + TypeScript
- `expo-router` for file-based navigation
- `react-native-reanimated`
- Expo modules:
  - `expo-image-picker`
  - `expo-notifications`
  - `expo-constants`

### Backend
- Firebase
  - Authentication
  - Firestore
  - Storage
  - Cloud Functions
- Firebase Admin SDK (Cloud Functions)

### Tooling
- TypeScript
- ESLint
- Expo CLI

---

## App Structure & Navigation

Routing is handled with **expo-router**, organized using route groups:

app/

├── (auth)/ # Auth flows (sign up, login, verify)

├── (tabs)/ # Main tab navigation

│ ├── index.tsx # Discover / Swipe feed

│ ├── add-listing.tsx

│ └── _layout.tsx # Custom tab bar

├── listing/ # Listing detail & edit routes

├── chat/ # Messaging threads

└── _layout.tsx # Root router & auth integration

markdown
Copy code

- Auth state is provided via `AuthProvider` (`AuthContext.tsx`)
- Firebase initialization and persistence are configured in `firebase.ts`
- Push notification routing is set up in `_layout.tsx`

---

## UI & Design

- Custom components:
  - `SwipeDeck`
  - `QuickComposeModal`
  - `LiquidGlassTabBar`
- Centralized design tokens in `theme.ts`
- Modern dark theme with smooth animations and consistent spacing

---

## Backend & Data Model

- **Firestore collections**
  - users
  - listings
  - conversations
  - messages
  - saves / views / notifications

- **Firebase Storage**
  - Listing image uploads

- **Cloud Functions**
  - Located in `/functions`
  - Separate TypeScript build pipeline and `package.json`
  
  In addition to Firebase services, the app integrates a custom **Spring Boot backend** that provides a secure API layer for handling protected operations.

- Implemented **JWT-based authentication** to enable stateless request handling
- Built **RESTful APIs** in Spring Boot with fine-grained access control
- Integrated the backend with **Firestore** for secure data access and validation
- Designed the API layer to support scalable authorization beyond client-side Firebase rules
---

## Getting Started (Local Development)

### 1. Install dependencies
```bash
npm install

### 2. Start Expo
npm run start

Platform-specific:

npm run android
npm run ios
npm run web

### 3. Environment Variables

Set the following Expo public environment variables (used in firebase.ts):

EXPO_PUBLIC_FIREBASE_API_KEY
EXPO_PUBLIC_FIREBASE_AUTH_DOMAIN
EXPO_PUBLIC_FIREBASE_PROJECT_ID
EXPO_PUBLIC_FIREBASE_STORAGE_BUCKET
EXPO_PUBLIC_FIREBASE_MESSAGING_SENDER_ID
EXPO_PUBLIC_FIREBASE_APP_ID

You can configure these using .env, app.config.js, or your preferred Expo env setup.

Cloud Functions
cd functions
npm install
npm run build
npm run serve    # Firebase emulator (requires Firebase CLI)
# or
npm run deploy
