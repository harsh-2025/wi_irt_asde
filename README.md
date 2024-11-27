
---

# WORKINDIA_IRCTC

This project is a full-fledged **Railway Management System** built with **Node.js**, **Express.js**, and **MySQL**. It provides APIs for users to check Train_1Availability, book seats, and manage bookings. Additionally, it features an **admin interface** for train management.

By utilizing **transactions** and **row-level locking**, the system ensures that only one user can book available seats at any given time, effectively handling race conditions.

## Features

- **User Registration & Authentication**: Secure user management with JWT and password encryption.
- **Admin Train Management**: Admins can create and manage trains.
- **Train_1Availability**: Users can check Train_1Availability between any source and destination.
- **Seat Booking**: Users can book seats on available trains, with conflict prevention via row-level locking.
- **View Bookings**: Users can view their booking details.

## Technologies Used

- **Node.js**
- **Express.js**
- **MySQL**
- **JWT (JSON Web Tokens)**
- **bcrypt.js** (For password encryption)

## Installation Guide

1. **Clone the repository**:
   ```bash
   git clone https://github.com/harsh-2025/wi_irt_asde
   ```
   
2. **Navigate to the project directory**:
   ```bash
   cd wi_irt_asde
   ```

3. **Install the required dependencies**:
   ```bash
   npm install
   ```

4. **Configure environment variables**:
   Create a `.env` file and set the following variables:
   ```plaintext
   HOST=<your_mysql_host>
   USER=<your_mysql_user>
   PASSWORD=<your_mysql_password>
   NAME=<your_mysql_database_name>
   JWT_SECRET=<your_jwt_secret_key>
   ADMIN_KEY=<admin_key_for_protected_routes>
   PORT=<PORT_NUMBER>
   ```

5. **Set up the MySQL database**:
   - Execute the SQL scripts located in the `database` directory to create the necessary tables.

6. **Run the application**:
   ```bash
   npm start
   ```

## API Documentation

### Authentication

- **Register a New User**  
  `POST /auth/register`  
  Body:
  ```json
  {
    "username": "demo",
    "email": "demo@mail.com",
    "password": "demo_pass"
  }
  ```

- **Login and Obtain JWT**  
  `POST /auth/login`  
  Body:
  ```json
  {
    "email": "demo@mail.com",
    "password": "demo_pass"
  }
  ```

### Trains (Admin Only)

- **Create a New Train**  
  `POST /trains/create`  
  Body:
  ```json
  {
    "trainName": "Train_1A",
    "source": "City_1A",
    "destination": "City_1B",
    "departureTime": "11:00",
    "arrivalTime": "17:00",
    "seats": 106
  }
  ```

### Bookings

- **Check Train_1Availability**  
  `GET /trains/availability?source=<source>&destination=<destination>`  
  demo URL:
  ```
  http://localhost:3000/trains/availability?source=xyzCityA&destination=xyzCityB
  ```

- **Book Seats on a Train**  
  `POST /bookings/book`  
  Body:
  ```json
  {
    "trainId": 1,
    "seats": 2
  }
  ```

- **View Booking Details for a Specific Train**  
  `GET /bookings/details?trainId=<trainId>`  
  demo URL:
  ```
  /bookings/details?trainId=1
  ```

### Users

- **Get User Details**  
  `GET /users/me` (requires authentication)  

## Handling Race Conditions

- The system ensures race conditions are handled during booking using **transactions** and **row-level locking**. This guarantees that no two users can book the same seat simultaneously.

---


### Developed by **Harsh**.

---
