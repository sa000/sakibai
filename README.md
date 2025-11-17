# SAKIB AI - Consulting Website

A modern, minimalistic consulting website for SAKIB AI, showcasing AI, analytics, and automation services for hedge funds and private equity.

## Features

- Modern, minimalistic design
- Responsive layout (mobile, tablet, desktop)
- Smooth scrolling navigation
- Interactive contact form
- Service showcase
- Professional experience section
- GitHub Pages ready

## Setup Instructions

### 1. GitHub Pages Deployment

1. Create a new GitHub repository (e.g., `sakibai-website`)
2. Push all files to the repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: SAKIB AI website"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/sakibai-website.git
   git push -u origin main
   ```

3. Enable GitHub Pages:
   - Go to your repository settings
   - Navigate to "Pages" section
   - Under "Source", select "main" branch
   - Click "Save"

### 2. Custom Domain (CNAME) Setup

The `CNAME` file is already included with the domain `sakibai.com`. To use your custom domain:

1. Update the `CNAME` file with your actual domain name
2. Configure your domain's DNS settings:
   - Add an A record pointing to GitHub Pages IPs:
     - 185.199.108.153
     - 185.199.109.153
     - 185.199.110.153
     - 185.199.111.153
   - Or add a CNAME record pointing to: `YOUR_USERNAME.github.io`

3. Wait for DNS propagation (can take up to 24-48 hours)

### 3. Contact Form Setup

The contact form uses **Web3Forms** for email submission.

**Security Note**: The Web3Forms access key is NOT stored in this public repository. You need to add it before deployment.

#### Setup Steps:

1. **Get your access key** from:
   - `index.local.html` (local file, not in git)
   - Your Web3Forms dashboard at [web3forms.com](https://web3forms.com)

2. **Add the key to `index.html`** (line 146):
   ```html
   <input type="hidden" name="access_key" value="YOUR_WEB3FORMS_ACCESS_KEY">
   ```

3. **Deploy** to your hosting platform (GitHub Pages, Netlify, etc.)

#### Managing Your Form:

1. **View Submissions**: Visit [web3forms.com](https://web3forms.com) and log in with your email
2. **Change Email**: Update your email in the Web3Forms dashboard
3. **Spam Protection**: Enabled by default
4. **Customization**: See `WEB3FORMS_INFO.md` for advanced options

## Customization

### Update Your Information

1. **Personal Details** (`index.html`):
   - Update the About section with your actual background
   - Modify the Experience section with correct company names and dates
   - Add or remove services as needed

2. **Styling** (`styles.css`):
   - Change colors in the `:root` variables (lines 8-16)
   - Adjust fonts, spacing, and other design elements

3. **Content**:
   - Replace company names with accurate information
   - Update expertise tags to match your skills
   - Modify service descriptions

### Color Customization

To change the color scheme, edit the CSS variables in `styles.css`:

```css
:root {
    --primary-color: #0066ff;  /* Main brand color */
    --secondary-color: #000000; /* Headers and important text */
    --text-color: #333333;      /* Body text */
    --text-light: #666666;      /* Secondary text */
}
```

## File Structure

```
sakibai/
├── index.html          # Main HTML file
├── styles.css          # Stylesheet
├── script.js           # JavaScript for interactivity
├── CNAME              # Custom domain configuration
├── .nojekyll          # GitHub Pages configuration
└── README.md          # This file
```

## Technologies Used

- HTML5
- CSS3 (with CSS Grid and Flexbox)
- Vanilla JavaScript
- Google Fonts (Inter)
- Web3Forms (for contact form)

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers

## Local Development

To test locally, simply open `index.html` in your web browser. For a better development experience with live reload:

```bash
# Using Python 3
python -m http.server 8000

# Using Node.js (install http-server first: npm install -g http-server)
http-server

# Using PHP
php -S localhost:8000
```

Then visit `http://localhost:8000` in your browser.

## License

Copyright (c) 2024 SAKIB AI. All rights reserved.

## Support

For questions or issues, please contact through the website contact form.
