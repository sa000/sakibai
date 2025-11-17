# Namecheap Domain Setup Guide

## Connecting sakibai.com to GitHub Pages

Follow these steps to link your Namecheap domain to your GitHub Pages site.

## Step 1: Configure DNS in Namecheap

### 1.1 Log in to Namecheap

1. Go to [namecheap.com](https://www.namecheap.com)
2. Click "Sign In" (top right)
3. Log in with your credentials

### 1.2 Access Domain Management

1. Click "Domain List" in the left sidebar
2. Find `sakibai.com` in your list
3. Click the "Manage" button next to it

### 1.3 Configure Advanced DNS

1. Click the "Advanced DNS" tab
2. You'll see a list of DNS records

### 1.4 Delete Existing Records

**Important**: Remove any existing A Records and CNAME Records that might conflict

- Look for records with Host: `@` or `www`
- Click the trash icon to delete them
- You can keep MX records (for email), TXT records, etc.

### 1.5 Add GitHub Pages A Records

Click "Add New Record" and add these **4 A Records**:

**Record 1:**
- Type: `A Record`
- Host: `@`
- Value: `185.199.108.153`
- TTL: `Automatic` (or `300`)

**Record 2:**
- Type: `A Record`
- Host: `@`
- Value: `185.199.109.153`
- TTL: `Automatic`

**Record 3:**
- Type: `A Record`
- Host: `@`
- Value: `185.199.110.153`
- TTL: `Automatic`

**Record 4:**
- Type: `A Record`
- Host: `@`
- Value: `185.199.111.153`
- TTL: `Automatic`

### 1.6 Add WWW CNAME Record (Optional but Recommended)

Click "Add New Record":

- Type: `CNAME Record`
- Host: `www`
- Value: `sa000.github.io`
- TTL: `Automatic`

### 1.7 Save Changes

Click the green checkmark or "Save All Changes" button at the bottom.

**Your DNS settings should now look like this:**

```
Type         Host    Value                  TTL
─────────────────────────────────────────────────
A Record     @       185.199.108.153        Automatic
A Record     @       185.199.109.153        Automatic
A Record     @       185.199.110.153        Automatic
A Record     @       185.199.111.153        Automatic
CNAME        www     sa000.github.io.       Automatic
```

## Step 2: Verify Domain in GitHub

### 2.1 Check GitHub Pages Settings

1. Go to https://github.com/sa000/sakibai/settings/pages
2. Under "Custom domain", you should see `sakibai.com`
3. GitHub will automatically check DNS configuration

### 2.2 Wait for DNS Check

- **Status**: You'll see a yellow warning: "DNS check in progress"
- **Time**: Can take 5 minutes to 48 hours (usually ~1 hour)
- **Why**: DNS changes need to propagate across the internet

### 2.3 Verify DNS is Working

**Test from command line:**
```bash
# Check if A records are set
dig sakibai.com +short

# Should show:
# 185.199.108.153
# 185.199.109.153
# 185.199.110.153
# 185.199.111.153
```

**Or use online tools:**
- https://www.whatsmydns.net/#A/sakibai.com
- https://dnschecker.org/#A/sakibai.com

### 2.4 Enable HTTPS

Once DNS check passes (green checkmark appears):

1. Go to https://github.com/sa000/sakibai/settings/pages
2. Check the box: **"Enforce HTTPS"**
3. Wait a few minutes for certificate to be issued
4. Your site will be available at: https://sakibai.com

## Step 3: Update Web3Forms Domain Whitelist

**Critical**: Add your custom domain to the whitelist!

1. Go to [web3forms.com](https://web3forms.com)
2. Log in and find your form
3. Go to Form Settings → Domain Whitelist
4. Add both:
   - `sakibai.com`
   - `www.sakibai.com`
   - `sa000.github.io` (keep this too)

## Troubleshooting

### DNS Not Propagating

**Check propagation status:**
```bash
# Mac/Linux
dig sakibai.com

# Windows
nslookup sakibai.com
```

**If showing old IP or not found:**
- Wait longer (can take up to 48 hours)
- Clear your DNS cache:
  - **Mac**: `sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder`
  - **Windows**: `ipconfig /flushdns`
  - **Linux**: `sudo systemd-resolve --flush-caches`

### GitHub Pages Shows "Improperly Configured"

**Possible causes:**
1. **CNAME file missing** - Already set in your repo ✓
2. **DNS not propagated yet** - Wait and refresh
3. **Wrong A record IPs** - Double-check the 4 IPs above
4. **Multiple domains** - Remove any other custom domains

**Fix:**
1. Go to GitHub Pages settings
2. Remove custom domain
3. Wait 1 minute
4. Re-add `sakibai.com`
5. Wait for DNS check

### "DNS Check Failed" in GitHub

**Common issues:**
- A records pointing to wrong IPs
- CNAME record pointing to wrong value
- DNS hasn't propagated yet

**Solution:**
1. Verify A records in Namecheap match exactly
2. Use https://www.whatsmydns.net to check global propagation
3. Wait 15-30 minutes and try again

### Site Shows 404 Error

**Causes:**
- DNS is working but GitHub Pages not deployed
- Wrong repository name in CNAME

**Fix:**
1. Check deployment status: https://github.com/sa000/sakibai/actions
2. Verify CNAME file contains only: `sakibai.com`
3. Trigger new deployment:
   ```bash
   git commit --allow-empty -m "Trigger deployment"
   git push origin main
   ```

### WWW vs Non-WWW

**Both should work:**
- `https://sakibai.com` → Main site
- `https://www.sakibai.com` → Redirects to main site

If www doesn't work, verify CNAME record in Namecheap.

## Timeline Expectations

| Step | Expected Time |
|------|---------------|
| DNS configuration in Namecheap | Immediate |
| DNS propagation (local) | 5-30 minutes |
| DNS propagation (global) | 1-48 hours |
| GitHub DNS check | 5 minutes - 1 hour |
| HTTPS certificate issuance | 5-10 minutes |

**Total time**: Usually 30 minutes - 2 hours, but can take up to 48 hours for full global propagation.

## Verification Checklist

After setup, verify everything works:

- [ ] `dig sakibai.com` shows GitHub Pages IPs
- [ ] https://sakibai.com loads your website
- [ ] https://www.sakibai.com redirects to sakibai.com
- [ ] HTTPS padlock shows in browser
- [ ] Contact form works (test by submitting)
- [ ] No mixed content warnings in browser console

## Important Notes

### Email Configuration

**If you use email with this domain** (like hello@sakibai.com):

⚠️ **DO NOT delete MX, TXT, or SPF records** in Namecheap!

Only delete/modify A and CNAME records as specified above.

### Apex Domain vs Subdomain

- **Apex domain**: `sakibai.com` (no www) - uses A records
- **Subdomain**: `www.sakibai.com` - uses CNAME record
- GitHub Pages supports both

### DNS TTL (Time To Live)

- Namecheap default: 300 seconds (5 minutes)
- This means DNS changes propagate every 5 minutes
- Lower TTL = faster changes, but more DNS queries

---

## Quick Reference: DNS Records

Copy these exact values into Namecheap Advanced DNS:

```
A       @     185.199.108.153
A       @     185.199.109.153
A       @     185.199.110.153
A       @     185.199.111.153
CNAME   www   sa000.github.io
```

**Need help?**
- Namecheap Support: https://www.namecheap.com/support/
- GitHub Pages Docs: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

---

**Once DNS propagates, your site will be live at https://sakibai.com!** 🚀
