# CallVerse (crypto-caller)

> **Free, secure, peer-to-peer audio and video calling across Web, Android, and Desktop.**

CallVerse is a modern, cross-platform communication platform engineered for ultra-low latency real-time voice and video conversations using WebRTC, Socket.IO signaling, and native mobile/desktop integrations.

---

## ✨ Features

- 📞 **Peer-to-Peer Calls**: Direct audio and video streams powered by WebRTC with adaptive quality and encrypted peer connections.
- ⚡ **Real-Time Signaling**: Low-latency session negotiation, ICE candidate exchange, and presence handling with Socket.IO.
- 🔔 **Native Android Incoming Calls**: Custom Android Capacitor plugins for background wake-ups, full-screen incoming call UI, native ringtones, and audio routing.
- 📲 **Push Notifications (FCM)**: Reliable background incoming call alerts via Firebase Cloud Messaging even when the application is completely closed.
- 🔐 **Authentication**: Fast and secure authentication powered by Firebase Authentication.
- 🖥️ **Cross-Platform Support**:
  - **Web**: Responsive React SPA built with Vite.
  - **Android**: Native wrapper with Capacitor.
  - **Desktop**: Electron integration with multi-OS build targets (Windows, macOS, Linux).
- 🎨 **Modern Interface**: Fluid animations, customizable themes (Dark/Light), and responsive layout with Zustand and Lucide icons.

---

## 🛠️ Tech Stack

### Frontend & Client
- **Framework**: React 19 + Vite
- **State Management**: Zustand
- **Real-Time / Media**: WebRTC, Socket.IO Client
- **Mobile Runtime**: Capacitor (Android native plugins for Ringtone, AudioRoute, and Push)
- **Desktop Runtime**: Electron
- **Authentication**: Firebase Authentication
- **Icons & Styling**: Lucide React, CSS Variables & Tokens

### Backend Signaling Server
- **Runtime**: Node.js (ES Modules)
- **Framework**: Express
- **Signaling Protocol**: Socket.IO
- **Database**: SQLite / Turso (`@libsql/client`, `better-sqlite3`)
- **Notifications**: Firebase Admin SDK (FCM)

---

## 📁 Project Structure

```
crypto-caller/
├── android/                 # Native Android project (Capacitor)
│   └── app/src/main/java/   # Native Android Plugins (AudioRoute, Ringtone, CallMessagingService)
├── electron/                # Electron main and preload scripts
├── public/                  # Static assets, icons, manifest
├── server/                  # Node.js + Socket.IO signaling server
│   ├── index.js             # Server entry point & socket events
│   ├── db.js                # Database connection & migrations
│   └── package.json         # Backend dependencies
├── src/                     # React Frontend source
│   ├── components/          # UI Screens (Auth, CallScreen, Dashboard, etc.)
│   ├── hooks/               # Custom hooks (useWebRTC, usePushNotifications)
│   ├── utils/               # Socket & Ringtone utilities
│   ├── App.jsx              # Main application router and call listener
│   └── main.jsx             # React DOM root
├── capacitor.config.json    # Capacitor configuration
├── package.json             # Root frontend dependencies & scripts
└── vite.config.js           # Vite build configuration
```

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v18 or higher recommended)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [Android Studio](https://developer.android.com/studio) (for Android build)
- Firebase Project credentials (for Authentication & Push Notifications)

---

### 1. Clone the Repository
```bash
git clone https://github.com/Adityaprajapati18/crypto-caller.git
cd crypto-caller
```

---

### 2. Configure Environment & Firebase

#### Client Configuration
Create or update `src/firebase.js` with your Firebase project configuration:
```javascript
import { initializeApp } from 'firebase/app';
import { getAuth } from 'firebase/auth';

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID"
};

export const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
```

#### Server Configuration
Navigate to `server/`, create a `.env` file, and provide your Firebase Admin service account:
```env
PORT=5000
DATABASE_URL=file:local.db
# Optional Turso auth token if using remote Turso database:
# TURSO_AUTH_TOKEN=your_token
```

---

### 3. Install Dependencies

#### Install Root Dependencies (Frontend):
```bash
npm install
```

#### Install Server Dependencies:
```bash
cd server
npm install
cd ..
```

---

### 4. Running the Application

#### Start the Signaling Server:
```bash
cd server
npm run dev
```

#### Start the Frontend (Web):
```bash
npm run dev
```
Open your browser and visit `http://localhost:5173`.

#### Run Desktop App (Electron):
```bash
npm run electron:dev
```

#### Run on Android:
```bash
npm run build
npx cap sync android
npx cap open android
```
*Build and run the project from Android Studio onto a physical device or emulator.*

---

## 📦 Building for Production

- **Web Build**:
  ```bash
  npm run build
  ```
- **Desktop Executable (Windows)**:
  ```bash
  npm run electron:build:win
  ```
- **Desktop Executable (Linux/macOS)**:
  ```bash
  npm run electron:build:linux   # Linux AppImage
  npm run electron:build         # macOS DMG
  ```

---

## 📄 License

This project is licensed under the MIT License.
