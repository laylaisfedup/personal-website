# Deployment Guide for Habibah Ibrahim's Website

## Quick Overview
This is a static website with pale grey and white colors, inspired by Patrick Collison's minimal design. It's ready to deploy on Netlify and connect to your GoDaddy domain.

---

## Step 1: Upload to GitHub

### Option A: Replace Your Existing Repository

1. **Download all these files** from the links provided by Claude

2. **Open your GitHub repository** (https://github.com/laylaisfedup/personal-website)

3. **Delete all old files:**
   - Go to your repo on GitHub
   - Delete the `backend/`, `frontend/`, and `content/` folders
   - Delete `package.json` and other old files

4. **Upload new files:**
   - Click "Add file" → "Upload files"
   - Drag and drop ALL the new files you downloaded
   - Commit message: "Convert to static site with new design"
   - Click "Commit changes"

### Option B: Use Git Command Line

```bash
cd personal-website
rm -rf backend frontend content
# Copy your downloaded files here
git add .
git commit -m "Convert to static site - pale grey minimal design"
git push origin master
```

---

## Step 2: Deploy on Netlify

### If You Already Have Netlify Connected:

1. Go to [app.netlify.com](https://app.netlify.com)
2. Click on your site
3. Go to **Site settings** → **Build & deploy** → **Build settings**
4. Update these settings:
   - **Build command:** (delete/leave empty)
   - **Publish directory:** `.` (just a period)
5. Click **Save**
6. Go to **Deploys** tab
7. Click **Trigger deploy** → **Deploy site**

### If This is a New Netlify Site:

1. Go to [app.netlify.com](https://app.netlify.com)
2. Click **"Add new site"** → **"Import an existing project"**
3. Choose **GitHub**
4. Select your repository: `laylaisfedup/personal-website`
5. Configure settings:
   - **Branch to deploy:** `master` (or `main`)
   - **Build command:** (leave empty)
   - **Publish directory:** `.`
6. Click **Deploy site**
7. Wait 1-2 minutes for deployment

---

## Step 3: Connect Your GoDaddy Domain

### In Netlify (Get DNS Records):

1. Go to your site on Netlify
2. Click **Domain settings** (in the left menu)
3. Click **Add custom domain**
4. Enter your GoDaddy domain (e.g., `habibahfarooki.com`)
5. Click **Verify**
6. Netlify will show you DNS records to configure

**You'll see something like:**
```
A Record:
Name: @
Value: 75.2.60.5

CNAME Record:
Name: www
Value: your-site-name.netlify.app
```

### In GoDaddy (Add DNS Records):

1. Log in to [GoDaddy.com](https://www.godaddy.com)
2. Go to **My Products**
3. Find your domain and click **DNS** next to it
4. **Add the A Record:**
   - Type: `A`
   - Name: `@`
   - Value: `75.2.60.5` (or the IP Netlify gave you)
   - TTL: `600` seconds (or default)
   - Click **Add Record**

5. **Add the CNAME Record:**
   - Type: `CNAME`
   - Name: `www`
   - Value: `your-site-name.netlify.app` (from Netlify)
   - TTL: `1 Hour` (or default)
   - Click **Add Record**

6. **Save all changes**

### Wait for DNS Propagation:
- DNS changes take **24-48 hours** to propagate worldwide
- Your Netlify URL (like `your-site.netlify.app`) will work immediately
- Your custom domain will work after DNS propagates

---

## Step 4: Enable HTTPS (SSL)

1. In Netlify, go to **Domain settings**
2. Scroll to **HTTPS**
3. Click **Verify DNS configuration**
4. Once verified, click **Provision certificate**
5. Wait a few minutes - Netlify automatically sets up free HTTPS!

---

## Verify Everything Works

### Immediately (Netlify URL):
- ✅ Go to `your-site.netlify.app`
- ✅ Click through all pages: About, Blog, Bookshelf, Projects, Learning, Progress, Questions
- ✅ Check that all links work
- ✅ Test on mobile

### After 24-48 Hours (Custom Domain):
- ✅ Go to `yourdomain.com`
- ✅ Test all pages again
- ✅ Verify HTTPS works (you see the padlock 🔒)

---

## Troubleshooting

### ❌ Netlify shows 404 errors
**Fix:**
- Check `netlify.toml` is uploaded
- Verify "Publish directory" is set to `.` in Netlify settings
- Trigger a new deploy

### ❌ Domain not working after 48 hours
**Fix:**
- Use [whatsmydns.net](https://www.whatsmydns.net) to check DNS propagation
- Verify DNS records in GoDaddy exactly match Netlify's instructions
- Make sure you added BOTH the A record and CNAME record

### ❌ "Your connection is not private" error
**Fix:**
- Wait for DNS to fully propagate (24-48 hours)
- In Netlify, go to Domain settings → HTTPS → "Verify DNS configuration"
- Click "Provision certificate" again

### ❌ Site looks broken or old version shows
**Fix:**
- Clear your browser cache (Ctrl+Shift+Delete)
- Try in incognito/private browsing mode
- Make sure you pushed the correct files to GitHub

---

## Customizing Your Site

### Update Your Information:

1. **index.html** - Your name is already set to "Habibah Ibrahim"
2. **about.html** - Add your bio, experience, interests, social links
3. **projects.html** - Add your projects and achievements
4. **bookshelf.html** - Add books you've read and recommend
5. **learning.html** - Add your learning philosophy and current studies
6. **progress.html** - Customize with your thoughts
7. **questions.html** - Add questions you're curious about

### Change Colors:

Edit `style.css`:
```css
/* Current: pale grey (#6b7280) and white */
/* To change link color: */
a {
  color: #YOUR_COLOR_HERE;
}
```

### Add Blog Posts:

1. Create a folder called `blog/`
2. Create HTML files for each post:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Post Title · Habibah Ibrahim</title>
  <link rel="stylesheet" href="../style.css">
</head>
<body>
  <div class="container">
    <a href="../blog.html" class="back">← Blog</a>
    <h1>Your Post Title</h1>
    <p>Your content here...</p>
  </div>
</body>
</html>
```

3. Link it in `blog.html`:
```html
<li><a href="blog/your-post.html">Your Post Title</a> (January 2026)</li>
```

---

## Success Checklist

- ✅ Files uploaded to GitHub
- ✅ Netlify deployed successfully
- ✅ All pages load correctly
- ✅ DNS records added to GoDaddy
- ✅ HTTPS certificate provisioned
- ✅ Custom domain working
- ✅ Site looks minimal with pale grey/white colors
- ✅ All navigation links work
- ✅ Mobile responsive

---

## Need Help?

If something doesn't work:
1. Check Netlify's deploy log for errors
2. Verify all files are in GitHub
3. Double-check DNS records in GoDaddy
4. Wait full 48 hours for DNS propagation
5. Ask for help with specific error messages

Your site should now be live at both:
- `your-site.netlify.app` (immediately)
- `yourdomain.com` (after DNS propagation)

Enjoy your new minimal website! 🎉
