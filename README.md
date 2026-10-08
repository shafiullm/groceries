# Grocery list: free hosting with a database

Two free services:

- **Firebase (Google)** keeps the list data and handles sign-in. Spark plan, no card needed.
- **Vercel** hosts the page itself. Hobby plan, no card needed, for personal use.

Files in this folder:

- `index.html` is the whole app.
- `firestore.rules` decides who may read and change the list.

## 1. Create the Firebase project

1. Go to https://console.firebase.google.com and sign in with your Google account.
2. Click **Create a project**. Name it `groceries`. You can turn Google Analytics off.
3. On the project home page, click the **</>** (Web) icon to add a web app. Name it `groceries-web`. Leave "Firebase Hosting" unticked.
4. Firebase shows a block called `firebaseConfig`. Copy the six lines inside the curly brackets (apiKey, authDomain, projectId, storageBucket, messagingSenderId, appId).
5. Open `index.html` in a text editor (Notepad or VS Code), find `const FIREBASE_CONFIG = {`, and paste those lines inside it in place of the commented lines. Save.

These keys are not secret. They only identify your project. The rules in step 3 are what protect the data.

## 2. Turn on the database

1. In the left menu, open **Build > Firestore Database** and click **Create database**.
2. Choose a location in Europe, for example `eur3 (europe-west)` or `europe-west3 (Frankfurt)`.
3. Start in **production mode**.

## 3. Lock it to your accounts

1. In Firestore, open the **Rules** tab.
2. Delete everything there and paste in the contents of `firestore.rules`.
3. Replace the two email addresses with the Google accounts that should use the list.
4. Click **Publish**.

## 4. Turn on Google sign-in

1. Open **Build > Authentication > Get started**.
2. Under **Sign-in method**, choose **Google**, switch it on, pick your support email and click **Save**.

## 5. Put the page on Vercel

1. Make an account at https://vercel.com with "Continue with GitHub" or with your email.
2. Easiest path, no GitHub needed: install Node.js from https://nodejs.org, then open a terminal in this folder and run:

   ```
   npx vercel deploy --prod
   ```

   Answer the questions with the defaults. At the end Vercel prints your address, for example `https://groceries-abc.vercel.app`.

3. Alternative path: put this folder in a GitHub repository, then on Vercel click **Add New > Project**, pick the repository and click **Deploy**. Every change you push to GitHub then updates the site.

## 6. Allow your Vercel address to sign in

1. Back in Firebase, open **Authentication > Settings > Authorized domains**.
2. Click **Add domain** and add your Vercel address without `https://`, for example `groceries-abc.vercel.app`.

## 7. First use

1. Open your Vercel address on your phone and tap **Sign in with Google**.
2. The list is empty the first time. Tap **Load starter list**.
3. On the phone, use **Add to Home Screen** from the browser menu so it opens like an app.

## Good to know

- Without a config in `index.html`, the page still works and saves on that one device only. That is handy for testing.
- To keep a second, separate list (for example one for Suan), change `const LIST_ID = "home";` to another word and deploy that copy too.
- Free limits are far above what one household uses: about 1 GB of data, 50,000 reads and 20,000 writes per day on Firestore, and 100 GB of traffic per month on Vercel.
- Vercel's free plan is for personal, non-commercial use. If you ever want to sell this as a product, you would need a paid plan.
