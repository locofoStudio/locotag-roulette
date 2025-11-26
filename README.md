# Locotag Multi-Tenant Roulette Wheel

A dynamic, multi-tenant roulette wheel game for Locotag's loyalty platform that automatically adapts to each venue's branding colors loaded from Firebase Firestore.

## Features

- 🎨 **Dynamic Color Theming**: Automatically loads venue-specific colors from Firebase
- 🎡 **Interactive Roulette Wheel**: Smooth animations using Winwheel.js and GSAP
- 🎉 **Win Modal & Confetti**: Celebratory effects when players win
- 📱 **Responsive Design**: Works on desktop and mobile devices
- 🎯 **Multi-Tenant Support**: Single codebase supports multiple venues

## Setup Instructions

### 1. Firebase Configuration

1. Open `index.html` and locate the Firebase configuration section (around line 350)
2. Replace the placeholder values with your actual Firebase config:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT_ID",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### 2. Firebase Firestore Structure

Ensure your Firestore database has a `venues` collection with documents structured like this:

```
venues/
  {venueId}/
    name: "Venue Name"
    logo: "https://example.com/logo.png" (optional)
    colors: {
      accent1: "#E86526",
      accent2: "#BF9BF2",
      accent3: "#C5C352",
      accent4: "#6FA6A0",
      background: "#0F2533",
      backgroundDark: "#0F2533",
      backgroundLight: "#0C1D27",
      disable: "#525E5D",
      dropShadow: "#C5C352",
      error: "#FC1414",
      metrics: "#E86526",
      primary: "#0F2533",
      secondary: "#FFFFFF"
    }
```

### 3. Usage

#### Option 1: Direct File Access
Simply open `index.html` in a web browser. It will use the default venue (`demo`).

#### Option 2: URL Parameters
Add a `venue` parameter to specify which venue to load:

```
index.html?venue=venueId
```

Example:
```
index.html?venue=demo
```

#### Option 3: Local Server (Recommended)
For development, use a local server to avoid CORS issues:

```bash
# Using Python 3
python3 -m http.server 8000

# Using Node.js (http-server)
npx http-server

# Using PHP
php -S localhost:8000
```

Then navigate to `http://localhost:8000/index.html?venue=venueId`

## Wheel Configuration

The wheel has 8 segments with the following prizes:

1. **300 Coins** - Light cream background
2. **STOP** - Teal-green background (no prize)
3. **150 Coins** - Purple background
4. **🎁 Free Item** - Orange background
5. **50 Coins** - Yellow-green background
6. **20 Coins** - Light cream background
7. **∞ 1000 Coins** - Orange background (jackpot)
8. **5 Coins** - Light cream background

### Customizing Segments

Edit the `createWheelSegments()` function in `index.html` to customize prizes, colors, and segment count.

## Color System

### Default Locotag Colors
If a venue doesn't have custom colors, the game falls back to Locotag's default color scheme:

- **Background**: `#0F2533` (dark teal)
- **Primary Accent**: `#E86526` (orange)
- **Secondary Accent**: `#BF9BF2` (purple)
- **Tertiary Accent**: `#C5C352` (yellow-green)
- **Quaternary Accent**: `#6FA6A0` (teal-green)

### Dynamic Color Application
Colors are applied via CSS custom properties (variables) that update when venue data loads.

## Deployment

### GitHub Pages (Recommended)

This project is configured for easy deployment to GitHub Pages. See [DEPLOY.md](./DEPLOY.md) for detailed instructions.

**Quick Steps:**
1. Create a GitHub repository
2. Push your code: `git push origin main`
3. Enable GitHub Pages in repository Settings
4. Your roulette will be live at: `https://YOUR_USERNAME.github.io/REPO_NAME/`

**Access with venue parameter:**
```
https://YOUR_USERNAME.github.io/REPO_NAME/?venue=venueId
```

The included GitHub Actions workflow will automatically deploy on every push to `main`.

## Integration with Backend

To integrate prize collection with your backend:

1. Locate the `collectBtn` event listener (around line 500)
2. Add your API call to send the prize data:

```javascript
document.getElementById('collectBtn').addEventListener('click', async () => {
  const modal = document.getElementById('winModal');
  modal.classList.remove('show');
  
  // Add your API call here
  try {
    const response = await fetch('/api/collect-prize', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        venueId: venueId,
        prize: currentPrize,
        userId: currentUserId
      })
    });
    // Handle response
  } catch (error) {
    console.error('Error collecting prize:', error);
  }
});
```

## Dependencies

All dependencies are loaded via CDN:

- **Winwheel.js**: Roulette wheel rendering and animation
- **GSAP 3.12.0**: Advanced animations (available for future enhancements)
- **Firebase SDK 10.7.1**: Firestore database access

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Customization

### Changing Wheel Size
Edit the `outerRadius` property in the `initWheel()` function:

```javascript
wheel = new Winwheel({
  outerRadius: 180, // Change this value
  // ...
});
```

### Adjusting Spin Duration
Modify the animation duration:

```javascript
animation: {
  type: 'spinToStop',
  duration: 5, // Change this (in seconds)
  spins: 8,
  // ...
}
```

### Modifying Confetti
Adjust the confetti count and colors in the `createConfetti()` function.

## Troubleshooting

### Colors Not Loading
- Check browser console for Firebase errors
- Verify Firebase config is correct
- Ensure Firestore security rules allow read access
- Check that venue document exists in Firestore

### Wheel Not Spinning
- Verify Winwheel.js is loading (check Network tab)
- Check browser console for JavaScript errors
- Ensure canvas element is properly initialized

### CORS Errors
- Use a local server instead of opening file directly
- Check Firebase CORS configuration

## License

Proprietary - Locotag Studio

