# 📧 Google Sheets Contact Form Setup Guide

This guide will help you connect your portfolio's contact form to Google Sheets so you can receive messages directly in a spreadsheet.

## 🎯 Step-by-Step Instructions

### Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Create a new spreadsheet
3. Name it "Portfolio Contact Form" or any name you prefer
4. In the first row, add these column headers:
   - A1: `Name`
   - B1: `Email`
   - C1: `Subject`
   - D1: `Message`
   - E1: `Timestamp`

### Step 2: Create Apps Script

1. In your Google Sheet, click **Extensions** → **Apps Script**
2. Delete any existing code
3. Copy and paste this code:

```javascript
function doPost(e) {
  try {
    // Get the active spreadsheet
    var sheet = SpreadsheetApp.getActiveSheet();
    
    // Parse the incoming data
    var data = JSON.parse(e.postData.contents);
    
    // Append a new row with the form data
    sheet.appendRow([
      data.name,
      data.email,
      data.subject,
      data.message,
      data.timestamp
    ]);
    
    // Return success response
    return ContentService.createTextOutput(JSON.stringify({
      result: 'success',
      message: 'Data saved successfully'
    }))
    .setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    // Return error response
    return ContentService.createTextOutput(JSON.stringify({
      result: 'error',
      message: error.toString()
    }))
    .setMimeType(ContentService.MimeType.JSON);
  }
}

// Optional: Test function
function doGet(e) {
  return ContentService.createTextOutput('Contact Form API is working!');
}
```

4. Click the **Save** icon (💾) or press `Ctrl+S`
5. Name your project "Portfolio Contact Form API"

### Step 3: Deploy as Web App

1. Click **Deploy** → **New deployment**
2. Click the gear icon ⚙️ next to "Select type"
3. Choose **Web app**
4. Fill in the deployment settings:
   - **Description**: "Portfolio Contact Form v1"
   - **Execute as**: "Me (your email)"
   - **Who has access**: "Anyone"
5. Click **Deploy**
6. Review permissions:
   - Click **Authorize access**
   - Choose your Google account
   - Click **Advanced** → **Go to Portfolio Contact Form API (unsafe)**
   - Click **Allow**
7. **Copy the Web App URL** - it will look like:
   ```
   https://script.google.com/macros/s/AKfycby.../exec
   ```

### Step 4: Update Your Portfolio Code

1. Open `script.js` in your portfolio repository
2. Find this line (around line 150):
   ```javascript
   const GOOGLE_SHEET_URL = 'YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE';
   ```
3. Replace `YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE` with your Web App URL:
   ```javascript
   const GOOGLE_SHEET_URL = 'https://script.google.com/macros/s/AKfycby.../exec';
   ```
4. Save and commit the changes

### Step 5: Test Your Contact Form

1. Visit your portfolio website
2. Go to the Contact section
3. Fill out the form with test data
4. Click "Send Message"
5. Check your Google Sheet - you should see a new row with the data!

## 🔧 Troubleshooting

### Form not submitting?
- Check browser console for errors (F12)
- Verify the Web App URL is correct
- Make sure "Who has access" is set to "Anyone"

### Data not appearing in sheet?
- Check if the Apps Script is deployed
- Verify column headers match exactly
- Try redeploying the Web App

### Getting CORS errors?
- This is normal! The form uses `mode: 'no-cors'`
- Data will still be saved to Google Sheets
- The success message will still display

## 📊 Viewing Your Messages

All contact form submissions will appear in your Google Sheet with:
- Name of the sender
- Email address
- Subject line
- Message content
- Timestamp of submission

## 🔒 Security Notes

- The Web App URL is public but only accepts POST requests
- No sensitive data is exposed
- You can revoke access anytime from Google Apps Script
- Consider adding spam protection for production use

## 🎨 Customization

### Add Email Notifications

To receive email notifications when someone submits the form, add this to your Apps Script:

```javascript
function doPost(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSheet();
    var data = JSON.parse(e.postData.contents);
    
    sheet.appendRow([
      data.name,
      data.email,
      data.subject,
      data.message,
      data.timestamp
    ]);
    
    // Send email notification
    MailApp.sendEmail({
      to: 'sudeshainapure18@gmail.com',
      subject: 'New Portfolio Contact: ' + data.subject,
      body: 'Name: ' + data.name + '\n' +
            'Email: ' + data.email + '\n' +
            'Subject: ' + data.subject + '\n' +
            'Message: ' + data.message + '\n\n' +
            'Sent at: ' + data.timestamp
    });
    
    return ContentService.createTextOutput(JSON.stringify({
      result: 'success'
    }))
    .setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({
      result: 'error',
      message: error.toString()
    }))
    .setMimeType(ContentService.MimeType.JSON);
  }
}
```

### Add Data Validation

To prevent spam or validate data, add checks in your Apps Script:

```javascript
function doPost(e) {
  try {
    var data = JSON.parse(e.postData.contents);
    
    // Validate email format
    var emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailRegex.test(data.email)) {
      throw new Error('Invalid email format');
    }
    
    // Check for minimum message length
    if (data.message.length < 10) {
      throw new Error('Message too short');
    }
    
    // Continue with saving data...
    var sheet = SpreadsheetApp.getActiveSheet();
    sheet.appendRow([
      data.name,
      data.email,
      data.subject,
      data.message,
      data.timestamp
    ]);
    
    return ContentService.createTextOutput(JSON.stringify({
      result: 'success'
    }))
    .setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({
      result: 'error',
      message: error.toString()
    }))
    .setMimeType(ContentService.MimeType.JSON);
  }
}
```

## 📞 Need Help?

If you encounter any issues:
1. Check the [Google Apps Script documentation](https://developers.google.com/apps-script)
2. Review the browser console for errors
3. Test the Web App URL directly in your browser
4. Make sure all permissions are granted

---

✅ Once set up, your contact form will automatically save all submissions to Google Sheets!