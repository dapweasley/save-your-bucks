# Quick Deployment Guide

## Ready-to-Deploy Package

Your `saveyobucks-app.zip` file contains everything needed to deploy the savings tracker application.

## Firebase Setup (Required)

1. **Create Firebase Project**
   - Go to https://console.firebase.google.com/
   - Create a new project named "saveyobucks"
   - Enable Email/Password authentication
   - Create Firestore database in production mode

2. **Update Environment Variables**
   - Extract the zip file
   - Edit `.env.local` with your Firebase configuration
   - Run `npm install` to install dependencies
   - Run `npm run build` to build the project

## Netlify Deployment

### Option 1: Drag & Drop
1. Go to https://netlify.com
2. Drag and drop the entire extracted folder
3. Add environment variables in Netlify dashboard

### Option 2: Git Integration
1. Push code to GitHub/GitLab
2. Connect repository to Netlify
3. Build command: `npm run build`
4. Publish directory: `.next`
5. Add environment variables

## Environment Variables to Add in Netlify

```
NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_auth_domain
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_storage_bucket
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=your_measurement_id
```

## Firestore Security Rules

Add these rules in Firebase Console > Firestore > Rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Testing Checklist

- [ ] User registration works
- [ ] User login works
- [ ] Adding savings goals works
- [ ] Making deposits works
- [ ] Progress tracking updates in real-time
- [ ] Responsive design works on mobile
- [ ] Logout functionality works

## Support

For issues, check the README.md file or open an issue in the repository.
