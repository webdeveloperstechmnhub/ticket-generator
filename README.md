# 🎫 Offline Ticket Generator - Zonex 2026

## Overview
This is a standalone ticket generator system for creating tickets for participants who registered offline (cash/in-person registrations).

## Features
✅ Manual registration form with all participant details  
✅ Automatic registration ID generation (format: `ZNX2026-XXXXXX`)  
✅ QR code generation for venue entry  
✅ Email delivery with ticket details  
✅ Downloadable HTML ticket  
✅ Team member support  
✅ Multiple payment modes (Cash, UPI, Card, Complimentary)  
✅ Database integration with User model  

## Setup Instructions

### 1. Backend Setup

#### Add Route to Server
Edit `backend/server.js` and add the offline ticket routes:

```javascript
const offlineTicketRoutes = require("./routes/offlineTicketRoutes");

// Add this line with other routes
app.use("/api/ticket", offlineTicketRoutes);
```

#### Update User Model
The User model has been updated to include a `paymentMode` field. Make sure your existing `backend/models/User.js` includes this field.

### 2. Frontend Setup

#### Update Backend URL
Edit `ticket/index.html` and update the backend URL (around line 329):

```javascript
const BACKEND_URL = 'http://localhost:5000'; // Change to your backend URL
```

For production, use:
```javascript
const BACKEND_URL = 'https://your-backend-url.com';
```

### 3. Running the System

#### Start Backend Server
```bash
cd backend
npm start
```

#### Open Frontend
Simply open `ticket/index.html` in your browser:
```bash
# Windows
start ticket/index.html

# Mac/Linux
open ticket/index.html
```

Or use a local server:
```bash
# Using Python
cd ticket
python -m http.server 8080

# Using Node.js (http-server)
npx http-server ticket -p 8080
```

Then visit: `http://localhost:8080`

## Usage

### Generating a Ticket

1. **Fill Participant Details**
   - Name, mobile, email, city
   - College and course details
   - Category (Individual/Team/Visitor)

2. **Select Activities**
   - Choose skills/activities participant is interested in
   - Multiple selections allowed

3. **Team Members** (if applicable)
   - Add team member names (comma-separated)
   - Automatically saved with ticket

4. **Pass & Payment**
   - Select pass type
   - Enter amount paid
   - Select payment mode (Cash/UPI/Card/Complimentary)

5. **Generate Ticket**
   - Click "Generate Ticket" button
   - QR code and registration ID generated automatically
   - Ticket preview displayed

6. **Download or Email**
   - Download HTML ticket for printing
   - Send email directly to participant

### Registration ID Format
- Format: `ZNX2026-XXXXXX`
- Example: `ZNX2026-234567`
- Automatically generated and unique

## API Endpoints

### POST `/api/ticket/generate`
Generate offline ticket

**Request Body:**
```json
{
  "fullName": "John Doe",
  "mobile": "9876543210",
  "email": "john@example.com",
  "city": "Muzaffarnagar",
  "college": "ABC College",
  "courseYear": "B.Tech 2nd Year",
  "category": "Individual",
  "subCategory": ["Coding", "Design"],
  "teamMembers": [],
  "passName": "Pro Participation - ₹150",
  "amountPaid": 150,
  "paymentMode": "Cash",
  "portfolio": "",
  "github": "",
  "instagram": ""
}
```

**Response:**
```json
{
  "msg": "Ticket generated successfully",
  "registrationId": "ZNX2026-234567",
  "qrCode": "data:image/png;base64,...",
  "user": { /* user object */ }
}
```

### POST `/api/ticket/send-email`
Send ticket via email

**Request Body:**
```json
{
  "userId": "mongodb-user-id"
}
```

**Response:**
```json
{
  "msg": "Email sent successfully",
  "email": "john@example.com"
}
```

## Security Considerations

### Email Uniqueness
- System checks for duplicate email addresses
- Prevents multiple registrations with same email
- Returns existing registration ID if duplicate found

### Data Validation
- Mobile number must be 10 digits
- Email format validation
- At least one activity must be selected
- Required fields enforced

## Troubleshooting

### CORS Issues
If you get CORS errors, make sure your backend has CORS enabled:

```javascript
const cors = require('cors');
app.use(cors());
```

### Email Not Sending
- Check Resend API key in `.env`
- Verify domain is verified in Resend dashboard
- Check backend logs for error messages

### Database Connection
- Ensure MongoDB is running
- Check connection string in `backend/config/db.js`

### QR Code Not Generating
- Ensure `qrcode` package is installed: `npm install qrcode`
- Check backend logs for errors

## File Structure

```
ticket/
├── index.html          # Main ticket generator interface
└── README.md           # This file

backend/
├── controllers/
│   └── offlineTicketController.js    # Offline ticket logic
├── routes/
│   └── offlineTicketRoutes.js        # API routes
└── models/
    └── User.js         # Updated with paymentMode field
```

## Support

For issues or questions:
- Email: techmnhub.team@gmail.com
- Check backend logs for detailed error messages
- Ensure all dependencies are installed

## License
© 2026 TechMNHub. All rights reserved.
"# ticket-generator" 
