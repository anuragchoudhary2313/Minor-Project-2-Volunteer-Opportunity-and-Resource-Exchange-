# Quick Start Guide - Help Hub with MongoDB

## Prerequisites Check

- [ ] Node.js installed (v18+) - Run `node --version`
- [ ] MongoDB installed OR MongoDB Atlas account
- [ ] npm installed - Run `npm --version`

## Step-by-Step Setup

### Step 1: MongoDB Setup (Choose One)

#### Option A: Local MongoDB (Windows)

```powershell
# Download from: https://www.mongodb.com/try/download/community
# After installation, start MongoDB:
mongod
```

#### Option B: MongoDB Atlas (Cloud - Recommended)

1. Go to https://www.mongodb.com/cloud/atlas
2. Create free account
3. Create a cluster (M0 Free tier)
4. Click "Connect" → "Connect your application"
5. Copy the connection string (looks like: `mongodb+srv://username:password@cluster.mongodb.net/...`)

### Step 2: Backend Setup

```powershell
# Navigate to server directory
cd server

# Install dependencies
npm install

# Create and edit .env file
# Copy .env.example to .env
copy .env.example .env

# Edit .env and set:
# MONGODB_URI=your_mongodb_connection_string
# JWT_SECRET=any_random_string_at_least_32_characters
# PORT=5000

# Start the backend server
npm run dev
```

**Expected Output:**

```
Server is running on port 5000
MongoDB Connected: cluster0.xxxxx.mongodb.net
```

### Step 3: Frontend Setup (New Terminal)

```powershell
# Navigate back to root directory
cd ..

# Install dependencies
npm install

# Start the frontend
npm run dev
```

**Expected Output:**

```
  VITE v5.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
  ➜  Network: use --host to expose
```

### Step 4: Test the Application

1. **Open Browser**: Go to `http://localhost:5173`

2. **Create Account**:

   - Click "Sign Up"
   - Enter email, password, and full name
   - Click "Sign Up"
   - You should be logged in and redirected to Dashboard

3. **Test Features**:
   - Update profile information
   - Create a volunteer opportunity
   - Create a resource listing
   - Browse opportunities and resources

## Common Issues & Solutions

### Issue: "Cannot connect to MongoDB"

**Solution**:

- Check if MongoDB is running (local) or connection string is correct (Atlas)
- Verify MONGODB_URI in `server/.env`

### Issue: "Port 5000 already in use"

**Solution**:

- Change PORT in `server/.env` to another port (e.g., 5001)
- Update VITE_API_URL in root `.env` accordingly

### Issue: "Module not found" errors

**Solution**:

- Run `npm install` in both root and server directories
- Delete `node_modules` and `package-lock.json`, then reinstall

### Issue: Frontend can't connect to backend

**Solution**:

- Verify backend is running on http://localhost:5000
- Check `.env` file has correct VITE_API_URL
- Restart Vite dev server after changing .env

## Environment Variables Reference

### Backend (server/.env)

```env
MONGODB_URI=mongodb://localhost:27017/helphub
# OR for Atlas:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/helphub

JWT_SECRET=your_secret_key_minimum_32_characters_long
PORT=5000
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:5000/api
```

## Default Test Data

The application starts with an empty database. To add test data:

1. Create a user account
2. Login with that account
3. Manually create opportunities, resources, etc.

## Stopping the Application

- Frontend: Press `Ctrl+C` in the terminal running Vite
- Backend: Press `Ctrl+C` in the terminal running the server
- MongoDB (local): You can stop the mongod process or leave it running

## Next Steps

- Read `MIGRATION_SUMMARY.md` for detailed changes
- Read `README_MONGODB.md` for full documentation
- Explore the codebase in `/src` and `/server`
- Customize the application for your needs

## Need Help?

1. Check console logs in browser (F12 → Console)
2. Check terminal output for backend errors
3. Review error messages carefully
4. Ensure all environment variables are set correctly
5. Verify MongoDB connection is established

## Production Deployment

For production deployment:

1. Use MongoDB Atlas instead of local MongoDB
2. Set strong JWT_SECRET (use a password generator)
3. Update VITE_API_URL to your production backend URL
4. Build frontend: `npm run build`
5. Deploy frontend `dist` folder to Vercel/Netlify
6. Deploy backend to Heroku/Railway/DigitalOcean
7. Set all environment variables in your hosting platform

---

**Congratulations!** 🎉 Your Help Hub application with MongoDB is now running!
