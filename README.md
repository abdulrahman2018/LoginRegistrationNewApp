

# LoginRegistrationApp

## Overview

**LoginRegistrationApp** is a full-stack web application designed to handle user registration and login functionalities. The project consists of two main components:

1. **Backend**: Built with ASP.NET Core 7, the backend handles API requests for user registration and login. It connects to a Microsoft SQL Server database to manage user data.
2. **Frontend**: Developed using React.js, the frontend provides a user interface for registration and login. It communicates with the backend API to perform the required operations.

## Features

- **User Registration**: Allows new users to create an account with a username, email, and password.
- **User Login**: Enables registered users to log in using their email and password.
- **Password Visibility Toggle**: Users can view or hide their password during login and registration.
- **Responsive Design**: The application is designed to be mobile-friendly and responsive across different devices.

## Technologies Used

- **Backend**:
  - ASP.NET Core 7
  - Microsoft SQL Server
  - C#
  - Entity Framework Core (for data access)
  
- **Frontend**:
  - React.js
  - Bootstrap (for styling)
  - Axios (for making HTTP requests)

## Setup

### Backend

1. **Clone the Repository**

   ```bash
   git clone https://github.com/abdulrahman2018/LoginRegistrationApp.git
   ```

2. **Navigate to the Backend Directory**

   ```bash
   cd LoginRegistrationApp/Backend
   ```

3. **Restore Packages and Build the Project**

   ```bash
   dotnet restore
   dotnet build
   ```

4. **Run the Backend**

   ```bash
   dotnet run
   ```

   The backend will be available at `https://localhost:7167`.

5. **Database Setup**

   Ensure you have Microsoft SQL Server installed. Create a database named `TestCoreApp` and run the SQL scripts for creating tables and stored procedures:

   ```sql
   CREATE DATABASE TestCoreApp;
   USE TestCoreApp;

   CREATE TABLE USERS (
       ID INT IDENTITY (1,1) PRIMARY KEY,
       Username VARCHAR(200),
       Email VARCHAR(200),
       Password VARCHAR(200)
   );

   CREATE PROC sp_register
       @Username VARCHAR(100),
       @Email VARCHAR(100),
       @Password VARCHAR(100),
       @ErrorMessage VARCHAR(200) OUTPUT
   AS
   BEGIN
       IF NOT EXISTS (SELECT 1 FROM USERS WHERE Email = @Email)
       BEGIN
           INSERT INTO USERS (Username, Email, Password)
           VALUES (@Username, @Email, @Password);
           SET @ErrorMessage = 'User created successfully';
       END
       ELSE
       BEGIN
           SET @ErrorMessage = 'User already exists with the same email';
       END
   END;

   CREATE PROC sp_login
       @Email VARCHAR(100),
       @Password VARCHAR(100)
   AS
   BEGIN
       SELECT * FROM USERS
       WHERE Email = @Email AND Password = @Password;
   END;
   ```

### Frontend

1. **Navigate to the Frontend Directory**

   ```bash
   cd LoginRegistrationApp/Frontend
   ```

2. **Install Dependencies**

   ```bash
   npm install
   ```

3. **Run the Frontend**

   ```bash
   npm start
   ```

   The frontend will be available at `http://localhost:3000`.

## Project Structure

- **Backend**:
  - `Controllers/`: Contains API controllers.
  - `Models/`: Contains data models and data access layer (DAL).
  - `Program.cs`: Configures and starts the ASP.NET Core application.

- **Frontend**:
  - `src/`: Contains React components, CSS files, and other frontend assets.
  - `public/`: Contains public assets like `index.html`.

## Usage

- **Registration**: Navigate to the registration page, enter the username, email, and password, then submit the form to create a new account.
- **Login**: Navigate to the login page, enter the email and password, then submit the form to log in.

## Contributing

Feel free to fork the repository, make changes, and submit pull requests. Contributions are welcome!

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

Replace `abdulrahman2018` in the clone URL with your actual GitHub username and update any other project-specific details as needed.
