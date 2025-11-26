# Deploying Locotag Roulette to GitHub Pages

## Quick Setup (5 minutes)

### Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and create a new repository
   - Name it: `locotag-roulette` (or any name you prefer)
   - Make it **Public** (required for free GitHub Pages)
   - **Don't** initialize with README, .gitignore, or license

### Step 2: Push Your Code

```bash
cd "/Users/nosh/Dropbox/LOCOFO STUDIO/LOCOTAG/app/locotag-roulette"

# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: Locotag Roulette"

# Add your GitHub repository as remote
git remote add origin https://github.com/YOUR_USERNAME/locotag-roulette.git

# Push to GitHub
git branch -M main
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** tab
3. Scroll down to **Pages** section (left sidebar)
4. Under **Source**, select:
   - Branch: `main` (or `master`)
   - Folder: `/ (root)`
5. Click **Save**

### Step 4: Wait for Deployment

- GitHub will build and deploy your site (takes 1-2 minutes)
- You'll see a green checkmark when it's ready
- Your site will be live at:
  ```
  https://YOUR_USERNAME.github.io/locotag-roulette/
  ```

---

## Using Your Roulette URL

### Basic URL
```
https://YOUR_USERNAME.github.io/locotag-roulette/
```

### With Venue Parameter
```
https://YOUR_USERNAME.github.io/locotag-roulette/?venue=venueId
```

### Example
```
https://YOUR_USERNAME.github.io/locotag-roulette/?venue=demo
```

---

## Automatic Deployment

The included `.github/workflows/deploy.yml` will automatically deploy your site whenever you push to the `main` branch. Just push your changes and GitHub Pages will update automatically!

```bash
# Make changes to your files
# Then commit and push
git add .
git commit -m "Update roulette"
git push
```

---

## Custom Domain (Optional)

1. Go to repository **Settings** → **Pages**
2. Under **Custom domain**, enter your domain
3. Follow DNS setup instructions
4. Your roulette will be available at your custom domain

---

## Testing Locally

Before deploying, test locally:

```bash
# Using Python (if installed)
python3 -m http.server 8000

# Or using Node.js http-server
npx http-server -p 8000

# Then open: http://localhost:8000
```

---

## Troubleshooting

### Site Not Loading
- Wait 2-3 minutes after enabling Pages
- Check repository Settings → Pages for any errors
- Ensure repository is **Public** (free accounts require public repos)

### Changes Not Showing
- GitHub Pages can take 1-2 minutes to update
- Hard refresh your browser (Ctrl+F5 or Cmd+Shift+R)
- Check Actions tab to see if deployment succeeded

### CORS Errors
- GitHub Pages should handle CORS automatically
- If issues persist, check Firebase security rules

---

## Quick Reference

**Your roulette URL format:**
```
https://YOUR_USERNAME.github.io/REPO_NAME/?venue=VENUE_ID
```

**To update:**
```bash
git add .
git commit -m "Your message"
git push
```
