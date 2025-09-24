# Supplier Engagement Game 🎮

A gamified web application designed to encourage meaningful interactions between event attendees and suppliers through QR code scanning and real-time leaderboards.

## 🚀 Features

### For Attendees
- **Mobile-first interface** optimized for smartphones
- **Badge UID authentication** - simple login with event badge
- **QR code scanning** with camera integration
- **Real-time scoring** with instant feedback
- **Live leaderboard** showing top performers
- **Personal scan history** tracking interactions
- **Duplicate prevention** - can't scan the same QR code twice

### For Admins
- **Password-protected access** to admin functions
- **QR code generation** for all 24 suppliers and interaction types
- **Live leaderboard monitoring** with admin view
- **Data management** including reset functionality
- **Print-friendly QR codes** for supplier distribution

### For Suppliers
- **Three interaction types** with different point values:
  - Check-In: 1 point (basic hello)
  - Chat: 2 points (meaningful conversation)
  - Bonus: 3 points (in-depth discussion)

## 🏗️ Technical Architecture

### Single File Application
- **Complete solution** in one HTML file
- **No build process** required
- **CDN dependencies** for easy deployment

### Technology Stack
- **Frontend**: HTML5, CSS3 (Tailwind CSS), Vanilla JavaScript
- **Backend**: Firebase (Firestore, Authentication)
- **QR Code Generation**: QRCode.js library
- **QR Code Scanning**: html5-qrcode library
- **Real-time Updates**: Firestore listeners

### Data Structure
```
/attendees/{badgeUid}
├── name: "Jane Doe"
├── score: 450
└── createdAt: timestamp

/scans/{scanId}
├── badgeUid: "ATTENDEE001"
├── supplierId: "supplier_name_5"
├── scanType: "excellent"
├── points: 100
└── timestamp: timestamp
```

## 📱 User Experience

### Attendee Journey
1. **Login** with Badge UID from event badge
2. **Visit supplier booth** and have conversation
3. **Scan appropriate QR code** based on interaction quality
4. **Receive instant feedback** with points awarded
5. **View progress** on personal dashboard and leaderboard

### Admin Workflow
1. **Access admin panel** with password authentication
2. **Generate QR codes** for all suppliers and interaction types
3. **Print and distribute** QR codes to suppliers
4. **Monitor live leaderboard** during event
5. **Manage data** as needed

## 🎯 Configuration

The application is easily configurable for different events by modifying the `CONFIG` object:

```javascript
const CONFIG = {
    adminPassword: 'admin123', // Change this to your desired admin password
    suppliers: [
        { id: 'supplier_1', name: 'TechCorp Solutions' },
        // ... 24 suppliers total
    ],
    pointValues: {
        checkin: 1,
        chat: 2,
        bonus: 3
    },
    attendees: [
        { badgeUid: 'ATT001', name: 'Jane Doe' },
        // ... all event attendees
    ]
};
```

## 🚀 Quick Start

### Prerequisites
- Firebase account
- Modern web browser with camera support
- HTTPS hosting (required for camera access)

### Setup Steps
1. **Create Firebase project** and enable Firestore + Authentication
2. **Update Firebase configuration** in the HTML file
3. **Configure your event data** (suppliers, attendees, points)
4. **Deploy to web hosting** (GitHub Pages recommended)
5. **Generate and print QR codes** via admin panel

### Detailed Setup
See [FIREBASE_SETUP.md](FIREBASE_SETUP.md) for comprehensive setup instructions.

## 📊 Event Statistics

### Designed For
- **~200 attendees** with unique Badge UIDs
- **24 suppliers** with 3 interaction types each
- **72 unique QR codes** total (24 suppliers × 3 types)
- **Real-time leaderboard** updates
- **Mobile-first experience** for easy scanning
- **Consistent QR generation** - same codes every time

### Scalability
- Firebase free tier supports up to 200 concurrent users
- Firestore handles real-time updates efficiently
- QR code scanning works on all modern mobile browsers

## 🔒 Security Features

- **Badge UID validation** against predefined attendee list
- **Duplicate scan prevention** per user per QR code
- **Anonymous authentication** for session management
- **Real-time data validation** in Firestore
- **Client-side duplicate checking** for immediate feedback

## 🎨 UI/UX Features

- **Tailwind CSS** for modern, responsive design
- **Mobile-first approach** with touch-friendly buttons
- **Real-time updates** without page refreshes
- **Visual feedback** for successful scans
- **Clean typography** optimized for readability
- **Professional color scheme** suitable for corporate events

## 📱 Browser Compatibility

### Supported Browsers
- Chrome (recommended)
- Firefox
- Safari
- Edge

### Mobile Requirements
- Camera access permissions
- HTTPS connection (required for camera)
- Modern JavaScript support

## 🚀 Deployment Options

### GitHub Pages (Recommended)
1. Upload `index.html` to GitHub repository
2. Enable Pages in repository settings
3. Access via `https://username.github.io/repository-name`

### Firebase Hosting
1. Install Firebase CLI
2. Run `firebase deploy`
3. Access via Firebase hosting URL

### Any Web Host
- Upload `index.html` to any web server
- Ensure HTTPS is enabled for camera access

## 🎮 Game Mechanics

### Scoring System
- **Check-In**: 1 point - Basic booth visit
- **Chat**: 2 points - Meaningful conversation
- **Bonus**: 3 points - In-depth discussion

### Engagement Strategy
- **Gamification** encourages quality interactions
- **Real-time feedback** provides immediate satisfaction
- **Leaderboard competition** drives engagement
- **Clear point values** set interaction expectations

## 🔧 Customization

### Easy Modifications
- **Admin password** - Change the admin access password
- **Supplier list** - Add/remove suppliers
- **Point values** - Adjust scoring system
- **Attendee list** - Update participant roster
- **Styling** - Modify colors and layout with Tailwind classes

### Advanced Customization
- **Additional scan types** - Extend beyond 3 types
- **Time-based bonuses** - Add rush hour multipliers
- **Team competitions** - Group attendees by company
- **Achievement system** - Add badges and milestones

## 📈 Analytics & Insights

### Real-time Monitoring
- Live leaderboard updates
- Scan frequency tracking
- Supplier engagement metrics
- Attendee participation rates

### Post-event Analysis
- Export data from Firestore
- Analyze interaction patterns
- Identify top-performing suppliers
- Generate engagement reports

## 🆘 Support & Troubleshooting

### Common Issues
- **Camera not working**: Ensure HTTPS and permissions
- **Login failures**: Check Badge UID format
- **Real-time issues**: Verify Firebase configuration
- **QR code problems**: Ensure proper printing quality

### Getting Help
1. Check browser console for errors
2. Verify Firebase setup
3. Test with sample data first
4. Ensure proper network connectivity

## 🎉 Success Metrics

### Engagement Goals
- **High participation rate** (>80% of attendees)
- **Quality interactions** (mix of all scan types)
- **Real-time engagement** (active leaderboard)
- **Supplier satisfaction** (meaningful conversations)

### Technical Success
- **Zero downtime** during event
- **Fast scan response** (<2 seconds)
- **Accurate scoring** (no duplicate issues)
- **Mobile optimization** (works on all devices)

---

**Ready to gamify your supplier engagement?** Follow the setup guide and start building meaningful connections! 🚀
