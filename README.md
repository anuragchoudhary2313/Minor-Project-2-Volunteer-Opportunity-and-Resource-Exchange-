# 🤝 Help Hub

### Volunteer Opportunity and Resource Exchange Platform

[![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Node.js](https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com/)

_Connecting volunteers with opportunities and facilitating resource exchange in communities_

[Demo](#) · [Report Bug](../../issues) · [Request Feature](../../issues)

---

## 📋 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

---

## 🌟 About the Project

**Help Hub** is a comprehensive platform designed to bridge the gap between volunteers and organizations seeking assistance. It facilitates seamless resource exchange within communities, making it easier for people to help each other and make a positive impact.

### Why Help Hub?

- 🎯 **Streamlined Matching**: Connect volunteers with opportunities that match their skills and interests
- 🔄 **Resource Exchange**: Enable communities to share resources efficiently
- 📱 **Modern Interface**: Intuitive, responsive design for seamless user experience
- 🔐 **Secure**: Built with authentication and data security in mind
- 🔐 **Secure**: JWT authentication with hashed passwords
- 🚀 **Deployed**: Vercel-ready frontend + API backend

---

## ✨ Features

- 🔍 **Opportunity Discovery**: Browse and search volunteer opportunities by category, location, and time commitment
- 👤 **User Profiles**: Create detailed profiles showcasing skills, interests, and availability
- 📝 **Opportunity Posting**: Organizations can post volunteer opportunities with detailed descriptions
- 💬 **Resource Exchange**: Post and request resources within the community
- 🔔 **Notifications**: Stay updated with real-time notifications
- 📊 **Dashboard**: Track volunteer hours, completed opportunities, and impact metrics
- 🌐 **Responsive Design**: Fully functional across desktop, tablet, and mobile devices
- 🔐 **Authentication**: Secure JWT-based auth

---

## 🛠 Tech Stack

| Technology                | Purpose                             |
| ------------------------- | ----------------------------------- |
| **React 18 + TypeScript** | Frontend UI                         |
| **Vite**                  | Fast dev/build tooling              |
| **Tailwind CSS**          | Styling                             |
| **React Router**          | Client-side routing                 |
| **React Hot Toast**       | Notifications                       |
| **Axios**                 | API client                          |
| **Node.js + Express**     | Backend API                         |
| **MongoDB + Mongoose**    | Database and ODM                    |
| **JWT + bcrypt**          | Authentication & password hashing   |
| **Vercel**                | Hosting (frontend & serverless API) |

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher) - [Download](https://nodejs.org/)
- **npm** or **yarn** package manager
- **MongoDB** (local) or **MongoDB Atlas** account

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/anuragchoudhary2313/Minor-Project-2-Volunteer-Opportunity-and-Resource-Exchange-.git
   cd Minor-Project-2-Volunteer-Opportunity-and-Resource-Exchange-
   ```

2. **Install dependencies**

   ```bash
   npm install
   # or
   yarn install
   ```

3. **Configure environment variables**

   **Frontend (.env):**

   ```env
   VITE_API_URL=http://localhost:5000/api
   ```

   **Backend (server/.env):**

   ```env
   MONGODB_URI=your_mongodb_connection_string
   JWT_SECRET=your_secret_key
   PORT=5000
   ```

4. **Install backend dependencies**

   ```bash
   cd server
   npm install
   ```

5. **Start backend (port 5000)**

   ```bash
   npm run dev
   ```

6. **Start frontend (port 5173)**

   ```bash
   cd ..
   npm install
   npm run dev
   ```

7. **Open your browser** at `http://localhost:5173`

### Environment Variables

| Variable       | Description                                        |
| -------------- | -------------------------------------------------- |
| `VITE_API_URL` | Base URL for API (e.g., http://localhost:5000/api) |
| `MONGODB_URI`  | MongoDB/Atlas connection string (server/.env)      |
| `JWT_SECRET`   | Secret for signing JWTs (server/.env)              |
| `PORT`         | Backend port (default 5000, server/.env)           |

---

## 💻 Usage

### For Volunteers

1. **Create an account** and complete your profile
2. **Browse opportunities** that match your interests
3. **Apply** to opportunities you're interested in
4. **Track** your volunteer hours and impact

### For Organizations

1. **Register** your organization
2. **Post opportunities** with detailed descriptions
3. **Manage applications** from interested volunteers
4. **Track** volunteer engagement and contributions

### Resource Exchange

1. **Post resources** you want to share or donate
2. **Browse available resources** in your community
3. **Request resources** you need
4. **Coordinate exchanges** with other users

---

## 📁 Project Structure

```
Minor-Project-2-Volunteer-Opportunity-and-Resource-Exchange-/
├── src/
│   ├── components/       # Reusable React components
│   ├── pages/           # Page components
│   ├── hooks/           # Custom React hooks
│   ├── utils/           # Utility functions
│   ├── types/           # TypeScript type definitions
│   ├── styles/          # Global styles
│   └── App.tsx          # Main application component
├── public/              # Static assets
├── index.html           # HTML entry point
├── vite.config.ts       # Vite configuration
├── tailwind.config.js   # Tailwind CSS configuration
├── tsconfig.json        # TypeScript configuration
├── server/              # Express API (Node.js + MongoDB)
│   ├── models/          # Mongoose schemas
│   ├── routes/          # API routes
│   ├── middleware/      # Auth middleware
│   └── index.js         # Server entry
├── vercel.json          # Vercel deployment config
└── package.json         # Project dependencies
```

---

## 🤝 Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

## 📧 Contact

**Anurag Choudhary** - [@anuragchoudhary2313](https://github.com/anuragchoudhary2313)

**Project Link**: [https://github.com/anuragchoudhary2313/Minor-Project-2-Volunteer-Opportunity-and-Resource-Exchange-](https://github.com/anuragchoudhary2313/Minor-Project-2-Volunteer-Opportunity-and-Resource-Exchange-)

---

<div align="center">

### ⭐ Star this repository if you find it helpful!

Made with ❤️ by [Anurag Choudhary](https://github.com/anuragchoudhary2313)

</div>
