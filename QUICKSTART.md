# 🚀 Quick Start Checklist

## Pre-Flight

- [ ] Node.js 16+ installed (`node --version`)
- [ ] npm installed (`npm --version`)
- [ ] Git cloned locally
- [ ] Code editor open (VSCode, etc.)

## Setup Phase

### Option A: Automated Setup (Recommended)

**macOS/Linux:**
```bash
bash setup.sh
```

**Windows:**
```bash
setup.bat
```

### Option B: Manual Setup

**Frontend Setup:**
```bash
cd frontend
npm install
```

**Backend Setup:**
```bash
cd backend
npm install
cp .env.example .env
# Edit .env with Gmail credentials
```

## Gmail Configuration (Required)

1. ✅ Go to [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)
2. ✅ Ensure 2-step verification is enabled
3. ✅ Select "Mail" and "Windows Computer" (or your device)
4. ✅ Generate App Password (16 characters, no spaces)
5. ✅ Copy password to `backend/.env` as `EMAIL_PASSWORD`
6. ✅ Set `EMAIL_USER=your-email@gmail.com`

Example `.env`:
```env
PORT=3001
FRONTEND_URL=http://localhost:5173
EMAIL_USER=your.email@gmail.com
EMAIL_PASSWORD=xxxx xxxx xxxx xxxx
```

## Running the Project

### Terminal 1 - Frontend
```bash
cd frontend
npm run dev
```
✅ Watch for: `VITE v6.x.x ready in xxx ms`
✅ Access: http://localhost:5173

### Terminal 2 - Backend
```bash
cd backend
npm run dev
```
✅ Watch for: `Backend server running on port 3001`
✅ Test: `curl http://localhost:3001/api/health`

## Testing Email Verification

1. [ ] Open http://localhost:5173 in browser
2. [ ] Scroll to bottom, click "Join the Ring" button
3. [ ] Modal should open
4. [ ] Enter your Laurier ID (for example `abcd1234`)
5. [ ] Click "Send Verification Code"
6. [ ] Check your email inbox for verification code
7. [ ] Copy the 6-digit code
8. [ ] Paste into modal's code field
9. [ ] Click "Verify Email"
10. [ ] See success screen: "Welcome to the Webring!"

## Troubleshooting Quick Fixes

### Backend won't start
```bash
# Check port 3001 not in use
lsof -i :3001  # macOS/Linux
netstat -ano | findstr :3001  # Windows
```

### Email not sending
- [ ] Check `.env` has `EMAIL_USER` and `EMAIL_PASSWORD`
- [ ] Verify Gmail App Password (16 chars, copy exactly)
- [ ] Check Gmail 2-step verification is ON
- [ ] Look at backend terminal for error messages

### Frontend can't reach backend
- [ ] Verify backend is running on http://localhost:3001
- [ ] Check browser console (F12) for error details
- [ ] Look for CORS errors in Network tab
- [ ] Ensure firewall allows localhost:3001

### Port Already in Use
```bash
# Kill process on port 5173 (frontend)
lsof -i :5173 | grep LISTEN | awk '{print $2}' | xargs kill -9

# Kill process on port 3001 (backend)
lsof -i :3001 | grep LISTEN | awk '{print $2}' | xargs kill -9
```

## File Locations Reference

| What | Location |
|------|----------|
| Frontend | `frontend/` |
| Backend | `backend/` |
| Join Modal | `frontend/src/components/JoinRing/` |
| Footer | `frontend/src/components/Footer/` |
| API Server | `backend/index.js` |
| Verified Members | `backend/verified-members.json` |
| Setup Docs | `SETUP.md` |
| Email Docs | `EMAIL_SETUP.md` |

## Common Commands

```bash
# Frontend
cd frontend && npm run dev          # Start dev server
cd frontend && npm run build        # Build for production
cd frontend && npm run preview       # Preview production build

# Backend
cd backend && npm run dev           # Start with auto-restart
cd backend && npm start             # Start production
cd backend && node --watch index.js # Manual restart

# Testing
curl http://localhost:3001/api/health  # Check backend
open http://localhost:5173              # Open frontend
```

## Next Steps After Setup Works

1. **Deploy Frontend**
   - Push to GitHub
   - Vercel auto-deploys main branch
   - Update `FRONTEND_URL` in backend .env

2. **Deploy Backend**
   - Choose: Vercel, Heroku, Railway, or VPS
   - Set environment variables
   - Test production email sending

3. **Add Member Storage**
   - Optional: Connect to MongoDB or PostgreSQL
   - Optional: Sync verified members to members.json

4. **Customize**
   - Update email template in `backend/index.js`
   - Change timeout from 10 minutes
   - Add more validation rules

## Support Resources

- **Setup Guide:** `SETUP.md`
- **Email Setup:** `EMAIL_SETUP.md`
- **Backend Docs:** `backend/README.md`
- **Frontend Code:** `frontend/src/`
- **GitHub Issues:** Report bugs here

## Success Indicators ✅

- [ ] `npm run dev` starts without errors
- [ ] Frontend loads at http://localhost:5173
- [ ] Backend health check works
- [ ] Gmail is configured
- [ ] Modal opens on "Join Ring" click
- [ ] Can enter email and request code
- [ ] Code arrives in email within 30 seconds
- [ ] Code verification works
- [ ] Success screen displays
- [ ] Verified member saved to file

**You're ready to go! 🎉**
