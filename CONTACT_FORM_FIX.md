# 🔧 Contact Form Fix - Complete Setup Guide

## ⚠️ Issue: Not Receiving Messages

The contact form needs the correct Google Apps Script setup. Follow these steps carefully.

---

## 📝 Step 1: Update Your Google Apps Script

1. **Open your Google Sheet** where you want to receive messages
2. Click **Extensions** → **Apps Script**
3. **Delete all existing code**
4. **Copy and paste this EXACT code**:

```javascript
function doGet(e) {
  return handleRequest(e);
}

function doPost(e) {
  return handleRequest(e);
}

function handleRequest(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    
    // Get parameters from either GET or POST
    var params = e.parameter;
    
    // Extract data
    var name = params.name || '';
    var email = params.email || '';
    var subject = params.subject || '';
    var message = params.message || '';
    var timestamp = params.timestamp || new Date().toLocaleString();
    
    // Append row to sheet
    sheet.appendRow([name, email, subject, message, timestamp]);
    
    // Return success response
    return ContentService.createTextOutput(
      JSON.stringify({
        'result': 'success',
        'message': 'Data saved successfully'
      })
    ).setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    // Return error response
    return ContentService.createTextOutput(
      JSON.stringify({
        'result': 'error',
        'message': error.toString()
      })
    ).setMimeType(ContentService.MimeType.JSON);
  }
}

// Test function - you can run this to test
function testFunction() {
  var testData = {
    parameter: {
      name: 'Test User',
      email: 'test@example.com',
      subject: 'Test Subject',
      message: 'Test Message',
      timestamp: new Date().toLocaleString()
    }
  };
  
  var result = handleRequest(testData);
  Logger.log(result.getContent());
}
```

5. Click **Save** (💾 icon)
6. Name it "Portfolio Contact Form"

---

## 🚀 Step 2: Deploy the Web App

1. Click **Deploy** → **New deployment**
2. Click the **gear icon** ⚙️ next to "Select type"
3. Choose **Web app**
4. Configure settings:
   - **Description**: "Contact Form v1"
   - **Execute as**: **Me (your-email@gmail.com)**
   - **Who has access**: **Anyone** ⚠️ IMPORTANT!
5. Click **Deploy**
6. **Authorize access**:
   - Click **Authorize access**
   - Choose your Google account
   - Click **Advanced**
   - Click **Go to Portfolio Contact Form (unsafe)**
   - Click **Allow**
7. **Copy the Web App URL** - it looks like:
   ```
   https://script.google.com/macros/s/AKfycby.../exec
   ```

---

## 📊 Step 3: Setup Your Google Sheet

Make sure your Google Sheet has these **exact column headers** in Row 1:

| A | B | C | D | E |
|---|---|---|---|---|
| Name | Email | Subject | Message | Timestamp |

---

## ✅ Step 4: Test the Setup

### Test Method 1: Direct URL Test

1. Copy your Web App URL
2. Add test parameters to the end:
   ```
   https://script.google.com/macros/s/YOUR_ID/exec?name=Test&email=test@test.com&subject=Test&message=Hello&timestamp=2025-01-06
   ```
3. Paste in browser and press Enter
4. Check your Google Sheet - you should see a new row!

### Test Method 2: Run Test Function

1. In Apps Script, select **testFunction** from dropdown
2. Click **Run** (▶️ button)
3. Check your Google Sheet for test data

---

## 🔄 Step 5: Update Portfolio (If Needed)

Your portfolio already has the correct code! But verify your URL is correct:

1. Go to your repository: https://github.com/sudeshainapure18-ship-it/portfolio
2. Open `script.js`
3. Find line ~170 with:
   ```javascript
   const GOOGLE_SHEET_URL = 'https://script.google.com/macros/s/AKfycbxrEDmBqfQJApJ-pcdM5UJDEm7qfbPVhQY5rlB11x8DaicT4ROrVzKNxnWpCBIFWXE/exec';
   ```
4. Make sure this matches your Web App URL from Step 2

---

## 🧪 Step 6: Test on Your Live Site

1. Visit: https://sudeshainapure18-ship-it.github.io/portfolio/
2. Scroll to **Contact** section
3. Fill out the form:
   - Name: Test User
   - Email: test@example.com
   - Subject: Testing Form
   - Message: This is a test message
4. Click **Send Message**
5. You should see: "✅ Thank you! Your message has been sent successfully."
6. Check your Google Sheet - the data should appear!

---

## 🔍 Troubleshooting

### Problem: "Who has access" is not set to "Anyone"

**Solution:**
1. Go to Apps Script
2. Click **Deploy** → **Manage deployments**
3. Click **Edit** (pencil icon)
4. Change "Who has access" to **Anyone**
5. Click **Deploy**

### Problem: Authorization issues

**Solution:**
1. Delete the current deployment
2. Create a new deployment
3. Go through authorization again
4. Make sure to click "Advanced" → "Go to ... (unsafe)" → "Allow"

### Problem: Data not appearing in sheet

**Solution:**
1. Check column headers match exactly: Name, Email, Subject, Message, Timestamp
2. Make sure you're looking at the correct sheet (first sheet/active sheet)
3. Try the direct URL test from Step 4

### Problem: Form shows error message

**Solution:**
1. Open browser console (F12)
2. Look for errors
3. Verify the Web App URL is correct
4. Make sure the deployment is set to "Anyone"

### Problem: Old deployment not working

**Solution:**
1. Create a **NEW deployment** (don't edit old one)
2. Use the new URL
3. Update `script.js` with new URL

---

## 📧 Alternative: Email Notifications

Want to receive emails when someone submits the form? Update your Apps Script:

```javascript
function handleRequest(e) {
  try {
    var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
    var params = e.parameter;
    
    var name = params.name || '';
    var email = params.email || '';
    var subject = params.subject || '';
    var message = params.message || '';
    var timestamp = params.timestamp || new Date().toLocaleString();
    
    // Append to sheet
    sheet.appendRow([name, email, subject, message, timestamp]);
    
    // Send email notification
    MailApp.sendEmail({
      to: 'sudeshainapure18@gmail.com',
      subject: '📧 New Portfolio Contact: ' + subject,
      body: 'You received a new message from your portfolio!\n\n' +
            '👤 Name: ' + name + '\n' +
            '📧 Email: ' + email + '\n' +
            '📝 Subject: ' + subject + '\n' +
            '💬 Message:\n' + message + '\n\n' +
            '🕐 Received: ' + timestamp
    });
    
    return ContentService.createTextOutput(
      JSON.stringify({'result': 'success'})
    ).setMimeType(ContentService.MimeType.JSON);
    
  } catch (error) {
    return ContentService.createTextOutput(
      JSON.stringify({'result': 'error', 'message': error.toString()})
    ).setMimeType(ContentService.MimeType.JSON);
  }
}
```

---

## ✅ Checklist

Before testing, make sure:

- [ ] Google Sheet has correct column headers
- [ ] Apps Script code is updated with the code above
- [ ] Web App is deployed with "Execute as: Me"
- [ ] "Who has access" is set to "Anyone"
- [ ] You've authorized the script
- [ ] Web App URL is copied correctly
- [ ] Portfolio script.js has the correct URL
- [ ] GitHub Pages is enabled and site is live

---

## 🆘 Still Not Working?

If you've followed all steps and it's still not working:

1. **Create a brand new Google Sheet**
2. **Start fresh with the Apps Script**
3. **Create a NEW deployment** (don't reuse old one)
4. **Test with direct URL first** before testing on website

---

## 📞 Need More Help?

Share these details:
1. Screenshot of your Google Sheet (with column headers)
2. Screenshot of your Apps Script deployment settings
3. Your Web App URL
4. Any error messages from browser console (F12)

The form should work perfectly after following these steps! 🎉