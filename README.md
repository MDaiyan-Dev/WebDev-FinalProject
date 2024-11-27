# **Naan Stop Wok - Restaurant Reservation System**

Welcome to the **Naan Stop Wok** project! This is a dynamic, feature-rich web application for managing reservations and providing users with an interactive experience for a fusion restaurant. It uses **Next.js**, **Firebase**, and a modern UI for seamless functionality and a visually appealing interface.

---

## **Features**

- **Dynamic Reservations System**
  - Users can view available dates and times on a calendar.
  - Reservations are tied to individual user accounts.
  - Users must be signed in to add or manage reservations.
  - Real-time updates of reservations using **Firestore**.

- **Authentication**
  - Email/Password-based sign-up and login.
  - Google OAuth integration for quick sign-in.

- **Alerts and Notifications**
  - Custom modals for errors, confirmations, and prompts (themed to match the website).

- **Calendar View**
  - Integrated calendar for easy date selection.
  - Disabled invalid dates (e.g., past dates).

- **Responsive Design**
  - Fully optimized for desktop and mobile viewing.

- **Modern UI**
  - Built with custom components and a consistent theme.

---

## **Tech Stack**

### **Frontend**
- **Next.js**: Framework for server-rendered React applications.
- **Tailwind CSS**: For styling the UI.
- **React Icons & Lucide**: For modern icons and visuals.

### **Backend**
- **Firebase Authentication**: User authentication and session management.
- **Cloud Firestore**: Database for storing user reservations.

---

## **Installation**

### **1. Clone the Repository**

```bash
git clone https://github.com/MDaiyan-Dev/WebDev-FinalProject.git
cd test
```

### **2. Install Dependencies**

Make sure you have `yarn` installed. Install the required dependencies:

```bash
yarn install
npm install -g firebase-tools
yarn add firebase
```

### **3. Set Up Firebase**

1. Log in to [Firebase Console](https://console.firebase.google.com/).
2. Create a new Firebase project.
3. Enable the following:
   - **Authentication** (Email/Password and Google OAuth).
   - **Cloud Firestore** (Create a `reservations` collection).
4. Obtain the Firebase configuration keys from the console.
5. Follow Firebase guide to install required sdk on local machine.

### **4. Create `config/firebase.js`**

Create the Firebase configuration file in `src/app/config/firebase.js`:

```javascript
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";
import { getFirestore } from "firebase/firestore";
import { GoogleAuthProvider } from "firebase/auth";

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_STORAGE_BUCKET",
  messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
  appId: "YOUR_APP_ID",
};

const app = initializeApp(firebaseConfig);
export const auth = getAuth(app);
export const db = getFirestore(app);
export const googleProvider = new GoogleAuthProvider();
```

Replace `YOUR_API_KEY` and other placeholders with your Firebase configuration.

---

## **Usage**

### **Development Mode**
Start the development server:

```bash
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) to view the app.

### **Building for Production**

```bash
yarn build
```

Serve the built app:

```bash
yarn start
```

---

## **Key Components**

### **1. Authentication**
- **File**: `src/app/components/authSignup.js`
- Handles user sign-up/login using Firebase Authentication.
- Includes Google OAuth and email/password sign-up.

### **2. Reservation System**
- **Files**:
  - `src/app/reservations/page.js`
  - `src/app/components/reservation-modal.js`
  - `src/app/components/calendar.js`
- Core reservation logic tied to user accounts.
- Displays reservations in a calendar format.
- Prevents selecting invalid dates (e.g., past dates).

### **3. Alert Modals**
- **File**: `src/app/components/AlertModal.js`
- Custom modals for error messages, prompts, and confirmations.

### **4. Navbar**
- **File**: `src/app/components/navbar.js`
- Responsive navigation bar with dynamic sign-in/out behavior.

---

## **Firestore Rules**

Ensure proper security rules are set up in Firestore for user-specific data access:

```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /reservations/{reservationId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.uid;
    }
  }
}
```
or use an empty test setup if the above does not work
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
---

## **Contributing**

We welcome contributions to improve this project. Please fork the repository and create a pull request.

## Top Contributors 

Daiyan
Logan 
Krishna
Easha
Rubab

---

## **License**

This project is licensed under the MIT License.

---

## **Contact**

For any inquiries, reach out to us:

- **Email**: daiyan.mohammad.offc@gmail.com

