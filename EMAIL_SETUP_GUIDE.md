# Email Setup Guide - KAGZSO Website

## Email Sending via EmailJS

Your website now has email functionality integrated using **EmailJS**, which allows form submissions to be sent directly to your email without needing a backend server.

### Quick Setup (5 minutes)

#### 1. Create a Free EmailJS Account
- Go to https://www.emailjs.com/
- Click **"Sign Up Free"**
- Sign up with your email (kagzso.in@gmail.com recommended)
- Verify your email

#### 2. Get Your Public Key
- Log in to your EmailJS dashboard
- Go to **Account** → **API Keys**
- Copy your **Public Key** (looks like: `abc123xyz456`)

#### 3. Connect Gmail to EmailJS
- In EmailJS dashboard, go to **Email Services**
- Click **Add Service**
- Choose **Gmail**
- Click **Connect with Gmail**
- Authorize EmailJS to access your Gmail account
- You'll get a **Service ID** (e.g., `gmail_service`)

#### 4. Create Email Template
- In EmailJS dashboard, go to **Email Templates**
- Click **Create New Template**
- Use these settings:

**Template Name:** `contact_form`
**Service:** `gmail_service` (or whatever you named it)
**From Email:** `{{from_email}}`
**To Email:** `{{to_email}}`
**Subject:** `New Automation Assessment Request from {{from_name}}`
**Template Content:**
```
Name: {{from_name}}
Email: {{from_email}}
Phone: {{phone}}
Business Type: {{business_type}}

Message:
{{message}}

---
Reply to this email to contact them directly.
```

- Click **Save**
- **Note the Template ID** (e.g., `contact_form`)

#### 5. Update Your Website Code
Open [index.html](./index.html) and find this section (around line 1223):

```javascript
// Initialize EmailJS
(function() {
  emailjs.init('YOUR_EMAILJS_PUBLIC_KEY');
})();
```

Replace `'YOUR_EMAILJS_PUBLIC_KEY'` with your actual public key.

Then find this section (around line 1247):

```javascript
emailjs.send('SERVICE_ID', 'TEMPLATE_ID', {
```

Replace:
- `'SERVICE_ID'` with your Service ID (e.g., `'gmail_service'`)
- `'TEMPLATE_ID'` with your Template ID (e.g., `'contact_form'`)

**Example:**
```javascript
emailjs.send('gmail_service', 'contact_form', {
```

#### 6. Test It
- Open your website
- Fill out the "Get Assessment" form
- Submit
- Check your email (kagzso.in@gmail.com) for the form submission
- Verify the email arrives correctly

### What Happens When Someone Submits the Form

1. **Form submission** → EmailJS receives the data
2. **Validation** → Checks required fields are complete
3. **Email sent** → Sends to kagzso.in@gmail.com with all form details
4. **Confirmation** → Shows success message to the user
5. **Reply-to** → User's email is set as reply-to, so you can click Reply to email them back

### Customizing the Email Template

To modify the email content:
1. Go to EmailJS Dashboard
2. Click on your template (`contact_form`)
3. Edit the **Template Content** (HTML)
4. Any field in `{{double_braces}}` will be filled from the form data

**Available form variables:**
- `{{from_name}}` - User's full name
- `{{from_email}}` - User's email
- `{{phone}}` - User's phone number
- `{{business_type}}` - Selected business type
- `{{message}}` - Their automation challenge/goal

### Troubleshooting

| Issue | Solution |
|-------|----------|
| Emails not sending | 1. Check Service ID & Template ID match exactly 2. Verify Gmail is connected in EmailJS 3. Check browser console for errors (F12) |
| Wrong recipient | Change `to_email` in the form handler to your actual email |
| Missing form fields in email | Update the template variables to match the form IDs in HTML |
| "Init error" message | Verify Public Key is correct and copied exactly |
| Rate limiting | EmailJS free plan allows ~200 emails/month. Upgrade for more. |

### Security Notes

✅ **Public Key is SAFE to put in public HTML** (it's meant for client-side)
✅ **No sensitive data in the code**
✅ **HTTPS not required** (EmailJS handles encryption)
❌ **DO NOT** put Service Key in your HTML (only Public Key)

### Next Steps

- [ ] Create EmailJS account
- [ ] Get Public Key
- [ ] Connect Gmail service
- [ ] Create email template
- [ ] Update SERVICE_ID in index.html
- [ ] Update TEMPLATE_ID in index.html
- [ ] Test the form

Need help? Visit https://www.emailjs.com/docs/

---
**Last updated:** December 20, 2025
**Website:** index.html (lines 1220-1290)
