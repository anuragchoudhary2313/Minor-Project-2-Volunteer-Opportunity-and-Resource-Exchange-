# Before & After: Supabase to MongoDB Migration

## File Structure Changes

### ❌ Removed Files/Folders

```
supabase/                          # Complete Supabase setup folder
  └── migrations/
      └── 20250518165236_purple_coral.sql
src/lib/supabase.ts               # Supabase client configuration
src/types/supabase.ts             # Auto-generated Supabase types
```

### ✅ Added Files/Folders

```
server/                            # New Express backend
  ├── config/
  │   └── db.js                   # MongoDB connection
  ├── middleware/
  │   └── auth.js                 # JWT authentication
  ├── models/
  │   ├── User.js                 # User model
  │   ├── Opportunity.js          # Opportunity model
  │   ├── Resource.js             # Resource model
  │   ├── VolunteerSignup.js      # Signup model
  │   └── CommunityTip.js         # Tip model
  ├── routes/
  │   ├── auth.js                 # Auth endpoints
  │   ├── users.js                # User endpoints
  │   ├── opportunities.js        # Opportunity endpoints
  │   ├── resources.js            # Resource endpoints
  │   └── communityTips.js        # Tips endpoints
  ├── .env                        # Server environment vars
  ├── .env.example                # Server env template
  ├── package.json                # Server dependencies
  └── index.js                    # Server entry point

src/lib/api.ts                    # Axios API client (replaces supabase.ts)
.env                              # Frontend environment vars
.env.example                      # Frontend env template
README_MONGODB.md                 # MongoDB setup guide
MIGRATION_SUMMARY.md              # Detailed migration notes
QUICKSTART.md                     # Quick start guide
```

## Code Changes - Side by Side

### 1. Dependencies

#### Before (package.json)

```json
{
  "dependencies": {
    "@supabase/supabase-js": "^2.38.4",
    "lucide-react": "^0.344.0",
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-hot-toast": "^2.4.1",
    "react-router-dom": "^6.22.2"
  }
}
```

#### After (package.json)

```json
{
  "dependencies": {
    "axios": "^1.6.7", // Added for API calls
    "lucide-react": "^0.344.0",
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "react-hot-toast": "^2.4.1",
    "react-router-dom": "^6.22.2"
  }
}
```

### 2. Database Connection

#### Before (Supabase Client)

```typescript
// src/lib/supabase.ts
import { createClient } from "@supabase/supabase-js";
import { Database } from "../types/supabase";

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

export const supabase = createClient<Database>(supabaseUrl, supabaseAnonKey);
```

#### After (MongoDB Connection)

```javascript
// server/config/db.js
import mongoose from "mongoose";

const connectDB = async () => {
  try {
    const conn = await mongoose.connect(process.env.MONGODB_URI);
    console.log(`MongoDB Connected: ${conn.connection.host}`);
  } catch (error) {
    console.error(`Error: ${error.message}`);
    process.exit(1);
  }
};

export default connectDB;
```

### 3. Authentication

#### Before (Supabase Auth)

```typescript
// src/context/AuthContext.tsx
import { User } from "@supabase/supabase-js";
import { supabase } from "../lib/supabase";

const signUp = async (email: string, password: string, fullName: string) => {
  const { data, error } = await supabase.auth.signUp({
    email,
    password,
  });

  if (data.user) {
    await supabase.from("profiles").insert({
      id: data.user.id,
      full_name: fullName,
      // ... other fields
    });
  }
};

const signIn = async (email: string, password: string) => {
  const { error } = await supabase.auth.signInWithPassword({
    email,
    password,
  });
};
```

#### After (JWT Auth)

```typescript
// src/context/AuthContext.tsx
import api from "../lib/api";

const signUp = async (email: string, password: string, fullName: string) => {
  const { data } = await api.post("/auth/signup", {
    email,
    password,
    full_name: fullName,
  });

  localStorage.setItem("token", data.token);
  localStorage.setItem("user", JSON.stringify(data));
  setUser(data);
};

const signIn = async (email: string, password: string) => {
  const { data } = await api.post("/auth/signin", {
    email,
    password,
  });

  localStorage.setItem("token", data.token);
  localStorage.setItem("user", JSON.stringify(data));
  setUser(data);
};
```

### 4. Data Fetching

#### Before (Supabase Query)

```typescript
// Fetching opportunities
const { data, error } = await supabase
  .from("opportunities")
  .select("*")
  .order("date", { ascending: true });

if (error) throw error;
setOpportunities(data);
```

#### After (REST API)

```typescript
// Fetching opportunities
const { data } = await api.get("/opportunities");
setOpportunities(data);
```

### 5. Data Creation

#### Before (Supabase Insert)

```typescript
// Creating opportunity
const { error } = await supabase.from("opportunities").insert({
  ...newOpportunity,
  user_id: user.id,
});

if (error) throw error;
```

#### After (REST API)

```typescript
// Creating opportunity
await api.post("/opportunities", newOpportunity);
```

### 6. Data Update

#### Before (Supabase Update)

```typescript
// Updating profile
const { error } = await supabase
  .from("profiles")
  .update({
    full_name: formData.full_name,
    location: formData.location,
    skills,
    interests,
  })
  .eq("id", user.id);
```

#### After (REST API)

```typescript
// Updating profile
await api.put("/users", {
  full_name: formData.full_name,
  location: formData.location,
  skills,
  interests,
});
```

### 7. Data Models

#### Before (PostgreSQL Schema - Supabase)

```sql
-- From supabase/migrations/*.sql
create table profiles (
  id uuid references auth.users not null primary key,
  full_name text,
  location text,
  skills text[],
  interests text[],
  avatar_url text,
  created_at timestamp with time zone default timezone('utc'::text, now()),
  updated_at timestamp with time zone default timezone('utc'::text, now())
);
```

#### After (Mongoose Schema - MongoDB)

```javascript
// server/models/User.js
const userSchema = new mongoose.Schema(
  {
    email: {
      type: String,
      required: true,
      unique: true,
    },
    password: {
      type: String,
      required: true,
    },
    full_name: {
      type: String,
      required: true,
    },
    location: String,
    skills: [String],
    interests: [String],
    avatar_url: String,
  },
  {
    timestamps: true, // Automatically adds createdAt, updatedAt
  }
);
```

## Architectural Changes

### Before (Supabase Architecture)

```
┌─────────────┐
│   Browser   │
│  (React)    │
└──────┬──────┘
       │
       │ Supabase Client SDK
       │
┌──────▼────────────────┐
│   Supabase Cloud      │
│                       │
│  ┌─────────────────┐  │
│  │  PostgreSQL DB  │  │
│  └─────────────────┘  │
│  ┌─────────────────┐  │
│  │  Auth Service   │  │
│  └─────────────────┘  │
│  ┌─────────────────┐  │
│  │  Storage        │  │
│  └─────────────────┘  │
└───────────────────────┘
```

### After (MongoDB + Express Architecture)

```
┌─────────────┐
│   Browser   │
│  (React)    │
└──────┬──────┘
       │
       │ Axios HTTP Requests
       │
┌──────▼──────────┐
│  Express API    │
│  (Node.js)      │
│                 │
│  ┌───────────┐  │
│  │   Auth    │  │
│  │   (JWT)   │  │
│  └───────────┘  │
│  ┌───────────┐  │
│  │  Routes   │  │
│  └───────────┘  │
└─────┬───────────┘
      │
      │ Mongoose
      │
┌─────▼──────────┐
│    MongoDB     │
│   (Database)   │
└────────────────┘
```

## Feature Comparison

| Feature              | Supabase              | MongoDB + Express                             |
| -------------------- | --------------------- | --------------------------------------------- |
| **Setup Time**       | 5 minutes             | 15-20 minutes                                 |
| **Learning Curve**   | Low                   | Medium                                        |
| **Control**          | Limited               | Full                                          |
| **Customization**    | Limited               | Full                                          |
| **Cost (Free Tier)** | 500MB DB, 2GB Storage | Unlimited (self-hosted) or MongoDB Atlas Free |
| **Authentication**   | Built-in              | Custom (JWT)                                  |
| **Real-time**        | Yes (built-in)        | No (add Socket.io)                            |
| **File Storage**     | Yes (built-in)        | No (add S3/Cloudinary)                        |
| **Database**         | PostgreSQL (SQL)      | MongoDB (NoSQL)                               |
| **Type Safety**      | Auto-generated        | Manual                                        |
| **Vendor Lock-in**   | Yes                   | No                                            |
| **Scalability**      | Automatic             | Manual                                        |
| **Debugging**        | Cloud logs            | Direct access                                 |

## Benefits of Migration

### ✅ Advantages

1. **Full Control**: Complete ownership of backend logic
2. **Flexibility**: Easy to customize and extend
3. **Learning**: Better understanding of full-stack development
4. **No Vendor Lock-in**: Can switch providers anytime
5. **Cost**: Self-hosting can be cheaper at scale
6. **Debugging**: Easier to debug with direct backend access

### ⚠️ Trade-offs

1. **Maintenance**: More code to maintain
2. **Deployment**: Need to deploy and manage backend separately
3. **Real-time**: Need to implement separately (Socket.io)
4. **File Upload**: Need to add separate service
5. **Security**: More responsibility for security implementation

## Environment Variables

### Before

```env
VITE_SUPABASE_URL=https://xxxxx.supabase.co
VITE_SUPABASE_ANON_KEY=xxxxxxxxxxxxx
```

### After

```env
# Frontend (.env)
VITE_API_URL=http://localhost:5000/api

# Backend (server/.env)
MONGODB_URI=mongodb://localhost:27017/helphub
JWT_SECRET=your_secret_key_here
PORT=5000
```

## Deployment

### Before (Supabase)

- **Frontend**: Any static host (Vercel, Netlify)
- **Backend**: Managed by Supabase
- **Database**: Hosted by Supabase

### After (MongoDB)

- **Frontend**: Any static host (Vercel, Netlify)
- **Backend**: Node.js host (Heroku, Railway, DigitalOcean, Vercel Functions)
- **Database**: MongoDB Atlas (managed) or self-hosted

## Summary

The migration from Supabase to MongoDB with Express gives you:

- Complete control over your backend
- Better understanding of full-stack architecture
- No dependency on third-party services
- Flexibility to extend and customize
- Direct database access for debugging

While requiring more setup and maintenance, this architecture provides a solid foundation for a production application with full customization capabilities.
