# 🔐 Google OAuth 2.0 Setup Complete Guide for MedFlow Pro

## ✅ **Step 1: Create Google Cloud Project** (Already Done ✓)

You should have:
- ✓ OAuth Client ID: `YOUR_GOOGLE_CLIENT_ID`
- ✓ Client Secret: `YOUR_CLIENT_SECRET` (keep this safe!)

---

## 📋 **Step 2: Configure Your Domain**

### **For Local Testing (Development)**
```
Authorized JavaScript Origins:
  - http://localhost:3000
  - http://localhost:8000
  - http://127.0.0.1:5500

Authorized Redirect URIs:
  - http://localhost:3000/auth/callback
  - http://localhost:8000/auth/callback
```

### **For Production (Live Website)**
```
Authorized JavaScript Origins:
  - https://yourdomain.com
  - https://www.yourdomain.com

Authorized Redirect URIs:
  - https://yourdomain.com/auth/callback
  - https://yourdomain.com/oauth2/callback
```

---

## 🔧 **Step 3: Add Your Client ID to Code**

Open `medflow-pro-v2.html` and find this line (around line 250):

```javascript
const GOOGLE_CLIENT_ID = 'YOUR_GOOGLE_CLIENT_ID.apps.googleusercontent.com';
```

**Replace it with YOUR actual Client ID:**

```javascript
const GOOGLE_CLIENT_ID = '123456789-abcdefghijklmnop.apps.googleusercontent.com';
```

### Where to find your Client ID:
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Navigate to **APIs & Services > Credentials**
3. Find your "Web application" credential
4. Click the copy icon next to the Client ID
5. Paste it in the code above

---

## 🚀 **Step 4: Choose Your Deployment Method**

### **Option A: GitHub Pages (Easiest - FREE)**

1. Push your `medflow-pro-v2.html` to GitHub repo
2. Go to **Settings > Pages**
3. Enable **GitHub Pages** from main branch
4. Your site will be: `https://yourusername.github.io/inicetrevisionplanner`

**Then update Google Console:**
```
Authorized JavaScript Origins:
  - https://yourusername.github.io

Authorized Redirect URIs:
  - https://yourusername.github.io/inicetrevisionplanner/auth/callback
```

### **Option B: Netlify (Recommended - FREE)**

1. Go to [Netlify](https://netlify.com)
2. Click "New site from Git" → Connect GitHub
3. Select your repo
4. Deploy (automatic)
5. Your site will be: `https://yourname.netlify.app`

**Then update Google Console:**
```
Authorized JavaScript Origins:
  - https://yourname.netlify.app

Authorized Redirect URIs:
  - https://yourname.netlify.app/auth/callback
```

### **Option C: Vercel (Premium - FREE tier)**

1. Go to [Vercel](https://vercel.com)
2. Import your GitHub repo
3. Deploy (automatic)
4. Your site will be: `https://yourname.vercel.app`

**Then update Google Console:**
```
Authorized JavaScript Origins:
  - https://yourname.vercel.app

Authorized Redirect URIs:
  - https://yourname.vercel.app/auth/callback
```

### **Option D: Your Own Domain**

```
Authorized JavaScript Origins:
  - https://medflow.yourdomain.com

Authorized Redirect URIs:
  - https://medflow.yourdomain.com/auth/callback
```

---

## 🧪 **Step 5: Test Locally (Development)**

1. Install a local server:
```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (if installed)
npx http-server

# Using PHP (if installed)
php -S localhost:8000
```

2. Open: `http://localhost:8000/medflow-pro-v2.html`
3. Click **"Sign in with Google"** button
4. You should see Google's login popup

**If you get "Redirect URI mismatch" error:**
- Check you added `http://localhost:8000/auth/callback` to Google Console

---

## ⚙️ **Step 6: Update Google Console with Your Domain**

### **Go to Google Cloud Console:**
1. [Google Cloud Console](https://console.cloud.google.com)
2. Click your project name (top left)
3. Go to **APIs & Services > Credentials**
4. Click your "Web application" credential
5. Click **Edit**
6. Scroll to "Authorized JavaScript origins" → **Add URI**
7. Paste your production domain
8. Scroll to "Authorized redirect URIs" → **Add URI**
9. Paste your callback URL
10. Click **Save**

---

## 🎯 **Step 7: What Happens After Login**

When user clicks **"Sign in with Google"**:

1. ✅ Google popup opens
2. ✅ User logs in with Google account
3. ✅ Google redirects back to your app
4. ✅ App stores `user.email` in localStorage
5. ✅ App shows user avatar & name
6. ✅ User data syncs to Google Drive (if backend configured)

---

## 💾 **Step 8: Backend Setup (Optional - For Cloud Sync)**

Currently the app only does **LOCAL storage**. To enable **cloud sync**, you need a backend:

### **Option 1: Firebase (Easiest)**
```html
<script src="https://www.gstatic.com/firebasejs/10.0.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.0.0/firebase-auth.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.0.0/firebase-database.js"></script>
```
- Go to [Firebase Console](https://console.firebase.google.com)
- Create project, enable Auth & Realtime Database
- Copy your config

### **Option 2: Custom Node.js Backend**
```javascript
// server.js
const express = require('express');
const { google } = require('googleapis');

app.post('/api/sync', (req, res) => {
  // Save user data to database
  // Verify Google token
  // Store encrypted data
});
```

### **Option 3: Google Sheets API**
- Store revision data directly to Google Sheets
- User can view data in spreadsheet format

---

## 🔒 **Security Checklist**

- ✅ Never expose `Client Secret` in HTML
- ✅ Always use HTTPS in production
- ✅ Set restrictive Authorized Origins
- ✅ Rotate credentials every 6 months
- ✅ Use environment variables for Client ID (on backend)

---

## ✨ **Final Checklist**

- [ ] Created Google Cloud Project
- [ ] Enabled OAuth consent screen (External)
- [ ] Created Web application credential
- [ ] Copied Client ID
- [ ] Updated Client ID in `medflow-pro-v2.html`
- [ ] Added Authorized Origins in Google Console
- [ ] Added Authorized Redirect URIs in Google Console
- [ ] Deployed to production (GitHub Pages/Netlify/Vercel)
- [ ] Updated Google Console with production domain
- [ ] Tested login flow locally
- [ ] Tested login flow on production
- [ ] (Optional) Set up Firebase for cloud sync

---

## 🆘 **Common Issues & Fixes**

### **"Redirect URI mismatch"**
- Check Google Console has exact redirect URI
- Ensure HTTPS matches (http vs https)

### **"OAuth redirect_uri_mismatch"**
- Probably using localhost but Google Console only has production domain
- Add `http://localhost:8000/auth/callback` to Google Console

### **"Access blocked"**
- App is in testing mode → add yourself as test user in Google Console
- Or set app to "Production" (requires security review for new apps)

### **Login button doesn't work**
- Client ID is wrong → copy again from Google Console
- JavaScript console shows errors → check browser DevTools

### **User data not syncing**
- Local storage is working fine (check localStorage in DevTools)
- For cloud sync, need to implement backend

---

## 📚 **Resources**

- [Google OAuth 2.0 Docs](https://developers.google.com/identity/protocols/oauth2)
- [Google Cloud Console](https://console.cloud.google.com)
- [Firebase Setup](https://firebase.google.com/docs/auth/get-started)
- [Google Sign-In for Web](https://developers.google.com/identity/sign-in/web)

---

## 🎉 **You're All Set!**

Your MedFlow Pro app is now ready for production with Google OAuth login! 🚀

