# 🌍 Solea Travel Planner — Backend

Welcome to the **Solea** backend API — a RESTful travel planning server built with Node.js, Express.js, MongoDB, Neo4j, and Redis. This backend powers everything from user authentication and trip planning to graph-based recommendations and session-based caching.

---

## 📦 Tech Stack

- **Node.js + Express** — API server
- **MongoDB + Mongoose** — Core data storage
- **Neo4j (AuraDB)** — Graph-based city & recommendation system
- **Redis (Redis Cloud)** — Session caching and draft trip storage
- **JWT Authentication** — Secure user sessions
- **Bcrypt** — Password hashing
- **CORS + Dotenv + Nodemon** — Dev & security helpers

---

## 🔐 Auth Routes

- POST /api/auth/register — Register a new user
- POST /api/auth/login — Login and receive JWT token

---

## 👤 User Routes

- GET /api/users/profile — Get logged-in user profile (🔒 JWT required)
- PUT /api/users/preferences — Update preferences
- GET /api/users/:id/trips — Fetch user's trips

---

## ✈️ Trip Routes

- POST /api/trips — Create a trip
- POST /api/trips/:tripId/cities — Add city to trip
- POST /api/trips/:tripId/hotels — Add hotel to trip
- GET /api/trips/:tripId — Trip details
- POST /api/trips/:tripId/confirm — Confirm and finalize

---

## 🏙️ City Routes

- GET /api/cities — All cities
- GET /api/cities/continent/:continent — Cities in a continent
- GET /api/cities/:cityId — Details of a city

---

## 📝 Blog Routes

- GET /api/blogs — Fetch all blog posts

---

## 🤖 Recommendation Routes (Neo4j)

Neo4j is used to model cities, tags, and relationships for smarter travel suggestions.

- GET /api/recommendations/city/:cityId — Get similar city recommendations based on tags and relationships
- GET /api/recommendations/user/:userId — Get personalized suggestions based on user's trip history

Neo4j is connected via the official Neo4j JavaScript driver using a secure `neo4j+s://` AuraDB URI.

Graph structure:
- City nodes with TAGGED_AS relationships to Tag
- User connected to City through VISITED relationship

---

## 🧠 Redis Routes (Trip Draft Caching)

Redis is used to temporarily store in-progress trip drafts per user.

- POST /api/redis/draft/:userId — Save a draft trip
- GET /api/redis/draft/:userId — Load a saved draft
- DELETE /api/redis/draft/:userId — Clear a saved draft

The backend uses `cacheService.js` to interact with Redis using the `tripDraft:<userId>` key format.

---

## 🧬 Seeding Setup

1. Make sure all city JSON files (Africa.json, Asia.json, Europe.json, etc.) are inside the `data/` directory.
2. From the root of your backend project, run the following command to populate the database:

→ node scripts/seedCities.js

This script will:

- Connect to your MongoDB instance using `.env` config.
- Clear existing cities and hotels (optional behavior).
- Insert all cities along with their tagged attractions and categorized hotels (7-star to 3-star).
- Automatically establish references between cities and hotels using ObjectId.

Each city entry includes:
- continent, country, city
- tags for personalization
- attractions (top 10 spots)
- hotels with pricePerNight and star category

Each hotel is stored as a separate document and linked to its respective city.

---

## 🚀 Deployment

- MongoDB hosted on MongoDB Atlas
- Redis hosted on Redis Cloud
- Neo4j hosted on Neo4j AuraDB
- Backend deployed on Render
- .env used to manage secure secrets

---

## 🧾 Author

Made with 💙 for Solea Project — *Your next-level travel companion.*