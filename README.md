# Digital Banking Backend System  
**Backend External API Assignment – NibssByPhoenix**

This project is a backend system built for a simulated digital banking environment.  
It supports customer onboarding, account creation, secure banking operations, and transaction privacy using **Node.js, Express, MongoDB, and JWT authentication**.

---

##  Objective

Develop a functional backend system that supports:

- Customer onboarding via BVN or NIN verification
- Account creation with initial funding
- Core banking operations
- Transaction history tracking
- Data privacy and access control
- Integration with the NibssByPhoenix APIs


## Features Implemented

### 1. Customer Onboarding
- BVN verification
- Customer must be successfully verified before onboarding is completed
- JWT-based authentication flow

---

### 2. Account Creation
- One account per verified customer
- Unique account number generation
- Each newly created account is pre-funded with **₦15,000**

---

### 3. Core Banking Operations
- **Name Enquiry**
- **Funds Transfer**
  - Intra-bank transfer
  - Inter-bank transfer (simulated across different fintechsin one database)
- **Account Balance Check**
- **Transaction Status Check**


### 4. Transaction History & Data Privacy
- Customers can only view their own transaction history
- Strict account ownership validation
- Proper data isolation enforced using JWT + account ownership checks


## Tech Stack

- **Node.js**
- **Express.js**
- **MongoDB / Mongoose**
- **JWT (jsonwebtoken)**
- **Nodemailer**
- **Swagger**
- **Postman** (for testing)

---

## Project Structure

Configs/
Controllers/
HtmlEmailTemplates/
Middleware/
Models/
Routes/
Utils/
app.js
package.json
README.md

## Installation & Setup
1. **Clone Repository**
git clone <your-repository-link>
cd NibssByPhoenix
2. **Install Dependencies**
npm install
3. **Create .env File**

Create a .env file in the root directory and add:

PORT=4040
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
EMAIL_USER=your_email_address
EMAIL_PASS=your_email_app_password
4. ## Start Server

## Development:

npm run dev

## Production:

npm start
🔐 Authentication Flow
**Step 1: Onboard Fintech**

Use the onboarding endpoint to register a fintech.

This returns:

apiKey
apiSecret
bankCode
bankName
**Step 2: Generate JWT Token**

Use:

POST /api/auth/token

with:

{
  "apiKey": "your_api_key",
  "apiSecret": "your_api_secret"
}

This returns a JWT token.

**Step 3: Use Bearer Token**

Use the token in protected routes:

Authorization: Bearer <your_token>
## Sample Endpoints

**Generate Token**
POST /api/auth/token

**Create Account**
POST /api/fintech/create-account

Sample body:

{
  "kycType": "bvn",
  "kycID": "12345678901",
  "dob": "2000-01-01"
}

**Name Enquiry**
GET /api/fintech/name-enquiry/:accountNumber

**Transfer Funds**
POST /api/fintech/transfer

Sample body:

{
  "from": "1234567890",
  "to": "0987654321",
  "amount": 2000
}

**Account Balance**
GET /api/fintech/balance/:accountNumber

**Transaction Status**
GET /api/fintech/transaction/:reference

**Transaction History**
GET /api/fintech/history/:accountNumber

## 🔒 Data Privacy Implementation

The system ensures strict data isolation by validating account ownership against the authenticated fintech before returning transaction or account information.

This prevents:

unauthorized balance access
unauthorized transaction history access
access to another customer’s data

**Testing**

All endpoints were tested using Postman.

Test scenarios covered:

onboarding
token generation
account creation
successful transfer
insufficient funds
invalid account
transaction history isolation

**Author**
Susan Oyeniyi-Israel
EXTERNAL API ASSIGNMENT