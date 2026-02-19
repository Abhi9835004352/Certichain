# Render.com Deployment Guide

This guide explains how to deploy the Certichain frontend to Render.com.

## Why "Not Found" Error Occurs

Render's static site hosting serves files as-is from your build folder. When you navigate to a route like `/verify` or `/admin`, the server looks for a file at that path and doesn't find it because React Router handles routing on the client side.

**Solution:** The `_redirects` file in the public folder tells the server to serve `index.html` for all non-file routes, allowing React Router to take over.

## Prerequisites

- Render.com account (free at https://render.com)
- GitHub repository with code pushed
- Environment variables from the `.env` file

## Deployment Methods

### Method 1: Using Web Service (Recommended)

1. **Push code to GitHub**
   ```bash
   git add .
   git commit -m "Add Render deployment files"
   git push origin main
   ```

2. **Go to [Render Dashboard](https://dashboard.render.com)**
   - Click "New +" → "Web Service"
   - Connect your GitHub account
   - Select the Certichain repository
   - Configure:
     ```
     Name: certichain-frontend
     Root Directory: frontend
     Environment: Node
     Build Command: npm install && npm run build
     Start Command: serve -s build
     ```

3. **Set Environment Variables**
   - In the service settings, add all variables:
   ```
   REACT_APP_ALGOD_SERVER=https://testnet-api.algonode.cloud
   REACT_APP_ALGOD_TOKEN=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
   REACT_APP_INDEXER_SERVER=https://testnet-idx.algonode.cloud
   REACT_APP_APP_ID=755789606
   REACT_APP_APP_ADDRESS=PJB7TQATUORZIFL3ZN3N4RW5NXZQV2WCQ4MG2U7ZS7BPMHM6DII7Q6NRPI
   REACT_APP_PINATA_KEY=your_pinata_key_here
   REACT_APP_PINATA_SECRET=your_pinata_secret_here
   ```

4. **Deploy**
   - Click "Create Web Service"
   - Render will build and deploy automatically

### Method 2: Using Static Site (Only if Not Using API)

If you only need static hosting (no backend API behind it):

1. Add `_redirects` file (already provided)
2. Use Render's Static Site feature
3. Deploy the `build` folder

## Configuration Files

### `_redirects` (in public folder)
```
/* /index.html 200
```
This file redirects all 404s to index.html, allowing React Router to handle routing.

### `render.yaml` (root of project)
Configuration file for Render's native deployment (optional if using dashboard).

## Troubleshooting

### Still Getting "Not Found"?

1. **Check if `_redirects` file exists**
   ```bash
   ls -la public/_redirects
   ```

2. **Verify it's in the build**
   - After running `npm run build`, check:
   ```bash
   ls -la build/_redirects
   ```

3. **Check Render logs**
   - In Render dashboard, go to Logs tab
   - Look for build and deployment errors

4. **Rebuild on Render**
   - In service settings, click "Clear build cache"
   - Click "Deploy" to rebuild

### Environment Variables Not Working

1. Verify all `REACT_APP_*` prefixed variables are set
2. Rebuild the service after adding variables
3. Check that variables are in the correct service (not just the account)

### Port Issues

- Render automatically assigns a port
- Don't hardcode ports in your code
- Use environment variables for port configuration

## Local Testing

Before deploying to Render, test the build locally:

```bash
# Build the app
npm run build

# Install serve globally
npm install -g serve

# Serve the build
serve -s build

# App will be at http://localhost:3000
```

Then navigate to different routes to verify React Router works correctly.

## Performance Optimization

### Caching
Render caches builds automatically. Clear cache if needed:
1. Go to Service Settings
2. Click "Clear build cache"
3. Redeploy

### Building Only When Needed
- Render only rebuilds when you push to the connected branch
- Manual redeploys don't trigger new builds

## Custom Domain

To add a custom domain:
1. Go to service settings
2. Click "Add Custom Domain"
3. Update DNS records with Render's nameservers
4. Wait for propagation (typically 24 hours)

## Monitoring

- Check build logs in the Logs tab
- Monitor application runtime logs
- Use browser DevTools to debug client-side issues

## Additional Resources

- [Render Documentation](https://docs.render.com)
- [Deploying Create React App](https://docs.render.com/deploy-react)
- [Environment Variables](https://docs.render.com/environment-variables)
- [Web Service Guide](https://docs.render.com/web-services)
