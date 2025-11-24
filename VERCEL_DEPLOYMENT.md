# 🚀 Backend Deployment to Vercel - Step by Step

## 📋 Current Status
✅ Backend files prepared in: `C:\Users\lenovo\Desktop\SIH Project\aquanova-backend-deploy`
✅ Git initialized and committed
✅ Vercel configuration ready
✅ Node.js 22.x configured

---

## 🎯 STEP 1: Create GitHub Repository

1. Go to: https://github.com/new
2. Repository name: `aquanova-backend`
3. Description: `AquaNova Backend API for Ocean Analytics Platform`
4. Make it **Public** or **Private** (your choice)
5. **DON'T** initialize with README (we already have one)
6. Click **"Create repository"**

---

## 🎯 STEP 2: Push Backend to GitHub

Open PowerShell and run these commands:

```powershell
cd "C:\Users\lenovo\Desktop\SIH Project\aquanova-backend-deploy"

git remote add origin https://github.com/sakthi44710/aquanova-backend.git

git push -u origin main
```

✅ Your backend code is now on GitHub!

---

## 🎯 STEP 3: Deploy to Vercel

### A. Import Project to Vercel

1. Go to: https://vercel.com
2. Click **"Add New Project"**
3. Click **"Import Git Repository"**
4. Find and select **"aquanova-backend"**
5. Click **"Import"**

### B. Configure Deployment Settings

**Framework Preset:** Other
**Root Directory:** `./` (leave as default)
**Build Command:** (leave empty)
**Output Directory:** (leave empty)
**Install Command:** `npm install`

### C. Add Environment Variables

Click **"Environment Variables"** and add these:

#### Required Variables:

1. **DB_HOST**
   - Value: `gateway01.ap-southeast-1.prod.aws.tidbcloud.com`

2. **DB_PORT**
   - Value: `4000`

3. **DB_USER**
   - Value: `2ZGMvSRghBi5aJw.root`

4. **DB_PASSWORD**
   - Value: `c5RZNwi4h8GQ6NZk`

5. **DB_NAME**
   - Value: `test`

6. **JWT_SECRET**
   - Value: Generate a new one using:
   ```powershell
   node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
   ```
   - Copy the output and paste as value

7. **EMAIL_USER**
   - Value: `testingforproject07@gmail.com`

8. **EMAIL_PASSWORD**
   - Value: `mrvxwiglfdwxcwkk`

9. **PORT**
   - Value: `5000`

**For ALL variables, select:** Production, Preview, Development

### D. Deploy!

Click **"Deploy"** button and wait (2-5 minutes)

---

## 🎯 STEP 4: Get Your Backend URL

After deployment completes:

1. You'll see: **"Congratulations! Your project has been deployed"**
2. Your backend URL will be something like:
   ```
   https://aquanova-backend.vercel.app
   ```
3. **Copy this URL!**

Test it by visiting:
```
https://aquanova-backend.vercel.app/api/health
```

You should see:
```json
{
  "status": "OK",
  "message": "AquaNova API is running"
}
```

---

## 🎯 STEP 5: Update Frontend with Backend URL

### A. Update Frontend Environment Variable

1. Go to your **frontend** project on Vercel (aquanova)
2. Go to **Settings** → **Environment Variables**
3. Find **REACT_APP_API_URL** and click **Edit**
4. Change value to: `https://aquanova-backend.vercel.app/api`
5. Click **Save**

### B. Redeploy Frontend

1. Go to **Deployments** tab
2. Click **"..."** on latest deployment
3. Click **"Redeploy"**

---

## 🎯 STEP 6: Test Complete Integration

### Test Backend Endpoints:

1. **Health Check:**
   ```
   https://your-backend.vercel.app/api/health
   ```

2. **Try Signup** from your frontend:
   - Go to your frontend URL
   - Click Signup
   - Enter name and email
   - Check if OTP email is received

3. **Check Logs:**
   - Vercel Dashboard → Your Backend Project → **Runtime Logs**
   - Look for any errors

---

## ⚠️ Important Notes

### Database Connection
- ✅ TiDB Cloud allows connections from Vercel IPs
- ✅ No additional configuration needed

### CORS
Your backend already has CORS enabled for all origins:
```javascript
app.use(cors());
```

For production, you might want to restrict to your frontend domain only.

### Serverless Limitations
- ⏱️ 10 second timeout on free tier
- 🔄 Each request creates a new serverless function instance
- 💾 No persistent file storage

---

## 🐛 Troubleshooting

### Issue: "502 Bad Gateway"
**Solution:** Check Runtime Logs in Vercel for errors

### Issue: "Database connection failed"
**Solution:** 
- Verify environment variables are set correctly
- Check TiDB Cloud connection settings
- Ensure database is accessible from 0.0.0.0/0

### Issue: "Module not found"
**Solution:** Make sure `package.json` has all dependencies

### Issue: Email not sending
**Solution:**
- Verify Gmail app password is correct
- Check if Less Secure Apps is enabled (if using regular password)
- Use App Password from Google Account settings

---

## 🔒 Security Checklist

✅ Generate new JWT_SECRET for production
✅ Environment variables are not in code
✅ .env is in .gitignore
✅ Use strong passwords
✅ Enable 2FA on GitHub and Vercel

---

## 📊 Monitoring

### Check Backend Health:
```
https://your-backend.vercel.app/api/health
```

### View Logs:
- Vercel Dashboard → Project → Runtime Logs
- Check for errors, warnings, and API calls

### Monitor Database:
- TiDB Cloud Dashboard
- Check connection count
- Monitor query performance

---

## 🎉 Success Checklist

- [ ] Backend deployed to Vercel
- [ ] Health endpoint returns OK
- [ ] Frontend environment variable updated
- [ ] Signup flow works (OTP email received)
- [ ] Login works
- [ ] All features accessible
- [ ] No errors in browser console
- [ ] No errors in Vercel logs

---

## 🔗 Your URLs

**Frontend:** `https://aquanova-[your-username].vercel.app`
**Backend:** `https://aquanova-backend.vercel.app`
**API Base:** `https://aquanova-backend.vercel.app/api`

---

## 📝 API Endpoints

```
POST   /api/auth/send-otp       - Send OTP to email
POST   /api/auth/verify-otp     - Verify OTP code
POST   /api/auth/signup         - Create account
POST   /api/auth/login          - Login user
GET    /api/auth/me             - Get current user (protected)

GET    /api/chat/history        - Get all conversations (protected)
GET    /api/chat/history/:id    - Get specific conversation (protected)
POST   /api/chat/history        - Create conversation (protected)
PUT    /api/chat/history/:id    - Update conversation (protected)
DELETE /api/chat/history/:id    - Delete conversation (protected)

GET    /api/health              - Health check
```

---

**You're all set! 🚀 Follow these steps and your full-stack application will be live!**
