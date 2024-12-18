
# JP Vocabulary Server

This is the server-side implementation of the Japanese Vocabulary Learning Application (JP Vocabulary). The server is built using Express, Node.js, Mongoose, MongoDB, Bcrypt, and JWT for authentication and data management.

## Features
- **Express**: A fast and lightweight web framework for Node.js.
- **Node.js**: JavaScript runtime for building scalable server-side applications.
- **Mongoose**: MongoDB object modeling tool designed to work in an asynchronous environment.
- **MongoDB**: NoSQL database for storing user and lesson data.
- **Bcrypt**: For secure password hashing.
- **JWT (JSON Web Token)**: For handling authentication and authorization.


## Installation Instructions

Follow these steps to set up and run the server locally:

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd <project-folder>
   ```

2. **Install dependencies**:
   Install all the necessary Node.js packages by running the following command:
   ```bash
   npm install
   ```

3. **Set up environment variables**:
   - Create a `.env` file in the root directory of the server.
   - Copy the contents of the `.env.example` file into the `.env` file and modify the values as required. Ensure to add the MongoDB URI and JWT secret key.
  

4. **Run the server**:
   You can run the server using `npm` or `nodemon` (if you have it installed).

   - **For development** (using nodemon):
     ```bash
     npm run dev
     ```

   This will start the server on the port defined in `.env` (default: 5000).

## Error Handling

The server includes error handling for common scenarios such as:

- **Authentication Errors**: Invalid credentials, expired tokens, etc.
- **Validation Errors**: Missing or invalid data in requests.
- **Server Errors**: Internal server issues or unexpected exceptions.

Error messages are returned in a standard format, which includes the error code and message.

## Authentication & Authorization

### JWT Authentication
- **Login**: Users authenticate with their email and password. Upon successful login, a JWT token is generated and returned.
- **Protected Routes**: Routes requiring authentication are protected by the `authMiddleware` which validates the JWT token.

### User Registration and Login
- Users can register by providing their name, email, password, and an optional profile photo. Passwords are hashed using `bcrypt`.
- On successful registration, the user data is stored in MongoDB.
- For login, users are authenticated using email and password. The JWT token is sent in the response, which is required for accessing protected routes.

## Routes

### User Routes
- `POST /api/auth/register`: Register a new user
- `POST /api/auth/login`: Login a user and return JWT token
- `GET /api/auth/user`: Get the logged-in user's data (protected route)

### Lesson Routes
- `GET /api/lessons`: Get all lessons
- `POST /api/lessons`: Add a new lesson (admin-only)
- `PUT /api/lessons/:id`: Update a lesson (admin-only)
- `DELETE /api/lessons/:id`: Delete a lesson (admin-only)

### Vocabulary Routes
- `GET /api/vocabularies`: Get all vocabularies
- `POST /api/vocabularies`: Add a new vocabulary (admin-only)
- `PUT /api/vocabularies/:id`: Update a vocabulary (admin-only)
- `DELETE /api/vocabularies/:id`: Delete a vocabulary (admin-only)

## Middleware

### Authentication Middleware
The `authMiddleware.js` checks for the presence of a valid JWT token in the request headers. If the token is valid, the request proceeds; otherwise, an error is thrown.

### Error Handling Middleware
The `errorMiddleware.js` handles errors by sending a consistent error response with the appropriate status code and message.

## Development Tips

- Ensure the MongoDB instance is running and accessible.
- If using `nodemon`, it will automatically restart the server on file changes.
- Use Postman or similar tools to test the API endpoints.
- Follow clean code practices by breaking logic into functions and handling errors gracefully.

## Conclusion

This server-side implementation provides all the functionality required for the **Japanese Vocabulary Learning Application**. It handles user authentication, lesson management, and vocabulary management with secure and scalable code.
