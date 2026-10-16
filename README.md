# Warehouse Asset Desk

A small warehouse system for loaning out assets.

- **Store managers** create assets, locations and user accounts. They approve loans, inspect returns and download inventory reports.
- **Staff** search for assets, request them, accept them when approved, and return them.

The website is hosted free on **GitHub Pages**. Logins and data are kept in **Firebase**, Google's free database service. Firebase checks every login and every change on its own servers, so nobody can get around the login.

---

## What's in this folder

| File | What it is | Upload to GitHub? |
|---|---|---|
| `index.html` | The desk itself | Yes |
| `firebase-config.js` | Tells the desk which Firebase project to use. **You fill this in (step 5).** | Yes |
| `firestore.rules` | The database security rules. **You paste these into Firebase (step 4).** | Yes, as a record |
| `README.md` | This guide | Yes |

Your asset list is in a separate file, `wms-data-export.json`. **Do not upload it to GitHub.** GitHub Pages sites are public on the free plan, and the list contains unreleased product names. You'll load it straight into the desk in step 11.

Allow about 20 minutes. You only need a web browser.

---

## Part 1: Firebase (the database and logins)

### Step 1. Create a Firebase project
1. Go to **https://console.firebase.google.com** and sign in with a Google account. Use one your team can keep long term, such as a shared work account.
2. Click **Create a project** (or **Add project**).
3. Name it, e.g. `warehouse-asset-desk`. Click **Continue**.
4. Turn **Google Analytics off**. Click **Create project**, wait, then click **Continue**.

### Step 2. Turn on email and password logins
1. In the left menu: **Build → Authentication → Get started**.
2. Under **Sign-in method**, click **Email/Password**.
3. Switch on the first toggle (**Email/Password**). Leave "Email link" off. Click **Save**.

### Step 3. Create the database
1. Left menu: **Build → Firestore Database → Create database**.
2. Location: choose **asia-southeast1 (Singapore)**. You can't change this later.
3. Choose **Start in production mode**. Click **Create**.

### Step 4. Publish the security rules
1. In Firestore Database, open the **Rules** tab.
2. Delete everything in the editor.
3. Open `firestore.rules` from this folder in Notepad (Windows) or TextEdit (Mac). Copy all of it and paste it into the editor.
4. Click **Publish**. If Firebase shows a red error, stop and send me a screenshot.

### Step 5. Connect the desk to your project
1. Click the **gear icon ⚙ → Project settings** (top of the left menu).
2. Under **Your apps**, click the **web icon `</>`**.
3. App nickname: `Warehouse Asset Desk`. **Leave "Firebase Hosting" unticked.** Click **Register app**.
4. Firebase shows a code box. Find the part that starts with `const firebaseConfig = {` and ends with `};`. Copy just that part.
5. Open `firebase-config.js` from this folder in Notepad or TextEdit. Select the example block, from `const firebaseConfig = {` down to `};`, and paste yours over it. Keep the last line, `window.FIREBASE_CONFIG = firebaseConfig;`. Save the file.

   It's fine for these values to be public. They only point to your project. The rules from step 4 are what protect the data.

---

## Part 2: GitHub (the website)

### Step 6. Create a repository
1. Go to **https://github.com** and sign in, or create a free account.
2. Click **+ (top right) → New repository**.
3. Name: `warehouse-asset-desk`. Choose **Public**, because free GitHub Pages needs a public repository. Only the code is public. Your data stays in Firebase behind the login.
4. Click **Create repository**.

### Step 7. Upload the files
1. On the new repository page, click **uploading an existing file**.
2. Drag in **index.html, firebase-config.js, firestore.rules and README.md**. Don't upload `wms-data-export.json`.
3. Click **Commit changes**.

### Step 8. Turn on the website
1. In the repository: **Settings → Pages** (left menu).
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder **/ (root)**. Click **Save**.
4. Wait 1–2 minutes and refresh. The page shows your site address, e.g. `https://your-name.github.io/warehouse-asset-desk/`.

---

## Part 3: Connect and start

### Step 9. Allow your website in Firebase
1. Firebase console → **Authentication → Settings → Authorized domains → Add domain**.
2. Enter just the domain part of your site address, e.g. `your-name.github.io`. No `https://`, no slashes. Click **Add**.

### Step 10. Create the store manager account. Do this straight away.
1. Open your site address.
2. You'll see **Set up the store manager account**. Enter your name, work email and a password.

The first person to do this becomes the store manager, so do it as soon as the site is live.

### Step 11. Load your assets
1. In **Manager → Assets**, find **Import or export assets**.
2. Choose `wms-data-export.json` and click **Import file**. Your 38 assets and the BYS_KL OFFICE location appear.

### Step 12. Create staff accounts
1. **Manager → Accounts**. Enter the person's name and **work email**, pick a role, and click **Generate** for a temporary password.
2. Click **Create account**, then **Copy details** and send them to the person.
3. They log in, choose their own password, and can start requesting assets.

---

## Day-to-day

- **Forgotten password:** in **Accounts**, click **Reset password**. Firebase emails them a link to set a new one. It comes from `noreply@<your-project>.firebaseapp.com`, so ask them to check spam.
- **Someone leaves:** in **Accounts**, click **Disable**. They can't log in any more, and their history stays.
- **Backups:** in **Assets → Import or export assets**, click **Export data** now and then and keep the file somewhere safe.
- **Updating the desk:** when I give you a new `index.html`, open the repository on GitHub and click **Add file → Upload files**. Drop in the new file and commit. The site updates within a couple of minutes. Your data in Firebase is not affected.

## If something goes wrong

| What you see | What to do |
|---|---|
| "This copy of the desk isn't connected to a database yet" | `firebase-config.js` still has the example values. Redo step 5 and upload the file again. |
| "This website isn't on Firebase's list of allowed sites" | Do step 9. Check the domain has no `https://` or `/`. |
| "Email/password login isn't switched on" | Do step 2. |
| "Firebase refused this…" or a blank list after logging in | The rules aren't published. Redo step 4. |
| Changes don't show after uploading a new file | Wait two minutes, then reload the page with Ctrl+F5 (Windows) or Cmd+Shift+R (Mac). |

## Costs and limits

The free Firebase **Spark** plan covers 50,000 database reads and 20,000 writes per day, which is far more than a warehouse team needs. GitHub Pages is free. No credit card is needed for either.
