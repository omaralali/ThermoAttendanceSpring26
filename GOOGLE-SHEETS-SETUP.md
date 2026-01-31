# 🎯 Google Sheets Database Setup Guide

## Complete Step-by-Step Instructions

### Step 1: Create Google Sheet

1. Go to **https://sheets.google.com**
2. Click **"+ Blank"** to create new spreadsheet
3. Name it: **"Thermodynamics Attendance Spring 2025"**
4. In Row 1, add these headers (exact spelling):
   - A1: `Date`
   - B1: `Session`
   - C1: `Student ID`
   - D1: `Name`
   - E1: `Time`
   - F1: `Status`
   - G1: `IP Address`

5. **Copy the Spreadsheet ID** from the URL:
   - URL looks like: `https://docs.google.com/spreadsheets/d/1ABC123xyz.../edit`
   - The ID is the long string: `1ABC123xyz...`
   - Save this ID - you'll need it in Step 2

---

### Step 2: Create Google Apps Script

1. Go to **https://script.google.com**
2. Click **"New Project"**
3. Delete all existing code
4. Copy and paste this ENTIRE script:

```javascript
// REPLACE THIS with your Spreadsheet ID from Step 1
const SPREADSHEET_ID = 'PASTE_YOUR_SPREADSHEET_ID_HERE';

function doPost(e) {
  try {
    const sheet = SpreadsheetApp.openById(SPREADSHEET_ID).getActiveSheet();
    const data = JSON.parse(e.postData.contents);
    
    // Add row with attendance data
    sheet.appendRow([
      data.date,
      data.sessionCode,
      data.studentId,
      data.studentName,
      data.time,
      data.status,
      data.ipAddress
    ]);
    
    return ContentService.createTextOutput(JSON.stringify({success: true}))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({success: false, error: error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  try {
    const sheet = SpreadsheetApp.openById(SPREADSHEET_ID).getActiveSheet();
    const data = sheet.getDataRange().getValues();
    
    // Skip header row, return as JSON
    const records = data.slice(1).map(row => ({
      date: row[0],
      sessionCode: row[1],
      studentId: row[2],
      studentName: row[3],
      time: row[4],
      status: row[5],
      ipAddress: row[6]
    }));
    
    return ContentService.createTextOutput(JSON.stringify(records))
      .setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({error: error.toString()}))
      .setMimeType(ContentService.MimeType.JSON);
  }
}
```

5. **Replace the Spreadsheet ID**:
   - Find the line: `const SPREADSHEET_ID = 'PASTE_YOUR_SPREADSHEET_ID_HERE';`
   - Replace `'PASTE_YOUR_SPREADSHEET_ID_HERE'` with your actual ID from Step 1
   - Should look like: `const SPREADSHEET_ID = '1ABC123xyz...';`

6. **Save the project**:
   - Click the disk icon or press Ctrl+S
   - Name it: "Attendance Database"

---

### Step 3: Deploy Apps Script

1. Click **"Deploy"** button (top right)
2. Select **"New deployment"**
3. Click the gear icon ⚙️ next to "Select type"
4. Choose **"Web app"**
5. Fill in settings:
   - **Description**: "Attendance API"
   - **Execute as**: **"Me (your email)"**
   - **Who has access**: **"Anyone"**
6. Click **"Deploy"**
7. Click **"Authorize access"**
8. Choose your Google account
9. Click **"Advanced"** → **"Go to Attendance Database (unsafe)"** → **"Allow"**
10. **Copy the Web App URL** - it looks like:
    ```
    https://script.google.com/macros/s/AKfycbz.../exec
    ```
11. **Save this URL** - you'll need it in Step 4!

---

### Step 4: Update Your HTML Files

#### A. Update checkin-sheets.html:

1. Open `checkin-sheets.html` in a text editor
2. Find this line (near the top of the script section):
   ```javascript
   const GOOGLE_SCRIPT_URL = 'PASTE_YOUR_GOOGLE_SCRIPT_URL_HERE';
   ```
3. Replace with your URL from Step 3:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbz.../exec';
   ```
4. Save the file

#### B. Update dashboard-sheets.html:

1. Open `dashboard-sheets.html` in a text editor
2. Find this line:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'PASTE_YOUR_GOOGLE_SCRIPT_URL_HERE';
   ```
3. Replace with the SAME URL:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbz.../exec';
   ```
4. Also find this line:
   ```javascript
   <button class="btn-success" onclick="window.open('YOUR_GOOGLE_SHEET_URL', '_blank')">
   ```
5. Replace `YOUR_GOOGLE_SHEET_URL` with your Google Sheet URL from Step 1
6. Save the file

---

### Step 5: Upload to GitHub

1. Go to your GitHub repository
2. Upload these files:
   - `checkin-sheets.html`
   - `dashboard-sheets.html`
3. Update `simple-session-manager.html` to use `checkin-sheets.html` instead of `checkin.html`

---

### Step 6: Test It!

#### Test Check-in:
1. On your laptop: Open `https://yourusername.github.io/your-repo/simple-session-manager.html`
2. Generate a new session
3. On your phone: Scan the QR code
4. Fill in Student ID and Name
5. Click "Check In"
6. Should see success message!

#### Test Dashboard:
1. Open `https://yourusername.github.io/your-repo/dashboard-sheets.html`
2. Click "Refresh Data"
3. Should see the check-in you just did!

#### Verify in Google Sheets:
1. Open your Google Sheet
2. Should see a new row with the attendance data!

---

## 🎉 You're Done!

### How It Works:

1. **Student checks in** → Data sent to Google Apps Script → Saved to Google Sheet
2. **You open dashboard** → Reads from Google Sheet → Shows all attendance
3. **Data lives in Google Sheets** → You can access it anytime, from anywhere!

### Your URLs:

**For Students (via QR code):**
- `https://yourusername.github.io/your-repo/checkin-sheets.html?session=ABC123`

**For You:**
- Dashboard: `https://yourusername.github.io/your-repo/dashboard-sheets.html`
- Google Sheet: (your sheet URL)

---

## 🔧 Troubleshooting

### "Configuration Error" message?
- Make sure you replaced BOTH instances of `GOOGLE_SCRIPT_URL` in checkin-sheets.html AND dashboard-sheets.html

### Data not appearing in Google Sheet?
- Check the Apps Script URL is correct
- Make sure "Who has access" is set to "Anyone"
- Try re-deploying: Deploy → Manage Deployments → Edit → New Version → Deploy

### "Authorization required" error?
- Go back to Apps Script
- Run → Test as web app
- Authorize again

### Dashboard shows no data?
- Click "Refresh Data"
- Check your Google Sheet has data
- Open browser console (F12) for error messages

---

## 💡 Pro Tips

1. **Bookmark your dashboard** for quick access
2. **The Google Sheet is the source of truth** - you can edit it directly if needed
3. **Keep the Apps Script URL private** - don't share it with students
4. **Auto-refresh**: Dashboard refreshes every 30 seconds automatically
5. **Backup**: Export to CSV regularly for extra safety

---

## 📊 Using Your Data

### In Google Sheets:
- Sort by date, student, or status
- Use formulas to calculate attendance percentages
- Create pivot tables for analysis
- Share view-only link with TA

### Attendance Formula:
```
=COUNTIFS($C:$C,C2,$F:$F,"ON-TIME")/COUNTIF($C:$C,C2)
```
(Where C is Student ID column, F is Status column)

---

## 🔒 Privacy & Security

- Google Sheet is private (only you can access)
- Apps Script runs as you, accessing your sheet
- Students never see the sheet or other students' data
- IP addresses stored for fraud detection only

---

## 📞 Need Help?

If something isn't working:
1. Check you completed ALL steps above
2. Verify URLs are correct (no typos)
3. Check Google Apps Script logs: Apps Script → Executions
4. Open browser console (F12) to see error messages

---

**You're all set! Test it out and let me know if you run into any issues!** 🎓
