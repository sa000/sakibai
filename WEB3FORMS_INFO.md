# Web3Forms Configuration Guide

## Your Form Details

**Access Key**: Stored securely in `index.local.html` (not committed to git)

To use the form locally or deploy it, you need to add your Web3Forms access key to `index.html`.

## How It Works

When someone submits the contact form on your website:
1. The form data is sent to Web3Forms API
2. Web3Forms processes the submission
3. You receive an email with the form details
4. The user is redirected to a success page

## Managing Your Form

### Access Your Dashboard

1. Go to [web3forms.com](https://web3forms.com)
2. Log in with the email you used to create the access key
3. View all form submissions, manage settings, and more

### View Submissions

All form submissions are stored in your Web3Forms dashboard for 30 days (on the free plan). You can:
- View submission history
- Export submissions to CSV
- Delete submissions

### Change Your Email

To receive submissions at a different email address:
1. Log in to your Web3Forms dashboard
2. Go to Form Settings
3. Update your email address
4. Verify the new email

## Advanced Customization

### Custom Success Page

Currently, users are redirected to `https://web3forms.com/success` after submission. To create your own success page:

1. Create a `success.html` file in your project
2. Update `index.html` line 149:
   ```html
   <input type="hidden" name="redirect" value="https://yourdomain.com/success.html">
   ```

### Custom Email Subject

Add a hidden field to customize the email subject:
```html
<input type="hidden" name="subject" value="New Contact from SAKIB AI Website">
```

### Add More Form Fields

You can add any custom fields to the form. Web3Forms will include them in the email. For example:

```html
<div class="form-group">
    <label for="phone">Phone Number</label>
    <input type="tel" id="phone" name="phone">
</div>
```

### Spam Protection

Web3Forms includes built-in spam protection. For additional security, you can add a honeypot field:

```html
<input type="checkbox" name="botcheck" class="hidden" style="display: none;">
```

### Custom Reply-To Address

The form already collects the user's email. Web3Forms automatically sets this as the reply-to address, so you can easily respond to inquiries.

## Troubleshooting

### Not Receiving Emails?

1. **Check Spam Folder**: Web3Forms emails might be in spam
2. **Verify Email**: Make sure you verified your email with Web3Forms
3. **Check Dashboard**: Log in to see if submissions are being received
4. **Whitelist**: Add `noreply@web3forms.com` to your contacts

### Form Not Submitting?

1. **Check Access Key**: Ensure the access key in `index.html` is correct
2. **Browser Console**: Open browser dev tools to check for errors
3. **Network Tab**: Verify the POST request is being sent to Web3Forms API

### Want to Test?

Simply fill out your own contact form and submit it. You should:
1. See the "Sending..." button state
2. Be redirected to the success page
3. Receive an email within a few minutes

## Rate Limits

**Free Plan Limits**:
- Unlimited form submissions
- 250 emails per month
- Submissions stored for 30 days
- Basic spam protection

If you need more, check out Web3Forms paid plans at [web3forms.com/pricing](https://web3forms.com/pricing).

## Support

- **Documentation**: [web3forms.com/docs](https://web3forms.com/docs)
- **Support Email**: support@web3forms.com
- **Response Time**: Usually within 24 hours

## Backup Your Access Key

**Important**: Keep your access key safe! If you lose it, you'll need to create a new form.

Your access key is stored in:
- `index.local.html` (local file, NOT in git)
- Your Web3Forms dashboard

## Alternative: Getting a New Access Key

If you need to create a new form or access key:

1. Go to [web3forms.com](https://web3forms.com)
2. Enter your email address
3. Click "Create Access Key"
4. Check your email for the new access key
5. Replace the old key in `index.html`

---

**Your form is ready to go!** No additional configuration needed. Just deploy to GitHub Pages and start receiving inquiries.
