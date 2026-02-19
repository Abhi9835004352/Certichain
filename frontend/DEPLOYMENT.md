# Vercel Deployment Guide

This guide explains how to deploy the Certichain frontend to Vercel.

## Prerequisites

- Vercel account (free at https://vercel.com)
- GitHub account with the repository pushed
- Environment variables from the `.env` file

## Deployment Steps

### 1. Connect Repository to Vercel

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Click "Add New..." → "Project"
3. Select "Import Git Repository"
4. Connect your GitHub account and select the Certichain repository
5. Click "Import"

### 2. Configure Environment Variables

In the Vercel project settings:

1. Go to **Settings** → **Environment Variables**
2. Add the following variables:

```
REACT_APP_ALGOD_SERVER = https://testnet-api.algonode.cloud
REACT_APP_ALGOD_TOKEN = aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
REACT_APP_INDEXER_SERVER = https://testnet-idx.algonode.cloud
REACT_APP_APP_ID = 755789606
REACT_APP_APP_ADDRESS = PJB7TQATUORZIFL3ZN3N4RW5NXZQV2WCQ4MG2U7ZS7BPMHM6DII7Q6NRPI
REACT_APP_PINATA_KEY = your_pinata_key_here
REACT_APP_PINATA_SECRET = your_pinata_secret_here
```

3. Make sure to set them for "Production", "Preview", and "Development" environments

### 3. Configure Build Settings (if needed)

The project is already configured with:
- **Framework Preset:** Create React App
- **Build Command:** `npm run build` (auto-detected by Vercel)
- **Output Directory:** `build` (auto-detected)

### 4. Deploy

1. Click the "Deploy" button to trigger the first deployment
2. Vercel will automatically build and deploy your project
3. Once complete, you'll receive a live URL (e.g., `https://certichain.vercel.app`)

## Local Development with Vercel

To test locally before deploying:

```bash
# Install Vercel CLI
npm install -g vercel

# Login to Vercel
vercel login

# Run development server
npm run dev

# Test build locally
npm run build
```

## Automatic Deployments

The project is configured for automatic deployments:
- **Production:** Deploys when you push to the `main` branch
- **Preview:** Deploys for every pull request

## Environment Variables in Vercel

To avoid hardcoding sensitive data:

1. Create environment variables in Vercel Dashboard
2. They will be automatically injected at build time
3. All `REACT_APP_*` variables are exposed to the frontend

## Troubleshooting

### Build Fails
- Check that all dependencies are installed: `npm install`
- Verify `package.json` has correct scripts
- Check build logs in Vercel dashboard

### Environment Variables Not Working
- Ensure variables are prefixed with `REACT_APP_`
- Rebuild after adding/changing variables
- Check variable scope (Production/Preview/Development)

### CORS Issues
- Verify Algorand API URLs are correct
- Check Pinata configuration
- Add API endpoints to allowed domains if needed

## Additional Resources

- [Vercel Documentation](https://vercel.com/docs)
- [Create React App on Vercel](https://vercel.com/guides/deploying-react-with-vercel)
- [Environment Variables in Vercel](https://vercel.com/docs/projects/environment-variables)
