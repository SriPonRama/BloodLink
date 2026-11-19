# 🩸 BloodLink — Blood Donation Management System

[![License: MIT](https://img.shields.io/badge/License-MIT-red.svg)](LICENSE)
[![React](https://img.shields.io/badge/React-18-blue.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-5-646CFF.svg)](https://vitejs.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-4.x-lightgrey.svg)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248.svg)](https://www.mongodb.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC.svg)](https://tailwindcss.com/)

A full-stack, healthcare-grade blood donation management platform that connects blood donors, hospitals, and blood banks in real time for life-saving emergency transfusions and scheduled donations.

---

## 📌 Table of Contents
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture](#-project-architecture)
- [Quick Start Guide](#-quick-start-guide)
  - [Prerequisites](#prerequisites)
  - [One-Command Setup](#one-command-setup-recommended)
  - [Manual Setup](#manual-setup)
- [Environment Variables](#-environment-variables)
- [API Documentation](#-api-documentation)
- [Blood Compatibility Matrix](#-blood-compatibility-matrix)
- [User Roles & Workflows](#-user-roles--workflows)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🩸 Features

### 🏥 Core Functionality
- **Multi-Role Authentication & Authorization**: Dedicated role workflows for **Donors**, **Hospitals**, and **Blood Banks**.
- **Real-Time Blood Requests**: Create, view, and fulfill emergency and normal blood requests.
- **Smart Compatibility Matching**: Automated matching engine based on standard ABO/Rh medical blood compatibility.
- **Emergency Alert Ticker**: Live real-time scrolling ticker showcasing critical emergency requirements.
- **Donor Response & Management**: Hospitals and blood banks can review and manage donor responses (accept/deny).
- **Profile & History Tracking**: User profile customization, donation eligibility tracking, and past donation history.

### 💻 User Experience & UI
- **Modern Healthcare Aesthetic**: Responsive, accessible, and clean UI built with Tailwind CSS.
- **Interactive Role-Based Dashboards**: Tailored views depending on whether the logged-in user is a donor, hospital, or blood bank.
- **Real-Time Feedback**: Interactive notifications via React Hot Toast.
- **Search & Filters**: Filter requests by blood group, urgency level, city, and status.

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: [React 18](https://react.dev/) with [Vite](https://vitejs.dev/)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/)
- **Icons & Animation**: [React Icons](https://react-icons.github.io/react-icons/) & [Framer Motion](https://www.framer.com/motion/)
- **State & Routing**: React Context API (`AuthContext`) & [React Router v6](https://reactrouter.com/)
- **HTTP Client**: [Axios](https://axios-http.com/)
- **Toasts**: [React Hot Toast](https://react-hot-toast.com/)

### Backend
- **Runtime**: [Node.js](https://nodejs.org/) (v16+)
- **Server Framework**: [Express.js](https://expressjs.com/)
- **Database**: [MongoDB](https://www.mongodb.com/) with [Mongoose ODM](https://mongoosejs.com/)
- **Authentication**: JSON Web Tokens ([JWT](https://jwt.io/)) with [bcryptjs](https://github.com/dcodeIO/bcrypt.js)
- **Validation**: [express-validator](https://express-validator.github.io/docs/)
- **Process Orchestration**: [concurrently](https://github.com/open-cli-tools/concurrently) for simultaneous development

---

## 📁 Project Architecture

```
BloodLink/
├── .gitignore                   # Root gitignore (protects secrets & node_modules)
├── deploy.md                    # Deployment guide for Render & Railway
├── package.json                 # Root script runner (concurrently)
├── README.md                    # Project documentation
│
├── client/                      # React Frontend (Vite)
│   ├── .env.example             # Client environment template
│   ├── index.html               # Single page application entry HTML
│   ├── package.json             # Frontend dependencies
│   ├── vite.config.js           # Vite dev server configuration & API proxy
│   ├── tailwind.config.js       # Tailwind CSS configuration
│   └── src/
│       ├── components/          # Reusable UI components (Navbar, Hero, Features, etc.)
│       ├── context/             # AuthContext & global state
│       ├── pages/               # Application views (Home, Dashboard, Emergency, etc.)
│       ├── services/            # Axios API client setup (api.js)
│       └── styles/              # Global styles (index.css)
│
└── server/                      # Express Backend API
    ├── .env.example             # Server environment template
    ├── package.json             # Backend dependencies
    └── src/
        ├── config/              # MongoDB connection setup
        ├── controllers/         # Request handling & business logic
        ├── middleware/          # JWT authentication & role-based route guards
        ├── models/              # Mongoose schemas (User, Profile, BloodRequest, Donation)
        ├── routes/              # Express API route definitions
        └── server.js            # Server entry point
```

---

## 🚀 Quick Start Guide

### Prerequisites
- [Node.js](https://nodejs.org/) (v16.x or higher)
- [MongoDB](https://www.mongodb.com/) (Local instance or MongoDB Atlas connection string)
- [Git](https://git-scm.com/)

---

### One-Command Setup (Recommended)

1. **Clone the repository**:
   ```bash
   git clone https://github.com/SriPonRama/BloodLink.git
   cd BloodLink
   ```

2. **Configure environment variables**:
   * Copy `client/.env.example` to `client/.env`
   * Copy `server/.env.example` to `server/.env` and insert your MongoDB URI and a JWT secret.

3. **Install all dependencies** (client & server):
   ```bash
   npm run install-all
   ```

4. **Start both client and server concurrently**:
   ```bash
   npm run dev
   ```

* **Frontend:** [http://localhost:3000](http://localhost:3000)
* **Backend API:** [http://localhost:5000](http://localhost:5000)

---

### Manual Setup

<details>
<summary>Click to view step-by-step setup for client & server</summary>

#### 1. Setup Backend
```bash
cd server
npm install
cp .env.example .env
# Edit .env with your MONGODB_URI and JWT_SECRET
npm run dev
```

#### 2. Setup Frontend
```bash
cd ../client
npm install
cp .env.example .env
# Default VITE_API_URL=http://localhost:5000/api
npm run dev
```
</details>

---

## ⚙️ Environment Variables

### Backend (`server/.env`)
| Variable | Description | Default / Example |
| :--- | :--- | :--- |
| `PORT` | Backend server port | `5000` / `5001` |
| `MONGODB_URI` | MongoDB connection string | `mongodb://localhost:27017/bloodlink` |
| `JWT_SECRET` | Secret string for signing auth tokens | `your_secure_jwt_secret` |
| `NODE_ENV` | Environment mode | `development` / `production` |
| `CLOUDINARY_*` | *(Optional)* Image upload credentials | `your_cloud_name`, etc. |

### Frontend (`client/.env`)
| Variable | Description | Default / Example |
| :--- | :--- | :--- |
| `VITE_API_URL` | Base endpoint for the backend API | `http://localhost:5000/api` |

---

## 📡 API Documentation

### Health Check
- `GET /api/health` — Returns server health status.

### Authentication & User (`/api/auth`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Public | Register a new user (`donor`, `hospital`, `bloodbank`) |
| `POST` | `/api/auth/login` | Public | Authenticate user and receive JWT token |
| `GET` | `/api/auth/me` | Authenticated | Retrieve current user profile and session details |
| `PUT` | `/api/auth/profile` | Authenticated | Update user information and medical profile |
| `GET` | `/api/auth/donors` | Hospital / Blood Bank | List all available registered donors |

### Blood Requests (`/api/blood-requests`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/blood-requests` | Public | Retrieve blood requests (supports query filters) |
| `GET` | `/api/blood-requests/emergency` | Public | Retrieve urgent/emergency priority blood requests |
| `POST` | `/api/blood-requests` | Hospital / Blood Bank | Post a new blood request |
| `GET` | `/api/blood-requests/my-requests` | Authenticated | Get all requests created by the current user |
| `POST` | `/api/blood-requests/:id/respond` | Donor | Respond to a specific blood request |
| `POST` | `/api/blood-requests/:id/donor/:donorId/manage` | Hospital / Blood Bank | Accept or reject donor response |
| `PATCH`| `/api/blood-requests/:id/status` | Hospital / Blood Bank | Update request status (`open`, `fulfilled`, `cancelled`) |

---

## 🩸 Blood Compatibility Matrix

BloodLink enforces medical compatibility rules:

| Blood Type | Can Receive From | Can Donate To |
| :---: | :--- | :--- |
| **O-** | O- *(Universal Red Blood Cell Donor)* | All Blood Types (O-, O+, A-, A+, B-, B+, AB-, AB+) |
| **O+** | O-, O+ | O+, A+, B+, AB+ |
| **A-** | O-, A- | A-, A+, AB-, AB+ |
| **A+** | O-, O+, A-, A+ | A+, AB+ |
| **B-** | O-, B- | B-, B+, AB-, AB+ |
| **B+** | O-, O+, B-, B+ | B+, AB+ |
| **AB-** | O-, A-, B-, AB- | AB-, AB+ |
| **AB+** | All Blood Types *(Universal Recipient)* | AB+ only |

---

## 👥 User Roles & Workflows

1. **Donors**:
   - Register and specify blood type, contact details, and location.
   - Browse emergency and nearby blood requests.
   - Respond to requests with a single click.
   - Track donation history and eligibility.

2. **Hospitals**:
   - Create urgent or routine blood requests specifying units required, patient condition, and hospital address.
   - Review incoming responses from eligible donors.
   - Coordinate with donors and track fulfillment.

3. **Blood Banks**:
   - Maintain regional blood bank directory and post inventory requests.
   - Manage donor outreach and respond to critical community shortages.

---

## 🌐 Deployment

For step-by-step instructions on deploying BloodLink to cloud providers (e.g., Render, Railway, Vercel, Netlify), see [deploy.md](deploy.md).

### Quick Deployment Summary:
1. **Database**: Create a production cluster on [MongoDB Atlas](https://www.mongodb.com/atlas). Whitelist your server IP (or `0.0.0.0/0`).
2. **Backend**: Deploy the `server/` directory to **Render** or **Railway**. Set `MONGODB_URI`, `JWT_SECRET`, `NODE_ENV=production`, and `PORT`.
3. **Frontend**: Deploy the `client/` directory to **Vercel** or **Netlify**. Set `VITE_API_URL` to your production backend URL.

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:
1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/NewFeature`)
3. Commit your Changes (`git commit -m "Add NewFeature"`)
4. Push to the Branch (`git push origin feature/NewFeature`)
5. Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

**BloodLink** — *Connecting donors, saving lives, one drop at a time.* 🩸❤️
