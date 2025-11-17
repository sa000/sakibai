# Deployment Guide

## ✅ Your Site is Already Deployed!

**Live URL**: https://sa000.github.io/sakibai/

Your website is automatically deployed via GitHub Actions whenever you push to the `main` branch.

## How It Works

### Automated Deployment Pipeline

1. **Push to main** → Triggers GitHub Actions workflow
2. **Inject Access Key** → Web3Forms key from GitHub Secrets
3. **Deploy to GitHub Pages** → Site goes live automatically
4. **Access Key Protected** → Never appears in public repository

### Security Setup ✅

- ✅ Web3Forms access key stored in GitHub Secrets
- ✅ Key automatically injected during deployment
- ✅ Key visible in deployed site (necessary for form to work)
- ✅ Key never committed to public repository

## Important: Enable Domain Whitelist

To prevent others from using your form key even if they find it:

1. Go to [web3forms.com](https://web3forms.com)
2. Log in with your email
3. Find your form settings
4. Enable **Domain Whitelist**
5. Add these domains:
   - `sa000.github.io`
   - `sakibai.com` (if using custom domain)

**Result**: Your key will ONLY work on your domains, even if someone copies it.

## Making Changes

### Update Website Content

1. Edit files locally (index.html, styles.css, etc.)
2. Commit changes:
   ```bash
   git add .
   git commit -m "Update website content"
   git push origin main
   ```
3. GitHub Actions automatically deploys (takes ~1 minute)
4. Check progress: https://github.com/sa000/sakibai/actions

### Update Web3Forms Access Key

If you need to change the access key:

```bash
gh secret set WEB3FORMS_ACCESS_KEY --body "your-new-key-here" --repo sa000/sakibai
```

Then trigger a new deployment:
```bash
gh workflow run deploy.yml --repo sa000/sakibai
```

## Custom Domain Setup (sakibai.com)

The CNAME file is already configured for `sakibai.com`. To activate:

### 1. Configure DNS at Your Domain Registrar

**Option A - A Records (for apex domain):**
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

**Option B - CNAME (for www subdomain):**
```
Type: CNAME
Host: www
Value: sa000.github.io
```

### 2. Verify Domain in GitHub

1. Go to https://github.com/sa000/sakibai/settings/pages
2. Under "Custom domain", verify `sakibai.com` is configured
3. Wait for DNS check to complete (can take up to 48 hours)
4. Enable "Enforce HTTPS" once DNS is verified

### 3. Update Domain Whitelist

Don't forget to add `sakibai.com` to your Web3Forms domain whitelist!

## Monitoring

### Check Deployment Status

```bash
gh run list --repo sa000/sakibai
```

### View Deployment Logs

```bash
gh run view --repo sa000/sakibai
```

### Manual Deployment

```bash
gh workflow run deploy.yml --repo sa000/sakibai
```

## Troubleshooting

### Deployment Failed

1. Check the Actions tab: https://github.com/sa000/sakibai/actions
2. Click on the failed workflow to see error logs
3. Common issues:
   - Missing GitHub Secret
   - Syntax errors in HTML/CSS/JS
   - Permissions issue with GitHub Pages

### Form Not Working

1. **Check if key is injected**: View page source, search for `access_key`
2. **Verify domain whitelist**: Make sure your domain is whitelisted on Web3Forms
3. **Test locally**: Use the key from `index.local.html` for testing

### Custom Domain Not Working

1. **Check DNS**: Use `dig sakibai.com` or `nslookup sakibai.com`
2. **Wait for propagation**: Can take up to 48 hours
3. **Verify in GitHub**: Settings → Pages → Custom domain should show green checkmark
4. **Check HTTPS**: May need to disable/re-enable after DNS is verified

## GitHub Actions Workflow

The deployment workflow (`.github/workflows/deploy.yml`) runs on:
- Every push to `main` branch
- Manual trigger via workflow_dispatch

**Workflow steps:**
1. Checkout code
2. Replace `YOUR_WEB3FORMS_ACCESS_KEY` with actual key from secrets
3. Upload to GitHub Pages
4. Deploy site

## Security Notes

### What's Protected
- ✅ Access key never in public repository
- ✅ Access key never in git history
- ✅ Access key stored encrypted in GitHub Secrets

### What's Public
- ⚠️ Access key visible in deployed site HTML (required for client-side forms)
- ⚠️ Anyone viewing source can see the key

### Why This Is OK
- Web3Forms keys are designed for client-side use
- Domain whitelist prevents unauthorized use
- Key only allows sending emails, not reading them
- Standard practice for client-side form services

## Need Help?

- **GitHub Actions Docs**: https://docs.github.com/en/actions
- **GitHub Pages Docs**: https://docs.github.com/en/pages
- **Web3Forms Docs**: https://web3forms.com/docs

---

**Your website is live and secure!** 🚀

Visit: https://sa000.github.io/sakibai/
