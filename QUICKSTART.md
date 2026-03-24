# Quick Start Guide - Finova AI

Get up and running in 5 minutes!

## Prerequisites Check

Before starting, ensure you have:
- ✅ Node.js v18 or higher (`node --version`)
- ✅ MongoDB installed or MongoDB Atlas account
- ✅ Google Gemini API key ([Get one here](https://makersuite.google.com/app/apikey))

---

## 🚀 5-Minute Setup

### Step 1: Install Dependencies (2 minutes)

```bash
# Install frontend dependencies
npm install

# Install backend dependencies
cd server
npm install
cd ..
```

### Step 2: Configure Environment (1 minute)

```bash
# Copy environment template
cd server
copy .env.example .env
```

Edit `server/.env` and add your API key:
```env
GEMINI_API_KEY=your_actual_api_key_here
```

### Step 3: Start MongoDB (30 seconds)

**Option A - Local MongoDB:**
```bash
# Windows
net start MongoDB

# macOS/Linux
sudo systemctl start mongod
```

**Option B - MongoDB Atlas:**
- Use your Atlas connection string in `.env`

### Step 4: Start the Application (1 minute)

**Terminal 1 - Backend:**
```bash
cd server
npm run dev
```

**Terminal 2 - Frontend:**
```bash
npm run dev
```

### Step 5: Access the App (30 seconds)

Open your browser and go to:
```
http://localhost:5173/landing
```

Click **"Try Demo"** to explore with pre-loaded data!

---

## 🎯 First Steps

### 1. Try the Demo Account
- Click "Try Demo" on landing page
- Explore the dashboard with sample data
- Chat with the AI advisor
- Run scenario simulations

### 2. Create Your Own Account
- Click "Get Started"
- Sign up with your email
- Update your financial profile
- Start getting personalized advice

### 3. Explore Features

**Dashboard:**
- View your financial health score
- See asset allocation
- Update your financial data

**AI Chat:**
- Ask: "What's my current financial health?"
- Ask: "Should I invest or pay off debt?"
- Toggle privacy mode to mask sensitive data

**Simulator:**
- Adjust monthly investment amount
- Set time horizon (years)
- Compare investment vs debt repayment
- See visual wealth projections

---

## 🐛 Troubleshooting

### Backend won't start?

**Check MongoDB:**
```bash
# Test MongoDB connection
mongosh
```

**Check port 5000:**
```bash
# Windows
netstat -ano | findstr :5000

# macOS/Linux
lsof -i :5000
```

### Frontend won't start?

**Check port 5173:**
```bash
# Windows
netstat -ano | findstr :5173
```

**Clear cache:**
```bash
rm -rf node_modules
npm install
```

### AI Chat not working?

**Verify API key:**
- Check `server/.env` has valid `GEMINI_API_KEY`
- Test API key at https://makersuite.google.com

**Check backend logs:**
- Look for errors in terminal running `npm run dev`
- Check for "AI Analysis Error" messages

### CORS errors?

**Update CORS origin:**
Edit `server/server.js`:
```javascript
app.use(cors({
  origin: 'http://localhost:5173', // Match your frontend URL
  credentials: true,
}));
```

---

## 📚 Next Steps

1. **Read the Documentation:**
   - `README.md` - Full project overview
   - `API_DOCUMENTATION.md` - API reference
   - `DEPLOYMENT.md` - Production deployment

2. **Customize the App:**
   - Update branding and colors
   - Add more financial instruments
   - Enhance AI prompts
   - Add new features

3. **Deploy to Production:**
   - Follow `DEPLOYMENT.md`
   - Set up monitoring
   - Configure backups
   - Enable security features

---

## 💡 Pro Tips

- Use the demo account to understand features before adding your data
- Enable privacy mode when sharing your screen
- Export your data regularly using MCP format
- Check the AI chat suggestions for common queries
- Adjust your risk profile in settings for better recommendations

---

## 🆘 Need Help?

- Check `TESTING.md` for detailed testing procedures
- Review `REQUIREMENTS_COMPLIANCE.md` for feature documentation
- Check browser console for frontend errors
- Check terminal for backend errors
- Verify all environment variables are set

---

**Happy Financial Planning! 🎉**
