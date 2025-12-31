# Vercel Deployment Guide

## Quick Deploy to Vercel

### Option 1: Deploy via Vercel CLI (Recommended)

1. **Install Vercel CLI**:
```powershell
npm install -g vercel
```

2. **Login to Vercel**:
```powershell
vercel login
```

3. **Deploy**:
```powershell
vercel
```

4. **Set Environment Variables** in Vercel Dashboard:
   - Go to your project settings
   - Add these variables:
     - `MONGODB_URI` = your MongoDB Atlas connection string
     - `JWT_SECRET` = your secret key
     - `VITE_API_URL` = your Vercel backend URL (will be shown after first deploy)

5. **Redeploy with env vars**:
```powershell
vercel --prod
```

### Option 2: Deploy via Vercel Dashboard

1. Go to [vercel.com](https://vercel.com)
2. Click "Add New Project"
3. Import your GitHub repository:
   `anuragchoudhary2313/Minor-Project-2-Volunteer-Opportunity-and-Resource-Exchange-`
4. Configure:
   - **Framework Preset**: Vite
   - **Root Directory**: ./
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`

5. **Add Environment Variables**:
   - `MONGODB_URI` = `mongodb+srv://anuragchoudhary603_db_user:kwd30YDYUJQy5RAt@cluster0.oj47e71.mongodb.net/helphub?retryWrites=true&w=majority&appName=Cluster0`
   - `JWT_SECRET` = `helphub_secret_key_change_this_in_production`
   - `VITE_API_URL` = `https://your-project-name.vercel.app/api` (update after first deploy)

6. Click "Deploy"

## Important Notes

### MongoDB Atlas Access
Make sure MongoDB Atlas allows connections from anywhere:
1. Go to MongoDB Atlas → Network Access
2. Click "Add IP Address"
3. Click "Allow Access from Anywhere" (0.0.0.0/0)
4. Save

### After First Deployment
1. Copy your Vercel deployment URL (e.g., `https://your-app.vercel.app`)
2. Update `VITE_API_URL` environment variable to: `https://your-app.vercel.app/api`
3. Redeploy or trigger a new build

### Updating Your App
```powershell
# Make changes, commit
git add .
git commit -m "Update message"
git push origin main

# Vercel will auto-deploy from GitHub
```

## Troubleshooting

### CORS Issues
If you get CORS errors, update `server/index.js`:
```javascript
app.use(cors({
  origin: ['https://your-app.vercel.app', 'http://localhost:5173'],
  credentials: true
}));
```

### Environment Variables Not Working
- Ensure all env vars are set in Vercel dashboard
- Redeploy after adding env vars
- Check spelling and values

### Build Fails
- Check build logs in Vercel dashboard
- Ensure all dependencies are in package.json
- Verify node version compatibility

## Production Checklist

- [ ] MongoDB Atlas whitelist: 0.0.0.0/0
- [ ] Strong JWT_SECRET set in Vercel
- [ ] VITE_API_URL points to production URL
- [ ] Test signup/login
- [ ] Test all features
- [ ] Update CORS to only allow your domain

## Custom Domain (Optional)

1. Go to Vercel Dashboard → Your Project → Settings → Domains
2. Add your custom domain
3. Follow DNS configuration instructions
4. Update VITE_API_URL if needed
