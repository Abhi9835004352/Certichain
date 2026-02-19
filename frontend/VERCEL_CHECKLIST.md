# Vercel Deployment Checklist

## Pre-Deployment Checklist

### Configuration Files
- [x] `vercel.json` - Created with build settings and rewrites
- [x] `.env.example` - Created with placeholder values
- [x] `.vercelignore` - Created to exclude unnecessary files
- [x] `.gitignore` - Updated to exclude .env files

### Package Configuration
- [x] `package.json` - Updated with dev script for local testing
- [x] Build command verified: `npm run build`
- [x] Output directory verified: `build`

### Environment Variables
Required environment variables for Vercel:
- [x] `REACT_APP_ALGOD_SERVER`
- [x] `REACT_APP_ALGOD_TOKEN`
- [x] `REACT_APP_INDEXER_SERVER`
- [x] `REACT_APP_APP_ID`
- [x] `REACT_APP_APP_ADDRESS`
- [x] `REACT_APP_PINATA_KEY`
- [x] `REACT_APP_PINATA_SECRET`

### Code Quality
- [x] No hardcoded API keys or sensitive data
- [x] Proper error handling for API calls
- [x] CORS-compatible API calls to Algorand nodes
- [x] Pinata API integration uses environment variables

### Testing Before Deployment
```bash
# 1. Install dependencies
npm install

# 2. Test build locally
npm run build

# 3. Test development locally
npm run dev

# 4. Check environment variables are loaded
echo $REACT_APP_ALGOD_SERVER
```

## Deployment Steps

### Via Vercel Dashboard
1. Push code to GitHub
2. Connect GitHub repository to Vercel
3. Add environment variables in Vercel Settings
4. Click Deploy
5. Wait for build to complete

### Via Vercel CLI
```bash
# Install Vercel CLI
npm install -g vercel

# Login to Vercel
vercel login

# Deploy
vercel --prod
```

## Post-Deployment Verification

### Check Deployment
- [ ] Access deployed URL
- [ ] Verify all pages load correctly
- [ ] Test wallet connection (Defly/Pera)
- [ ] Test credential creation flow
- [ ] Test IPFS upload functionality
- [ ] Check console for any errors

### Monitoring
- [ ] Enable Vercel analytics
- [ ] Set up error tracking
- [ ] Monitor API calls to Algorand nodes
- [ ] Check build logs for warnings

## Troubleshooting

If deployment fails:
1. Check Vercel build logs
2. Verify environment variables are set
3. Run `npm run build` locally to reproduce issues
4. Check package-lock.json is up to date
5. Verify all dependencies are compatible

## Additional Notes

- The app is configured for React Router client-side routing
- All API calls use environment variables from `.env`
- CORS should work since external APIs are used directly
- The frontend connects to public Algorand testnet
