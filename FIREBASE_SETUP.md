# Firebase Setup Guide for Supplier Engagement Game

## Prerequisites
1. A Google account
2. Access to the Firebase Console (https://console.firebase.google.com/)

## Step 1: Create a Firebase Project

1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Click "Create a project" or "Add project"
3. Enter a project name (e.g., "supplier-engagement-game")
4. Choose whether to enable Google Analytics (optional for this project)
5. Click "Create project"
6. Wait for the project to be created

## Step 2: Set up Firestore Database

1. In your Firebase project, click on "Firestore Database" in the left sidebar
2. Click "Create database"
3. Choose "Start in test mode" (this allows read/write access for 30 days)
4. Select a location for your database (choose the closest to your event location)
5. Click "Done"

### Important: Update Firestore Security Rules

After creating the database, you'll need to update the security rules:

1. Go to the "Rules" tab in Firestore Database
2. Replace the default rules with these more specific rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow read/write access to attendees collection
    match /attendees/{badgeUid} {
      allow read, write: if true;
    }
    
    // Allow read/write access to scans collection
    match /scans/{scanId} {
      allow read, write: if true;
    }
  }
}
```

3. Click "Publish" to save the rules

## Step 3: Enable Authentication

1. Click on "Authentication" in the left sidebar
2. Click "Get started"
3. Go to the "Sign-in method" tab
4. Enable "Anonymous" authentication:
   - Click on "Anonymous"
   - Toggle "Enable"
   - Click "Save"

## Step 4: Get Your Firebase Configuration

1. Click on the gear icon (⚙️) next to "Project Overview" in the left sidebar
2. Select "Project settings"
3. Scroll down to "Your apps" section
4. Click the web icon (</>) to add a web app
5. Register your app with a nickname (e.g., "supplier-game")
6. **Do NOT** check "Also set up Firebase Hosting"
7. Click "Register app"
8. Copy the Firebase configuration object

## Step 5: Update the Application

1. Open the `index.html` file
2. Find the `firebaseConfig` object (around line 200)
3. Replace the placeholder values with your actual Firebase configuration:

```javascript
const firebaseConfig = {
    apiKey: "your-actual-api-key",
    authDomain: "your-project-id.firebaseapp.com",
    projectId: "your-actual-project-id",
    storageBucket: "your-project-id.appspot.com",
    messagingSenderId: "your-actual-sender-id",
    appId: "your-actual-app-id"
};
```

## Step 6: Test Your Setup

1. Open the `index.html` file in a web browser
2. Try logging in with a test Badge UID (e.g., "ATT001")
3. Check the Firebase Console to see if data is being created:
   - Go to Firestore Database
   - You should see collections for "attendees" and "scans"

## Step 7: Deploy to GitHub Pages (Optional)

1. Create a new repository on GitHub
2. Upload your `index.html` file
3. Go to repository Settings > Pages
4. Select "Deploy from a branch" and choose "main"
5. Your app will be available at `https://your-username.github.io/your-repo-name`

## Configuration Customization

### Adding/Modifying Suppliers
Edit the `suppliers` array in the `CONFIG` object:

```javascript
suppliers: [
    { id: 'supplier_1', name: 'Your Company Name' },
    // Add more suppliers...
]
```

### Modifying Point Values
Edit the `pointValues` object:

```javascript
pointValues: {
    checkin: 1,     // Points for basic check-in
    chat: 2,        // Points for meaningful conversation
    bonus: 3        // Points for in-depth discussion
}
```

### Adding/Modifying Attendees
Edit the `attendees` array:

```javascript
attendees: [
    { badgeUid: 'ATT001', name: 'John Doe' },
    // Add more attendees...
]
```

### Changing Admin Password
Edit the `adminPassword` value:

```javascript
adminPassword: 'your-secure-password-here', // Change this to your desired admin password
```

## Security Considerations

### For Production Use
1. **Update Firestore Rules**: The current rules allow full read/write access. For production, implement proper authentication-based rules.

2. **Validate Data**: Add server-side validation for scan data integrity.

3. **Rate Limiting**: Consider implementing rate limiting to prevent spam scans.

### Current Security Features
- Admin password protection for administrative functions
- Duplicate scan prevention (same user can't scan the same QR code twice)
- Badge UID validation against predefined list
- Anonymous authentication for session management

## Troubleshooting

### Common Issues

1. **"Firebase not initialized" error**
   - Check that your Firebase configuration is correct
   - Ensure all CDN links are loading properly

2. **"Permission denied" error**
   - Check your Firestore security rules
   - Ensure the rules allow read/write access

3. **QR scanner not working**
   - Ensure camera permissions are granted
   - Try using HTTPS (required for camera access on most browsers)

4. **Real-time updates not working**
   - Check browser console for errors
   - Verify Firestore rules allow read access

### Testing Checklist

- [ ] Can log in with valid Badge UID
- [ ] Cannot log in with invalid Badge UID
- [ ] QR scanner opens and works
- [ ] Scans are recorded in Firestore
- [ ] Leaderboard updates in real-time
- [ ] Admin password protection works
- [ ] Admin panel generates QR codes
- [ ] Duplicate scans are prevented
- [ ] Mobile interface works properly

## Support

If you encounter issues:
1. Check the browser console for error messages
2. Verify your Firebase configuration
3. Test with a simple Badge UID first (e.g., "ATT001")
4. Ensure you're using a modern browser with camera support

## Cost Considerations

This application is designed to work within Firebase's free tier limits:
- **Firestore**: 1GB storage, 50K reads/day, 20K writes/day
- **Authentication**: Unlimited anonymous users
- **Hosting**: Free on GitHub Pages

For events with more than 200 attendees or heavy usage, monitor your Firebase usage in the console.
