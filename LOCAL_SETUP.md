# Local Development Setup

## Prerequisites
- Node.js 18+
- npm
- Supabase account

## Quick Setup

1. **Run setup script:**
   ```bash
   setup.bat
   ```

2. **Configure environment variables:**
   
   **Backend (.env in /api directory):**
   ```env
   SUPABASE_URL=your_supabase_url
   SUPABASE_ANON_KEY=your_supabase_anon_key
   JWT_SECRET=your_jwt_secret
   PORT=5000
   ```

   **Frontend (.env in /apps/frontend directory):**
   ```env
   VITE_API_URL=http://localhost:5000/api
   VITE_SUPABASE_URL=your_supabase_url
   VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
   ```

3. **Start development servers:**
   ```bash
   npm run dev
   ```

## Available Scripts

- `npm run dev` - Start both frontend and backend
- `npm run dev:frontend` - Frontend only (port 5173)
- `npm run dev:backend` - Backend only (port 5000)
- `npm run build` - Build for production

## Troubleshooting

- If ports are in use, kill processes or change ports in package.json
- Ensure Supabase credentials are correct
- Check that all dependencies are installed with `npm run install:all`