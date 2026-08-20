# 🏸 Badminton Court Management System - Backend API

![Node.js](https://img.shields.io/badge/Node.js-v18+-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-5.x-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![MySQL](https://img.shields.io/badge/MySQL-8.0-%2300758F.svg?style=for-the-badge&logo=mysql&logoColor=white)
![Socket.io](https://img.shields.io/badge/Socket.io-Realtime-black?style=for-the-badge&logo=socket.io&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger-OpenAPI%203.0-%2385EA2D?style=for-the-badge&logo=swagger&logoColor=black)
![JWT](https://img.shields.io/badge/JWT-Secure%20Auth-black?style=for-the-badge&logo=jsonwebtokens&logoColor=white)

A high-performance Node.js/Express REST API and WebSocket server powering the Badminton Court Management System (BCMS). Engineered with MySQL relational storage, concurrency-safe double-booking prevention, automated background cron jobs, and real-time status synchronization.

---

## 🌐 Live API & Interactive Documentation

- **Base API URL**: [https://badminton-court-management-be.onrender.com/api/v1](https://badminton-court-management-be.onrender.com/api/v1)
- **Interactive Swagger UI Docs**: [https://badminton-court-management-be.onrender.com/api-docs](https://badminton-court-management-be.onrender.com/api-docs)
- **Frontend Web Application**: [https://badminton-court-management.vercel.app](https://badminton-court-management.vercel.app)
- **System Architecture & ERD**: [Notion Workspace](https://app.notion.com/p/Badminton-Court-Management-System-3849f49bca6d8032a1b6d16c2a71ce08?source=copy_link)

### 🔐 Demo Credentials (For Testing & Recruitment)

| Role | Phone Number / Account | Password |
| :--- | :--- | :--- |
| **Admin** | `0388874855` | `123456` |
| **Customer** | Register freely via `/auth/register` or the web portal | Custom |

---

## 🚀 Key Features & Architectural Highlights

- **Concurrency-Safe Double-Booking Prevention**: Specialized MySQL overlap queries that validate time slots (`start_time` < `new_end_time` AND `end_time` > `new_start_time`), preventing race condition double-bookings across concurrent requests.
- **Real-Time WebSocket Integration**: Integrated `socket.io` broadcasting that immediately pushes court schedule updates, payment confirmations, and cancellations to all active clients.
- **Automated Background Cron Jobs**: Background worker that continuously inspects pending reservations and automatically releases slots if left unpaid after 15 minutes.
- **Role-Based Access Control (RBAC)**: Fine-grained middleware authorization separating `admin`, `staff`, and `customer` permissions.
- **Transactional Consistency**: Relational database architecture ensuring foreign key integrity between users, courts, bookings, and payment records.

---

## 🛠 Tech Stack & Dependencies

- **Core Runtime**: Node.js (CommonJS)
- **Framework**: Express.js (v5)
- **Database**: MySQL 8.0 with `mysql2/promise` connection pooling
- **Real-Time Communication**: `socket.io` (v4)
- **Authentication**: `jsonwebtoken`, `bcryptjs`
- **Validation**: `express-validator`
- **Background Jobs**: Node native intervals & cron workers
- **API Documentation**: `swagger-jsdoc`, `swagger-ui-express`
- **Security & Utilities**: `cors`, `morgan`, `dotenv`

---

## 🗄️ Database Schema & Data Models

- **`users`**: Customer and employee profiles, hashed credentials, contact phone numbers, and permission roles.
- **`courts`**: Court identifiers, display names, active/maintenance statuses, and hourly pricing (`price_per_hour`).
- **`bookings`**: Booking records, customer associations, target court IDs, start/end timestamps, total costs, and lifecycle statuses (`pending`, `confirmed`, `completed`, `cancelled`).
- **`payments`**: Payment transaction logs, transaction codes, payment methods (VietQR, Cash), and audit trails.

---

## 💻 Local Installation & Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/nhatthaiuit/Badminton_Court_Management_BE.git
   cd Badminton_Court_Management_BE
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure Environment Variables**:
   Create a `.env` file from the example:
   ```bash
   cp .env.example .env
   ```
   Fill in your local configuration:
   ```env
   PORT=5001
   NODE_ENV=development
   DB_HOST=localhost
   DB_PORT=3306
   DB_USER=root
   DB_PASSWORD=your_mysql_password
   DB_NAME=bcms_db
   JWT_SECRET=your_super_secret_jwt_key
   JWT_EXPIRES_IN=7d
   CORS_ORIGIN=http://localhost:5173
   ```

4. **Initialize Database Schema**:
   Run the SQL migrations located in `/migrations` against your MySQL database:
   ```bash
   mysql -u root -p bcms_db < migrations/init.sql
   ```

5. **Start Development Server**:
   ```bash
   npm run dev
   ```
   API runs at `http://localhost:5001/api/v1` and Swagger documentation at `http://localhost:5001/api-docs`.

---

## 📁 Project Structure

```
Badminton_Court_Management_BE/
├── migrations/          # SQL initialization and schema migration scripts
├── src/
│   ├── config/          # Database connection pool & environment setup
│   ├── controllers/     # Request controllers (Auth, Bookings, Courts, Admin)
│   ├── middlewares/     # JWT authentication & role authorization middlewares
│   ├── routes/          # Express route definitions
│   ├── utils/           # Cron workers, date formatters, and helpers
│   └── swagger/         # OpenAPI/Swagger documentation configuration
├── server.js            # HTTP & WebSocket server bootstrap
├── .env.example         # Template environment variables
└── package.json
```

---

## 📄 License & Author

Developed by **Nhat Thai** for academic and recruitment portfolio showcase.  
Licensed under the [ISC License](LICENSE).
