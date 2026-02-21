# Antigravity Engine 🚀

The Antigravity Engine is a lightweight, serverless AI chat application designed to "lift cognitive load." It leverages the lightning-fast Groq API for inference, Firebase for seamless Google Sign-In and chat logging, and Vercel for secure backend execution and hosting.

## ✨ Features

* **High-Speed AI Inference:** Powered by Groq (Mixtral 8x7b / Llama 3) for near-instant responses.
* **Custom Persona:** Pre-configured with the "Antigravity" system prompt, optimized for theoretical physics, engineering, and workflow unblocking.
* **Rich Math Rendering:** Integrates MathJax to perfectly render complex LaTeX equations (e.g., $$E = mc^2$$).
* **Secure Authentication:** Google Sign-In via Firebase Auth.
* **Chat Logging:** Stores user queries in Google Firestore for history and analysis.
* **Serverless Architecture:** Uses Vercel Serverless Functions to securely hide the Groq API key from the client side.

## 🛠 Tech Stack

* **Frontend:** HTML5, Tailwind CSS (CDN), Vanilla JavaScript
* **Backend:** Node.js (Vercel Serverless Functions)
* **Database & Auth:** Google Firebase (Firestore, Firebase Auth)
* **AI SDK:** `groq-sdk`

## 📂 Project Structure

\`\`\`text
antigravity-project/
├── api/
│   └── chat.js          # Vercel serverless function (Groq API bridge)
├── index.html           # Main frontend UI and Firebase logic
├── package.json         # Project dependencies (groq-sdk)
└── README.md            # Project documentation
\`\`\`

## 🚀 Setup & Installation

### 1. Prerequisites
* [Node.js](https://nodejs.org/) installed on your machine.
* A [Groq Cloud](https://console.groq.com/) account and API Key.
* A [Firebase](https://console.firebase.google.com/) project.
* A [Vercel](https://vercel.com/) account.

### 2. Firebase Configuration
1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.
2. Navigate to **Authentication**, click "Get Started", and enable the **Google** sign-in provider.
3. Navigate to **Firestore Database** and create a database (Start in test mode or configure security rules to allow writes only from authenticated users).
4. Go to Project Settings > General, scroll down to "Your apps", and register a new Web App.
5. Copy your Firebase config object and replace the placeholder in `index.html`:

\`\`\`javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "SENDER_ID",
    appId: "APP_ID"
};


### 3. Local Setup
Create a new directory for your project and add the files (`index.html`, `api/chat.js`, `package.json`).

Install the required dependencies for the backend:
\`\`\`bash
npm install
\`\`\`

### 4. Deployment (Vercel)
To deploy this project securely and make the serverless functions work, you must host it on Vercel.

1. Install the Vercel CLI globally:
   \`\`\`bash
   npm install -g vercel
   \`\`\`
2. Run the deployment command from the root of your project directory:
   \`\`\`bash
   vercel
   \`\`\`
   *(Follow the CLI prompts to link your project).*

### 5. Add Environment Variables
Your Groq API key must remain a secret. **Do not put it in your HTML.**

1. Go to your Vercel Dashboard -> Select your project -> Settings -> Environment Variables.
2. Add a new variable:
   * **Key:** `GROQ_API_KEY`
   * **Value:** `your_actual_groq_api_key_here`
3. Redeploy your project to apply the environment variables:
   \`\`\`bash
   vercel --prod
   \`\`\`

## 🔒 Security Note
Ensure your Firestore Security Rules are set to prevent unauthorized writes. A basic secure rule for this app looks like:

\`\`\`javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /logs/{logId} {
      // Only allow users to write if they are signed in and their UID matches the document
      allow create: if request.auth != null && request.resource.data.uid == request.auth.uid;
      allow read, update, delete: if false; // Deny all other actions
    }
  }
}
\`\`\`






**Project File**
https://github.com/sai-10-15/codeforu.git
