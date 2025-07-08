# Blog App

A full-stack blog application built with React (frontend), Express (backend), and MySQL (database). This project allows users to register, log in, create, update, and delete blog posts, with image upload support.

## Features
- User authentication (register, login, logout)
- Create, read, update, and delete blog posts
- Image upload for posts
- Category filtering
- MySQL database integration
- RESTful API

## Folder Structure
├── api/ # Backend (Express, Node.js)
│ ├── controllers/
│ ├── routes/
│ ├── db.js
│ ├── index.js
│ ├── createDefaultUser.js
│ └── package.json
├── client/ # Frontend (React)
│ ├── public/
│ ├── src/
│ └── package.json

## Prerequisites
- Node.js (v14+ recommended)
- MySQL server

## Database Setup
1. Create a MySQL database named `blog`:
   ```sql
   CREATE DATABASE blog;
   ```
2. Create the required tables (example):
   ```sql
   CREATE TABLE users (
     id INT AUTO_INCREMENT PRIMARY KEY,
     username VARCHAR(255) NOT NULL,
     email VARCHAR(255) NOT NULL,
     password VARCHAR(255) NOT NULL,
     img VARCHAR(255)
   );

   CREATE TABLE posts (
     id INT AUTO_INCREMENT PRIMARY KEY,
     title VARCHAR(255) NOT NULL,
     `desc` TEXT,
     img VARCHAR(255),
     cat VARCHAR(255),
     date DATETIME,
     uid INT,
     FOREIGN KEY (uid) REFERENCES users(id)
   );
   ```
3. Update the MySQL credentials in `api/db.js` if needed:
   ```js
   export const db = mysql.createConnection({
     host: "localhost",
     user: "root",
     password: "root",
     database: "blog",
   });
   ```
4. (Optional) Create a default user by running:
   ```bash
   cd api
   node createDefaultUser.js
   ```

## Backend Setup (API)
1. Install dependencies:
   ```bash
   cd api
   npm install
   ```
2. Start the backend server:
   ```bash
   npm start
   ```
   The backend runs on [http://localhost:8081](http://localhost:8081)

## Frontend Setup (React)
1. Install dependencies:
   ```bash
   cd client
   npm install
   ```
2. Start the frontend app:
   ```bash
   npm start
   ```
   The frontend runs on [http://localhost:3000](http://localhost:3000)

## API Endpoints
### Auth
- `POST /api/auth/register` — Register a new user
- `POST /api/auth/login` — Log in
- `POST /api/auth/logout` — Log out

### Posts
- `GET /api/posts` — Get all posts (optionally filter by `cat` query param)
- `GET /api/posts/:id` — Get a single post by ID
- `POST /api/posts` — Create a new post
- `PUT /api/posts/:id` — Update a post
- `DELETE /api/posts/:id` — Delete a post
- `POST /api/upload` — Upload an image file

## Notes
- The backend uses CORS to allow requests from the frontend.
- Uploaded images are stored in `client/public/upload`.
- JWT is used for authentication; tokens are stored in cookies.
- For development, some authentication checks may be temporarily disabled in controllers.

## License
This project is licensed under the ISC License.
