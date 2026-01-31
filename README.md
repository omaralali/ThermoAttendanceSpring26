# Thermodynamics Class Attendance System

A complete QR code-based attendance tracking system for your Kuwait University Thermodynamics class.

## 📋 System Overview

This system consists of three HTML files:

1. **attendance-checkin.html** - Student check-in page (accessed via QR code)
2. **attendance-dashboard.html** - Admin dashboard for viewing attendance
3. **qr-code-generator.html** - Tool to generate QR codes

## ⏰ Class Schedule

- **Days:** Sunday, Tuesday, Thursday
- **Time:** 1:00 PM
- **Semester:** February 1, 2025 - Mid-May 2025

## 🎯 Attendance Status Rules

- **ON-TIME:** Check-in before or at 1:00 PM (13:00)
- **LATE:** Check-in between 1:01 PM - 1:05 PM (13:01-13:05)
- **VERY LATE:** Check-in after 1:05 PM (13:05+)

## 🚀 Quick Start Guide

### Step 1: Host the Files

You need to upload these HTML files to a web server. Here are some free options:

#### Option A: GitHub Pages (Recommended)
1. Create a GitHub account at https://github.com
2. Create a new repository called "attendance-system"
3. Upload all three HTML files
4. Go to Settings → Pages
5. Enable GitHub Pages from the main branch
6. Your URL will be: `https://yourusername.github.io/attendance-system/attendance-checkin.html`

#### Option B: Netlify
1. Go to https://netlify.com
2. Sign up for a free account
3. Drag and drop all three HTML files
4. Get your URL (e.g., `https://your-site.netlify.app/attendance-checkin.html`)

#### Option C: Local Network (For Testing)
1. Install Python on your computer
2. Open terminal/command prompt in the folder with the files
3. Run: `python -m http.server 8000`
4. Access at: `http://your-computer-ip:8000/attendance-checkin.html`
   - Find your IP: Windows (`ipconfig`), Mac (`ifconfig`)
   - Students must be on the same WiFi network

### Step 2: Generate QR Code

1. Open `qr-code-generator.html` in your browser
2. Paste the URL of your hosted `attendance-checkin.html`
3. Click "Generate QR Code"
4. Download or print the QR code

### Step 3: Display in Class

- Print the QR code on paper (A4 size recommended)
- Or display it on a projector/screen
- Students scan with their phone cameras to check in

### Step 4: Monitor Attendance

1. Open `attendance-dashboard.html` in your browser
2. Bookmark this page for easy access
3. View real-time attendance as students check in
4. Export data to CSV for grading

## 📊 Dashboard Features

### View Modes
- **All Records:** Complete attendance history
- **Today's Attendance:** Current class session
- **By Student:** Individual student summaries
- **By Date:** Filter by specific class date

### Statistics Dashboard
- Total number of unique students
- Total class sessions held
- Total check-ins recorded
- Overall on-time percentage

### Student Summary View
Shows for each student:
- Total attendance count
- On-time count
- Late count
- Very late count

### Export Options
- **CSV Export:** Download all records as spreadsheet
- **Auto-refresh:** Dashboard updates every 30 seconds

## 💾 Data Storage

The system uses two storage methods:

1. **Browser Local Storage:** Stores data in the browser
2. **Persistent Storage:** Syncs data across devices (if supported)

### Important Notes:
- Data is stored locally in the browser by default
- For multi-device access, both check-in and dashboard pages use shared storage
- Data persists across browser sessions
- **Backup regularly** by exporting to CSV

## 🔧 Troubleshooting

### Students can't access the check-in page
- Verify the URL is correct
- Check that the files are properly hosted
- Ensure students have internet connection

### QR code doesn't work
- Make sure the URL starts with `http://` or `https://`
- Test the URL in a browser first
- Regenerate the QR code if needed

### Dashboard shows no data
- Click the "Refresh" button
- Check that students are using the correct check-in page
- Verify browser allows local storage

### Data disappeared
- Check if browser cache was cleared
- Always export to CSV as backup
- Consider hosting on a server with database backup

### Multiple students checking in simultaneously
- The system handles concurrent check-ins
- Each student gets timestamped individually
- Duplicate check-ins on the same day are prevented

## 📱 Student Instructions

Share these simple steps with your students:

1. **Scan the QR code** displayed on the board with your phone camera
2. **Enter your Student ID** (your university ID number)
3. **Enter your Full Name** (as registered at the university)
4. **Click "Check In"**
5. **Confirm** you see a success message

### Important Student Notes:
- Arrive before 1:00 PM to be marked "ON-TIME"
- You can only check in once per class
- Make sure to check in before leaving class
- Take a screenshot of your confirmation if needed

## 📈 Grading & Reports

### Export Attendance Data
1. Open the dashboard
2. Click "Export CSV"
3. Open in Excel or Google Sheets
4. Calculate attendance percentages per student

### Suggested Grading Formula
```
Attendance Grade = (On-Time × 100%) + (Late × 80%) + (Very Late × 60%)
                   ÷ Total Classes
```

Example calculation in Excel:
```
=((ON_TIME_COUNT*100)+(LATE_COUNT*80)+(VERY_LATE_COUNT*60))/(TOTAL_CLASSES*100)
```

## 🔒 Privacy & Security

- Student data stays in the browser (no external server)
- No personally identifiable information beyond what students enter
- Only student ID and name are collected
- Data can be cleared anytime from the dashboard

## 🛠️ Customization

### Change Class Times
Edit the `getAttendanceStatus()` function in `attendance-checkin.html`:

```javascript
function getAttendanceStatus(checkInTime) {
    const hour = checkInTime.getHours();
    const minute = checkInTime.getMinutes();
    
    // Modify these values for different times
    if (hour < 13) {  // Change 13 to your class hour (24-hour format)
        return 'ON-TIME';
    }
    // ... rest of the code
}
```

### Change Semester Dates
Update the README or add date validation in the code if needed.

### Customize Appearance
- Colors can be changed in the `<style>` sections
- Modify the gradient backgrounds
- Change button styles and fonts

## 📞 Support

For technical issues:
1. Check this README first
2. Export your data as backup
3. Try refreshing the browser
4. Clear browser cache if problems persist

## 📄 File Structure

```
attendance-system/
├── attendance-checkin.html    (Student check-in page)
├── attendance-dashboard.html  (Admin dashboard)
├── qr-code-generator.html     (QR code generator)
└── README.md                  (This file)
```

## ✅ Best Practices

1. **Before Each Class:**
   - Display QR code prominently
   - Arrive early to test the system
   - Have dashboard open on your device

2. **During Class:**
   - Monitor check-ins in real-time
   - Note any technical issues
   - Keep QR code visible entire class

3. **After Class:**
   - Export attendance data
   - Review any anomalies
   - Backup data regularly

4. **Weekly:**
   - Export CSV backup
   - Review attendance trends
   - Update students on their status

## 🎓 Semester Schedule

Based on your schedule (Sun/Tue/Thu starting Feb 1, 2025):
- **Total Weeks:** ~14 weeks
- **Expected Classes:** ~42 classes
- **First Class:** Sunday, February 1, 2025
- **Last Class:** Mid-May 2025

## 📊 Sample Reports

The dashboard automatically tracks:
- Attendance by date
- Attendance by student
- Punctuality trends
- Overall class statistics

All data can be exported to CSV for further analysis in Excel.

---

## 🎉 You're All Set!

Your attendance system is ready to use. Good luck with your Thermodynamics class at Kuwait University!

For questions or improvements, you can modify these files as needed.
