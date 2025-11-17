# Quick Setup Guide for SAKIB AI Website

## Immediate Next Steps

### 1. Configure Contact Form Access Key

**Your Web3Forms access key is stored locally** in `index.local.html` (not in git for security).

**To deploy the website:**
1. Open `index.html` and find line 146
2. Replace `YOUR_WEB3FORMS_ACCESS_KEY` with your actual access key
3. Deploy to your hosting platform

**Your access key can be found in:**
- `index.local.html` (local file, not in git)
- Your Web3Forms account at [web3forms.com](https://web3forms.com)

**To manage your form:**
- Visit [web3forms.com](https://web3forms.com) and log in with your email
- View submissions, change settings, etc.
- See `WEB3FORMS_INFO.md` for detailed documentation

### 2. Deploy to GitHub Pages (10 minutes)

```bash
# Initialize git repository
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: SAKIB AI consulting website"

# Create main branch
git branch -M main

# Add your GitHub repository as remote (replace with your repo URL)
git remote add origin https://github.com/YOUR_USERNAME/sakibai.git

# Push to GitHub
git push -u origin main
```

Then in GitHub:
1. Go to repository Settings
2. Click "Pages" in the sidebar
3. Under "Source", select "main" branch
4. Click "Save"
5. Your site will be live at `https://YOUR_USERNAME.github.io/sakibai/`

### 3. Custom Domain Setup (Optional)

If you own `sakibai.com` or another domain:

1. **Update CNAME file:**
   - Edit the `CNAME` file and replace `sakibai.com` with your actual domain

2. **Configure DNS at your domain registrar:**

   **Option A - Using A Records (recommended for apex domains):**
   ```
   Type: A
   Host: @
   Value: 185.199.108.153

   Type: A
   Host: @
   Value: 185.199.109.153

   Type: A
   Host: @
   Value: 185.199.110.153

   Type: A
   Host: @
   Value: 185.199.111.153
   ```

   **Option B - Using CNAME (for subdomains like www):**
   ```
   Type: CNAME
   Host: www
   Value: YOUR_USERNAME.github.io
   ```

3. **Wait for DNS propagation** (can take up to 48 hours, usually much faster)

4. **Enable HTTPS in GitHub Pages:**
   - Go to repository Settings > Pages
   - Check "Enforce HTTPS"

### 4. Customize Content

Update the following in `index.html`:

- **Line 37-51**: Hero section - adjust your tagline
- **Line 57-68**: About section - add your actual background
- **Line 107-133**: Experience section - verify company names and dates
- **Line 134-144**: Expertise tags - add/remove skills

### 5. Test Your Website

**Locally:**
```bash
# Option 1: Python
python -m http.server 8000

# Option 2: PHP
php -S localhost:8000
```

Then visit `http://localhost:8000`

**Live:**
- Visit your GitHub Pages URL
- Test the contact form
- Check on mobile devices
- Verify all links work

## Customization Tips

### Change Colors

Edit `styles.css` lines 8-16:
```css
:root {
    --primary-color: #0066ff;    /* Change to your brand color */
    --secondary-color: #000000;   /* Change headers color */
}
```

### Add More Services

In `index.html`, duplicate a service card (lines 75-80) and modify:
```html
<div class="service-card">
    <div class="service-icon">🎨</div>
    <h3 class="service-title">Your Service</h3>
    <p class="service-description">Service description</p>
</div>
```

### Update Contact Email Display

To show your email on the page, add this in the contact section:
```html
<p class="contact-intro">
    Ready to transform your business with AI? Let's discuss your project.<br>
    Email: <a href="mailto:your.email@example.com">your.email@example.com</a>
</p>
```

## Troubleshooting

**Contact form not working:**
- Verify you replaced `YOUR_FORM_ID` with actual Formspree form ID
- Check Formspree dashboard for submissions
- Make sure form action URL is correct

**GitHub Pages not showing updates:**
- Wait 1-2 minutes after pushing changes
- Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)
- Check GitHub Actions tab for deployment status

**Custom domain not working:**
- Verify DNS records are correct
- Wait for DNS propagation
- Check GitHub Pages settings show your domain
- Ensure CNAME file contains only your domain name

## Need Help?

- GitHub Pages Docs: https://docs.github.com/en/pages
- Formspree Docs: https://help.formspree.io/
- DNS Configuration: Contact your domain registrar's support

---

**Your website is ready to go live!** 🚀

Just follow the steps above to configure the contact form and deploy to GitHub Pages.
