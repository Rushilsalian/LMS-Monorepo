# Deployment Guide

This guide will help you deploy the LMS monorepo to Vercel.

## Prerequisites

1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com)
2. **Supabase Project**: Set up a Supabase project at [supabase.com](https://supabase.com)
3. **Git Repository**: Push your code to GitHub, GitLab, or Bitbucket

## Step 1: Prepare Your Environment Variables

### Supabase Setup
1. Go to your Supabase project dashboard
2. Navigate to Settings > API
3. Copy the following values:
   - Project URL
   - Anon/Public key

### Environment Variables Needed
```env
SUPABASE_URL=your_supabase_project_url
SUPABASE_ANON_KEY=your_supabase_anon_key
JWT_SECRET=your_random_jwt_secret_string
```

## Step 2: Deploy to Vercel

### Option A: Deploy via Vercel Dashboard

1. **Connect Repository**:
   - Go to [vercel.com/dashboard](https://vercel.com/dashboard)
   - Click "New Project"
   - Import your Git repository

2. **Configure Build Settings**:
   - **Framework Preset**: Other
   - **Root Directory**: Leave empty (monorepo root)
   - **Build Command**: `cd apps/frontend && npm run build`
   - **Output Directory**: `apps/frontend/dist`
   - **Install Command**: `npm install && cd apps/frontend && npm install && cd ../../api && npm install`

3. **Add Environment Variables**:
   - Go to Project Settings > Environment Variables
   - Add the following variables:
     ```
     SUPABASE_URL=your_supabase_project_url
     SUPABASE_ANON_KEY=your_supabase_anon_key
     JWT_SECRET=your_random_jwt_secret_string
     ```

4. **Deploy**:
   - Click "Deploy"
   - Wait for the build to complete

### Option B: Deploy via Vercel CLI

1. **Install Vercel CLI**:
   ```bash
   npm i -g vercel
   ```

2. **Login to Vercel**:
   ```bash
   vercel login
   ```

3. **Deploy from project root**:
   ```bash
   vercel
   ```

4. **Follow the prompts**:
   - Link to existing project or create new one
   - Confirm settings
   - Add environment variables when prompted

## Step 3: Configure Domain (Optional)

1. Go to your project dashboard on Vercel
2. Navigate to Settings > Domains
3. Add your custom domain
4. Follow DNS configuration instructions

## Step 4: Set Up Database Schema

1. **Run SQL Schema**:
   - Go to your Supabase project
   - Navigate to SQL Editor
   - Run the contents of `api/supabase-schema.sql`

2. **Configure Row Level Security (RLS)**:
   - Enable RLS on all tables
   - Set up appropriate policies for your use case

## Step 5: Test Your Deployment

1. **Frontend Test**:
   - Visit your Vercel domain
   - Verify the React app loads correctly
   - Check that routing works

2. **API Test**:
   - Visit `your-domain.vercel.app/api/health`
   - Should return: `{\"message\": \"Server is running!\", \"timestamp\": \"...\"}`

3. **Full Integration Test**:
   - Try registering a new user
   - Test login functionality
   - Verify database operations work

## Troubleshooting

### Common Issues

1. **Build Fails**:
   - Check that all dependencies are properly installed
   - Verify build command is correct
   - Check for TypeScript errors

2. **API Routes Not Working**:
   - Verify `api/index.js` exists and exports the Express app
   - Check environment variables are set correctly
   - Review Vercel function logs

3. **Database Connection Issues**:
   - Verify Supabase URL and key are correct
   - Check that database schema is properly set up
   - Ensure RLS policies allow your operations

4. **CORS Issues**:
   - Verify CORS configuration in `api/index.js`
   - Check that frontend domain is allowed

### Vercel Logs

To view deployment and function logs:
```bash
vercel logs your-project-name
```

Or view them in the Vercel dashboard under Functions tab.

## Environment-Specific Configuration

### Development
- Frontend: `http://localhost:3000`
- API: `http://localhost:5000`

### Production
- Frontend: `https://your-domain.vercel.app`
- API: `https://your-domain.vercel.app/api`

## Automatic Deployments

Vercel automatically deploys:
- **Production**: When you push to `main` branch
- **Preview**: When you create pull requests

## Performance Optimization

1. **Frontend**:
   - Vite automatically optimizes the build
   - Static assets are served via Vercel's CDN

2. **API**:
   - Serverless functions auto-scale
   - Cold start optimization via Vercel

3. **Database**:
   - Supabase provides connection pooling
   - Consider adding database indexes for better performance

## Security Considerations

1. **Environment Variables**:
   - Never commit secrets to Git
   - Use Vercel's environment variable system

2. **API Security**:
   - JWT tokens for authentication
   - CORS properly configured
   - Input validation on all endpoints

3. **Database Security**:
   - Row Level Security enabled
   - Proper access policies
   - Regular security updates

## Monitoring

1. **Vercel Analytics**:
   - Enable in project settings
   - Monitor performance and usage

2. **Error Tracking**:
   - Consider integrating Sentry or similar
   - Monitor API function errors

3. **Database Monitoring**:
   - Use Supabase dashboard for query performance
   - Monitor connection usage

## Scaling

As your application grows:

1. **Database**: Supabase handles scaling automatically
2. **API**: Vercel serverless functions scale automatically
3. **Frontend**: Served via global CDN

For high-traffic applications, consider:
- Database read replicas
- Caching strategies
- API rate limiting