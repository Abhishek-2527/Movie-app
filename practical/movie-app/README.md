# 🎬 Movie Catalog Management System

A full-stack web application for managing a movie catalog with complete CRUD functionality. Built with Node.js, Express.js backend, MongoDB database, and vanilla HTML/CSS/JavaScript frontend.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Architecture](#project-architecture)
- [Installation & Setup](#installation--setup)
- [Environment Configuration](#environment-configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [Project Structure](#project-structure)
- [Usage Guide](#usage-guide)
- [Development Commands](#development-commands)
- [Troubleshooting](#troubleshooting)

---

## 📖 Overview

Movie Catalog Management System is a lab project demonstrating full-stack CRUD operations. It allows users to:
- View all movies in the catalog
- Add new movies with detailed information
- Update movie details (rating and duration)
- Delete movies from the catalog
- Browse movies with a clean, user-friendly interface

---

## ✨ Features

- **Complete CRUD Operations**: Create, Read, Update, Delete movie records
- **Real-time Data Display**: Movies are sorted by creation date (newest first)
- **Form Validation**: Server-side validation with detailed error messages
- **Responsive UI**: Clean, intuitive interface for easy movie management
- **RESTful API**: Well-structured REST API endpoints for movie operations
- **Error Handling**: Comprehensive error handling at both frontend and backend
- **MongoDB Integration**: Persistent data storage with Mongoose ODM
- **Environment Configuration**: Support for local and cloud MongoDB databases

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | HTML5, CSS3, Vanilla JavaScript (ES6+) |
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB, Mongoose ODM |
| **Runtime** | Node.js v26.0.0+ |
| **Package Manager** | npm |

---

## 🏗️ Project Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Frontend (Browser)                │
│        (HTML/CSS/JavaScript - /public)              │
└──────────────────┬──────────────────────────────────┘
                   │ HTTP/JSON
                   ▼
┌─────────────────────────────────────────────────────┐
│          Backend - Express.js Server                │
│         (routes/movies.js, server.js)               │
└──────────────────┬──────────────────────────────────┘
                   │ MongoDB Driver
                   ▼
┌─────────────────────────────────────────────────────┐
│     Database - MongoDB (Local or Atlas)             │
│     Movie Collection (models/Movie.js)              │
└─────────────────────────────────────────────────────┘
```

---

## 🚀 Installation & Setup

### Prerequisites

Ensure you have the following installed:
- **Node.js** v26.0.0 or higher
- **npm** v10.0.0 or higher
- **MongoDB** (local installation or MongoDB Atlas account)
- **Git** (for version control)

### Step 1: Clone or Extract the Repository

```bash
cd practical/movie-app
```

### Step 2: Install Dependencies

```bash
npm install
```

This will install all required packages:
- `express` - Web framework
- `mongoose` - MongoDB ODM
- `dotenv` - Environment variable management

### Step 3: Configure Environment Variables

Create a `.env` file in the root directory by copying from `.env.example`:

```bash
# Copy the example file
cp .env.example .env

# Edit the .env file with your settings
```

---

## 🔧 Environment Configuration

### Using Local MongoDB

```env
PORT=3000
MONGO_URI=mongodb://127.0.0.1:27017/movie_catalog
```

### Using MongoDB Atlas (Cloud)

```env
PORT=3000
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/movie_catalog?retryWrites=true&w=majority
```

Replace `<username>`, `<password>`, and `<cluster>` with your Atlas credentials.

### Starting MongoDB Locally (Windows)

If using local MongoDB:

```bash
# Start MongoDB service
net start MongoDB

# Or if using mongod directly
mongod
```

---

## ▶️ Running the Application

### Production Mode

```bash
npm start
```

Starts the server on the configured port (default: 3000).

### Development Mode (with Auto-reload)

```bash
npm run dev
```

Watches for file changes and automatically restarts the server using Node's `--watch` flag.

### Access the Application

Open your browser and navigate to:
```
http://localhost:3000
```

### Health Check

To verify the server is running:
```
curl http://localhost:3000/health
```

Expected response:
```json
{ "status": "ok" }
```

---

## 📡 API Documentation

### Base URL
```
http://localhost:3000/api/movies
```

### 1. Get All Movies

**Request:**
```
GET /api/movies
```

**Response (200 OK):**
```json
[
  {
    "_id": "507f1f77bcf86cd799439011",
    "title": "Inception",
    "director": "Christopher Nolan",
    "genre": "Science Fiction",
    "releaseYear": 2010,
    "rating": 8.8,
    "duration": 148,
    "language": "English",
    "createdAt": "2024-01-15T10:30:00.000Z"
  }
]
```

---

### 2. Create a New Movie

**Request:**
```
POST /api/movies
Content-Type: application/json

{
  "title": "Oppenheimer",
  "director": "Christopher Nolan",
  "genre": "Biography, Drama",
  "releaseYear": 2023,
  "rating": 8.5,
  "duration": 180,
  "language": "English"
}
```

**Response (201 Created):**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Oppenheimer",
  "director": "Christopher Nolan",
  "genre": "Biography, Drama",
  "releaseYear": 2023,
  "rating": 8.5,
  "duration": 180,
  "language": "English",
  "createdAt": "2024-01-16T12:45:00.000Z"
}
```

**Error Response (400 Bad Request):**
```json
{
  "message": "Title is required, Director is required"
}
```

---

### 3. Get a Specific Movie

**Request:**
```
GET /api/movies/:id
```

**Example:**
```
GET /api/movies/507f1f77bcf86cd799439011
```

**Response (200 OK):**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "title": "Inception",
  "director": "Christopher Nolan",
  "genre": "Science Fiction",
  "releaseYear": 2010,
  "rating": 8.8,
  "duration": 148,
  "language": "English",
  "createdAt": "2024-01-15T10:30:00.000Z"
}
```

**Error Response (404 Not Found):**
```json
{
  "message": "Movie not found"
}
```

---

### 4. Update a Movie

**Request:**
```
PUT /api/movies/:id
Content-Type: application/json

{
  "rating": 8.9,
  "duration": 150
}
```

**Example:**
```
PUT /api/movies/507f1f77bcf86cd799439011
```

**Response (200 OK):**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "title": "Inception",
  "director": "Christopher Nolan",
  "genre": "Science Fiction",
  "releaseYear": 2010,
  "rating": 8.9,
  "duration": 150,
  "language": "English",
  "createdAt": "2024-01-15T10:30:00.000Z"
}
```

---

### 5. Delete a Movie

**Request:**
```
DELETE /api/movies/:id
```

**Example:**
```
DELETE /api/movies/507f1f77bcf86cd799439011
```

**Response (200 OK):**
```json
{
  "message": "Movie deleted successfully",
  "deletedMovie": {
    "_id": "507f1f77bcf86cd799439011",
    "title": "Inception",
    "director": "Christopher Nolan"
  }
}
```

**Error Response (404 Not Found):**
```json
{
  "message": "Movie not found"
}
```

---

## 📊 Database Schema

### Movie Collection

```javascript
{
  "_id": ObjectId,
  "title": String,           // Required, trimmed
  "director": String,        // Required, trimmed
  "genre": String,           // Optional, trimmed, default: ""
  "releaseYear": Number,     // Optional, min: 1888
  "rating": Number,          // Optional, range: 0-10
  "duration": Number,        // Optional, min: 1 minute
  "language": String,        // Optional, trimmed, default: "English"
  "createdAt": Date          // Auto-generated, defaults to current time
}
```

### Validation Rules

| Field | Type | Required | Constraints |
|-------|------|----------|-------------|
| title | String | Yes | Trimmed, max length based on MongoDB |
| director | String | Yes | Trimmed, max length based on MongoDB |
| genre | String | No | Trimmed, default: empty string |
| releaseYear | Number | No | Must be >= 1888 |
| rating | Number | No | Must be between 0 and 10 |
| duration | Number | No | Must be >= 1 minute |
| language | String | No | Trimmed, default: "English" |

---

## 📁 Project Structure

```
movie-app/
├── public/                      # Frontend files
│   ├── index.html              # Main HTML page
│   ├── app.js                  # Frontend JavaScript logic
│   └── styles.css              # Styling
├── models/
│   └── Movie.js                # MongoDB schema definition
├── routes/
│   └── movies.js               # API route handlers
├── server.js                   # Express server setup
├── package.json                # Project dependencies
├── .env.example                # Environment variables template
├── .env                        # Environment variables (not tracked)
└── README.md                   # Documentation

### Detailed File Descriptions

- **server.js**: Initializes Express app, connects to MongoDB, sets up middleware
- **models/Movie.js**: Defines the Movie schema with validation rules
- **routes/movies.js**: Contains all CRUD endpoints and request handling
- **public/app.js**: Frontend logic for fetching/displaying/managing movies
- **public/index.html**: HTML structure for the user interface
- **public/styles.css**: Styling and responsive design
```

---

## 🎯 Usage Guide

### Adding a New Movie

1. Fill in the form fields:
   - **Title** (required)
   - **Director** (required)
   - **Genre** (optional)
   - **Release Year** (optional)
   - **Rating** (optional, 0-10)
   - **Duration** (optional, in minutes)
   - **Language** (optional, defaults to English)

2. Click "Add Movie" to submit
3. The new movie appears at the top of the list

### Editing a Movie

1. Find the movie in the list
2. Use the inline edit form to modify:
   - Rating
   - Duration
3. Click "Update" to save changes

### Deleting a Movie

1. Find the movie in the list
2. Click the "Delete" button
3. Confirm the deletion when prompted
4. The movie is removed from the catalog

### Refreshing the List

- Click the "Refresh" button to reload all movies
- The list automatically refreshes after adding or deleting

---

## 💻 Development Commands

### Start Development Server
```bash
npm run dev
```
- Watches for file changes
- Auto-restarts the server
- Best for development

### Start Production Server
```bash
npm start
```
- Standard server startup
- No file watching
- Use for deployment

### Check Server Health
```bash
curl http://localhost:3000/health
```

### Install Dependencies
```bash
npm install
```

---

## 🔍 Troubleshooting

### Issue: "Cannot connect to MongoDB"

**Solutions:**
- Ensure MongoDB is running locally: `mongod`
- Verify `MONGO_URI` in `.env` file
- If using MongoDB Atlas, check your IP whitelist settings
- Verify network connectivity to MongoDB cluster

### Issue: "Port 3000 already in use"

**Solutions:**
```bash
# Find process using port 3000
netstat -ano | findstr :3000

# Kill the process (Windows)
taskkill /PID <PID> /F

# Or change PORT in .env file
PORT=3001
```

### Issue: "Module not found" error

**Solutions:**
```bash
# Reinstall all dependencies
npm install

# Clear npm cache
npm cache clean --force

# Reinstall packages
npm install
```

### Issue: Validation errors when creating movies

**Common Causes:**
- Missing required fields (Title or Director)
- Rating outside 0-10 range
- Release year before 1888
- Non-numeric values for numeric fields

**Solution:** Check the error message in the form for specific details

### Issue: Blank page after starting server

**Solutions:**
- Check browser console for JavaScript errors
- Verify server is running: `curl http://localhost:3000/health`
- Clear browser cache
- Check that `public/` files exist

---

## 📝 Notes

- All movie data is persisted in MongoDB
- The application uses RESTful API design principles
- Frontend communicates with backend via JSON
- Timestamps are automatically recorded for each movie
- Movies are displayed in reverse chronological order (newest first)

---

## 📄 License

ISC License - See package.json for details

---

**Last Updated:** January 2024
**Version:** 1.0.0
