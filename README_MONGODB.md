# Help Hub - Volunteer Opportunity and Resource Exchange

A full-stack web application for connecting volunteers with opportunities and facilitating resource sharing within communities.

## Tech Stack

### Frontend

- React 18 with TypeScript
- Vite for build tooling
- TailwindCSS for styling
- React Router for navigation
- Axios for API calls
- React Hot Toast for notifications

### Backend

- Node.js with Express
- MongoDB with Mongoose ODM
- JWT for authentication
- bcryptjs for password hashing

## Prerequisites

- Node.js (v18 or higher)
- MongoDB (local installation or MongoDB Atlas account)
- npm or yarn

## Setup Instructions

### 1. MongoDB Setup

#### Option A: Local MongoDB

1. Install MongoDB from [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)
2. Start MongoDB service:
   ```bash
   mongod
   ```

#### Option B: MongoDB Atlas (Cloud)

1. Create a free account at [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new cluster
3. Get your connection string
4. Update the `MONGODB_URI` in `server/.env`

### 2. Backend Setup

```bash
# Navigate to server directory
cd server

# Install dependencies
npm install

# Create .env file from example
copy .env.example .env

# Edit .env file with your MongoDB URI and JWT secret
# MONGODB_URI=mongodb://localhost:27017/helphub
# JWT_SECRET=your_secret_key_here
# PORT=5000

# Start the server
npm run dev
```

The backend server will run on `http://localhost:5000`

### 3. Frontend Setup

```bash
# Navigate back to root directory
cd ..

# Install dependencies
npm install

# Create .env file from example
copy .env.example .env

# The .env should contain:
# VITE_API_URL=http://localhost:5000/api

# Start the development server
npm run dev
```

The frontend will run on `http://localhost:5173`

## Project Structure

```
.
├── src/                      # Frontend source code
│   ├── components/          # Reusable React components
│   ├── context/            # React context (Auth)
│   ├── lib/                # Utilities (API client)
│   ├── pages/              # Page components
│   ├── types/              # TypeScript type definitions
│   ├── App.tsx             # Main app component
│   └── main.tsx            # App entry point
│
├── server/                  # Backend source code
│   ├── config/             # Database configuration
│   ├── models/             # Mongoose models
│   ├── routes/             # API routes
│   ├── middleware/         # Auth middleware
│   └── index.js            # Server entry point
│
└── public/                 # Static assets
```

## API Endpoints

### Authentication

- `POST /api/auth/signup` - Register new user
- `POST /api/auth/signin` - Login user

### Users

- `GET /api/users` - Get current user profile (protected)
- `PUT /api/users` - Update user profile (protected)

### Opportunities

- `GET /api/opportunities` - Get all opportunities
- `POST /api/opportunities` - Create opportunity (protected)
- `GET /api/opportunities/signups` - Get user's signups (protected)
- `POST /api/opportunities/signup` - Sign up for opportunity (protected)
- `DELETE /api/opportunities/signup/:id` - Cancel signup (protected)

### Resources

- `GET /api/resources` - Get all resources
- `GET /api/resources/my-resources` - Get user's resources (protected)
- `POST /api/resources` - Create resource (protected)
- `DELETE /api/resources/:id` - Delete resource (protected)

### Community Tips

- `GET /api/community-tips` - Get all tips
- `POST /api/community-tips` - Create tip (protected)
- `PUT /api/community-tips/:id/like` - Like a tip (protected)

## Features

- **User Authentication**: Secure signup/login with JWT tokens
- **Volunteer Opportunities**: Browse and sign up for volunteer opportunities
- **Resource Exchange**: Offer or request resources within the community
- **User Profiles**: Manage personal information, skills, and interests
- **Community Tips**: Share and discover helpful tips
- **Dashboard**: Personalized view of signups and resources

## Migration from Supabase to MongoDB

This project was migrated from Supabase to MongoDB. Key changes include:

1. **Authentication**: Replaced Supabase Auth with JWT-based authentication
2. **Database**: Migrated from PostgreSQL (Supabase) to MongoDB
3. **API Layer**: Created Express REST API to replace Supabase client calls
4. **Data Models**: Converted Supabase tables to Mongoose schemas

## Development

### Running Tests

```bash
npm test
```

### Building for Production

```bash
# Build frontend
npm run build

# Build and start backend
cd server
npm start
```

## Environment Variables

### Frontend (.env)

```
VITE_API_URL=http://localhost:5000/api
```

### Backend (server/.env)

```
MONGODB_URI=mongodb://localhost:27017/helphub
JWT_SECRET=your_jwt_secret_key_change_this_in_production
PORT=5000
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License.

## Support

For support, email support@helphub.com or open an issue in the repository.
