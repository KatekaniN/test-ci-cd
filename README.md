# fullstack-nodejs-app

A basic full-stack HTML/Node.js application for User Management.

## Overview

This project is a simple User Management application demonstrating a full-stack setup. The frontend is built with HTML, CSS, and vanilla JavaScript, while the backend is a Node.js application using the Express framework. It allows users to be added and viewed.

**Technologies Used:**

*   **Frontend:** HTML, CSS, JavaScript
*   **Backend:** Node.js, Express.js
*   **Deployment:** Configured for Firebase Hosting (via GitHub Actions)

## Features

*   **Add Users:** Users can be added with a name and email address through a simple form.
*   **View Users:** Display a list of all added users.
*   **API Health Check:** Endpoint to verify backend server status.
*   **In-Memory Data Storage:** The application uses in-memory storage for user data. This means data will be reset if the server restarts.

## Prerequisites

To run this project locally, you will need:

*   [Node.js](https://nodejs.org/) (which includes npm, the Node Package Manager)

## Getting Started

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd fullstack-nodejs-app
    ```
2.  **Install dependencies:**
    Install the backend dependencies using npm:
    ```bash
    npm install
    ```
    There are no separate frontend build steps or dependencies to install beyond what's handled by the browser.

3.  **API Configuration (Frontend):**
    The frontend (`public/index.html`) is configured to communicate with the backend API at `http://localhost:3000/api`. If your backend runs on a different port or host, you may need to update the `API_BASE_URL` constant in the `<script>` section of `public/index.html`.

## Running the Application

1.  **Start the Backend Server:**
    You can run the server using one of the following npm scripts:
    *   For production mode:
        ```bash
        npm start
        ```
    *   For development mode (with automatic restarts on file changes, using `nodemon`):
        ```bash
        npm run dev
        ```
    The server will typically start on `http://localhost:3000`.

2.  **Open the Frontend:**
    Open the `public/index.html` file in your web browser.
    You can usually do this by navigating to `file:///path/to/your/project/public/index.html` or by using a simple HTTP server if you prefer.

    Once both are running, you should be able to interact with the User Management application.

## API Endpoints

The backend server (`server.js`) provides the following RESTful API endpoints:

*   **`GET /api/health`**
    *   Description: Checks the health of the server.
    *   Response:
        ```json
        {
          "success": true,
          "message": "Server is running",
          "timestamp": "YYYY-MM-DDTHH:mm:ss.sssZ"
        }
        ```

*   **`GET /api/users`**
    *   Description: Fetches all users.
    *   Response:
        ```json
        {
          "success": true,
          "data": [
            {
              "id": 1,
              "name": "John Doe",
              "email": "john.doe@example.com",
              "createdAt": "YYYY-MM-DDTHH:mm:ss.sssZ"
            }
            // ... other users
          ]
        }
        ```

*   **`POST /api/users`**
    *   Description: Creates a new user.
    *   Request Body:
        ```json
        {
          "name": "Jane Doe",
          "email": "jane.doe@example.com"
        }
        ```
    *   Response (Success - 201):
        ```json
        {
          "success": true,
          "data": {
            "id": 2,
            "name": "Jane Doe",
            "email": "jane.doe@example.com",
            "createdAt": "YYYY-MM-DDTHH:mm:ss.sssZ"
          },
          "message": "User created successfully"
        }
        ```
    *   Response (Error - 400 for missing fields):
        ```json
        {
          "success": false,
          "message": "Name and email are required"
        }
        ```

*   **`GET /api/users/:id`**
    *   Description: Fetches a specific user by their ID.
    *   Response (Success - 200):
        ```json
        {
          "success": true,
          "data": {
            "id": 1,
            "name": "John Doe",
            "email": "john.doe@example.com",
            "createdAt": "YYYY-MM-DDTHH:mm:ss.sssZ"
          }
        }
        ```
    *   Response (Error - 404 if user not found):
        ```json
        {
          "success": false,
          "message": "User not found"
        }
        ```

*   **`PUT /api/users/:id`**
    *   Description: Updates an existing user's information.
    *   Request Body (include fields to update):
        ```json
        {
          "name": "Johnathan Doe",
          "email": "johnathan.doe@example.com"
        }
        ```
    *   Response (Success - 200):
        ```json
        {
          "success": true,
          "data": {
            "id": 1,
            "name": "Johnathan Doe",
            "email": "johnathan.doe@example.com",
            "createdAt": "YYYY-MM-DDTHH:mm:ss.sssZ",
            "updatedAt": "YYYY-MM-DDTHH:mm:ss.sssZ"
          },
          "message": "User updated successfully"
        }
        ```
    *   Response (Error - 404 if user not found):
        ```json
        {
          "success": false,
          "message": "User not found"
        }
        ```

*   **`DELETE /api/users/:id`**
    *   Description: Deletes a user by their ID.
    *   Response (Success - 200):
        ```json
        {
          "success": true,
          "message": "User deleted successfully"
        }
        ```
    *   Response (Error - 404 if user not found):
        ```json
        {
          "success": false,
          "message": "User not found"
        }
        ```

## Deployment

This project is configured for deployment to **Firebase Hosting**.
The `.github/workflows/` directory contains GitHub Actions that automate the deployment process:
*   A preview deployment is created for each pull request.
*   Changes are deployed to the live Firebase Hosting site upon merging to the main branch.

Refer to `firebase.json` for hosting configuration and `.firebaserc` for project details.

## License

This project is licensed under the MIT License.
