# LMS Monorepo

A full-stack Learning Management System built with React, Express.js, and Supabase, deployed on Vercel.

## Project Structure

```
LMS/
├── api/                    # Backend API (Express.js + Supabase)
│   ├── src/
│   │   ├── config/        # Database and service configurations
│   │   ├── controllers/   # API route handlers
│   │   ├── middleware/    # Authentication and validation
│   │   ├── models/        # Database models
│   │   ├── routes/        # API routes
│   │   ├── services/      # Business logic services
│   │   └── utils/         # Utility functions
│   ├── index.js          # Vercel serverless entry point
│   └── package.json
├── apps/
│   └── frontend/         # React frontend (Vite + TypeScript)
│       ├── src/
│       │   ├── api/      # API client configuration
│       │   ├── components/ # React components
│       │   ├── pages/    # Application pages
│       │   ├── context/  # React context providers
│       │   └── layouts/  # Page layouts
│       └── package.json
├── vercel.json           # Vercel deployment configuration
└── package.json          # Root package.json for monorepo
```

## Features

- **Multi-role Authentication**: Admin, Teacher, Student, Parent roles
- **Exam Management**: Create, assign, and manage exams
- **Question Bank**: Comprehensive question management system
- **Real-time Results**: Instant exam results and analytics
- **User Management**: Complete user lifecycle management
- **Responsive Design**: Mobile-first UI with Tailwind CSS
- **Modern Stack**: React 18, TypeScript, Express.js, Supabase

## Tech Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for build tooling
- **Tailwind CSS** for styling
- **Shadcn/ui** for UI components
- **React Router** for navigation
- **Axios** for API calls
- **React Hook Form** for form handling

### Backend
- **Express.js** with ES modules
- **Supabase** for database and authentication
- **JWT** for session management
- **Multer** for file uploads
- **CORS** for cross-origin requests

### Deployment
- **Vercel** for hosting (both frontend and serverless API)
- **Supabase** for database hosting

## Getting Started

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Supabase account

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd LMS
```

2. Install dependencies for all packages:
```bash
npm run install:all
```

3. Set up environment variables:

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
```

4. Start development servers:

```bash
# Start both frontend and backend
npm run dev

# Or start individually
npm run dev:frontend  # Frontend only
npm run dev:backend   # Backend only
```

### Building for Production

```bash
npm run build
```

## Deployment on Vercel

1. Connect your repository to Vercel
2. Set the following build settings:
   - **Build Command**: `npm run build`
   - **Output Directory**: `apps/frontend/dist`
   - **Install Command**: `npm run install:all`

3. Add environment variables in Vercel dashboard:
   - `SUPABASE_URL`
   - `SUPABASE_ANON_KEY` 
   - `JWT_SECRET`

4. Deploy! Vercel will automatically handle:
   - Frontend static files serving
   - API routes as serverless functions
   - Automatic deployments on git push

## API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout

### User Management
- `GET /api/admin/users` - Get all users (Admin only)
- `POST /api/admin/users` - Create user (Admin only)
- `PUT /api/admin/users/:id` - Update user (Admin only)
- `DELETE /api/admin/users/:id` - Delete user (Admin only)

### Profile Management
- `GET /api/profile` - Get user profile
- `PUT /api/profile` - Update user profile
- `POST /api/profile/change-password` - Change password

### Exam Management
- `GET /api/student/exams` - Get available exams
- `POST /api/student/exams/:id/submit` - Submit exam
- `GET /api/teacher/exams` - Get teacher's exams
- `POST /api/teacher/exams` - Create new exam

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit changes: `git commit -am 'Add feature'`
4. Push to branch: `git push origin feature-name`
5. Submit a pull request

## License

This project is licensed under the MIT License.