# TaskFlow Backend API

A robust REST API and WebSocket server for the TaskFlow task management application, built with Node.js, Express, and MongoDB.

## 🚀 Live Deployment

**Backend API:** https://task3backend-vpcq.onrender.com

**Health Check:** https://task3backend-vpcq.onrender.com/api/health

---

## 📋 Features

- ✅ User authentication (JWT + cookies)
- ✅ Task management (CRUD operations)
- ✅ Real-time updates (WebSocket)
- ✅ User messaging system
- ✅ File uploads
- ✅ Reports and analytics
- ✅ Team collaboration features
- ✅ Rate limiting & security
- ✅ MongoDB Atlas integration
- ✅ CORS-enabled for frontend

---

## 🛠️ Tech Stack

- **Runtime:** Node.js (v20+)
- **Framework:** Express.js
- **Language:** TypeScript
- **Database:** MongoDB Atlas
- **Real-time:** Socket.IO
- **Security:** Helmet, JWT, bcryptjs
- **Other:** Multer (file uploads), express-rate-limit

---

## 📦 Project Structure

```
src/
├── server.ts                 # Main application entry point
├── config/
│   └── database.ts          # MongoDB connection config
├── middleware/
│   ├── auth.middleware.ts   # JWT authentication
│   ├── validation.middleware.ts
│   └── index.ts
├── models/
│   ├── User.ts              # User schema
│   ├── Task.ts              # Task schema
│   ├── Message.ts           # Message schema
│   └── index.ts
├── routes/
│   ├── auth.routes.ts       # Authentication endpoints
│   ├── user.routes.ts       # User endpoints
│   ├── task.routes.ts       # Task endpoints
│   ├── message.routes.ts    # Messaging endpoints
│   ├── report.routes.ts     # Reports endpoints
│   └── upload.routes.ts     # File upload endpoints
├── services/
│   ├── auth.service.ts      # Auth business logic
│   ├── user.service.ts
│   ├── task.service.ts
│   ├── message.service.ts
│   └── index.ts
├── socket/
│   └── index.ts             # WebSocket handlers
├── scripts/
│   └── seed.ts              # Database seeding script
└── uploads/                 # User uploads directory
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js v20 or higher
- npm or yarn
- MongoDB Atlas account (connection URI)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yaswanth65/task3Backend.git
   cd task3Backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Create `.env` file**
   ```env
   PORT=5000
   NODE_ENV=development
   
   MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/taskflow
   
   JWT_SECRET=your-secret-key-here
   JWT_EXPIRES_IN=7d
   
   FRONTEND_URL=http://localhost:3000
   
   MAX_FILE_SIZE=10485760
   UPLOAD_DIR=./uploads
   
   RATE_LIMIT_WINDOW_MS=900000
   RATE_LIMIT_MAX_REQUESTS=100
   ```

4. **Run development server**
   ```bash
   npm run dev
   ```

   Server runs on `http://localhost:5000`

### Available Scripts

```bash
npm run dev        # Start development server with hot reload
npm run build      # Compile TypeScript to JavaScript
npm start          # Run production build
npm run seed       # Seed database with sample data
```

---

## 📡 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/me` - Get current user

### Users
- `GET /api/users` - List all users
- `GET /api/users/:id` - Get user details
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user

### Tasks
- `GET /api/tasks` - List all tasks
- `GET /api/tasks/:id` - Get task details
- `POST /api/tasks` - Create task
- `PUT /api/tasks/:id` - Update task
- `DELETE /api/tasks/:id` - Delete task

### Messages
- `GET /api/messages` - List messages
- `POST /api/messages` - Send message
- `DELETE /api/messages/:id` - Delete message

### Reports
- `GET /api/reports` - Get reports/analytics

### Uploads
- `POST /api/upload` - Upload file

### Health Check
- `GET /api/health` - Server health status

---

## 🔐 Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `PORT` | No | `5000` | Server port |
| `NODE_ENV` | No | `development` | Environment mode |
| `MONGODB_URI` | Yes | - | MongoDB connection string |
| `JWT_SECRET` | Yes | - | Secret for JWT signing |
| `JWT_EXPIRES_IN` | No | `7d` | JWT expiration time |
| `FRONTEND_URL` | No | `localhost:3000` | Frontend origin(s) for CORS |
| `MAX_FILE_SIZE` | No | `10485760` | Max file upload size (bytes) |
| `UPLOAD_DIR` | No | `./uploads` | Upload directory path |
| `RATE_LIMIT_WINDOW_MS` | No | `900000` | Rate limit window (ms) |
| `RATE_LIMIT_MAX_REQUESTS` | No | `100` | Requests per window |

---

## 🔌 WebSocket Events

### Client → Server
- `connect` - Connection established
- `disconnect` - Connection closed
- `join_task` - Join task real-time updates
- `leave_task` - Leave task real-time updates
- `task_updated` - Task updated
- `message_sent` - New message sent

### Server → Client
- `task_updated` - Task change notification
- `message_received` - New message notification
- `user_joined` - User joined notification
- `error` - Error notification

---

## 📝 Test Account

Use these credentials to test (if database seeded):
- **Email:** `admin@example.com`
- **Password:** `password123`

Or register a new account through the app.

---

## 🐛 Troubleshooting

### MongoDB Connection Error
- Verify `MONGODB_URI` is correct
- Ensure MongoDB Atlas allows connections from your IP (Network Access → 0.0.0.0/0)

### CORS Errors
- Check `FRONTEND_URL` env variable matches frontend origin
- Include protocol: `https://` or `http://`
- No trailing slashes

### WebSocket Connection Issues
- Verify Socket.IO is properly configured
- Check browser console for connection errors
- Ensure frontend uses correct WebSocket URL

### File Upload Errors
- Check `UPLOAD_DIR` folder exists and is writable
- Verify file size is under `MAX_FILE_SIZE`
- Ensure `uploads/` directory has proper permissions

---

## 📚 API Documentation

### Register User
```bash
POST /api/auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123",
  "name": "John Doe"
}
```

### Login User
```bash
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password123"
}
```

### Create Task
```bash
POST /api/tasks
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Complete project",
  "description": "Finish the TaskFlow app",
  "dueDate": "2025-12-31",
  "priority": "high",
  "status": "pending"
}
```

---

## 🔗 Related Projects

- **Frontend:** https://github.com/yaswanth65/task3frontend
- **Live Frontend:** https://task3frontend.vercel.app

---

## 📄 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

**Yaswanth** - TaskFlow Developer

---

## 🤝 Support

For issues and questions, please create an issue in the repository or contact the development team.
