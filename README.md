# Car Insurance Recommendation Backend

This repository contains the backend server for the AI Insurance Recommendation Application. It serves as the core logic provider, interacting with the Google Generative AI API to power the "Tina" AI consultant and manage chat sessions.

## 1. Project Overview

The "Car Insurance Recommendation Backend" is a Node.js Express application that facilitates communication between the frontend chat interface and the Google Generative AI model. It manages chat histories, integrates detailed insurance product knowledge into the AI's system instructions, and enforces business rules for insurance recommendations.

### Key Responsibilities:
- **Google Generative AI Integration**: Connects to the Google Generative AI API to generate AI responses based on user queries.
- **Chat History Management**: Stores and retrieves conversation histories in memory for ongoing sessions (for production, this would be a persistent database).
- **AI System Instruction**: Dynamically provides the AI (Tina) with its persona, rules for interaction, and comprehensive knowledge about Mechanical Breakdown Insurance (MBI), Comprehensive, and Third-Party car insurance policies, including detailed descriptions and external links (MoneyHub guides).
- **Business Rule Enforcement**: Incorporates specific business rules for recommending insurance products, such as vehicle age restrictions for Comprehensive insurance and exclusions for MBI.
- **API Endpoint**: Exposes a `/chat` endpoint for the frontend to send user messages and receive AI responses and updated chat history.

## 2. Technologies Used
- **Node.js**: JavaScript runtime environment.
- **Express.js**: Web application framework for Node.js.
- **@google/generative-ai**: Official Google Generative AI client library for Node.js.
- **cors**: Middleware to enable Cross-Origin Resource Sharing.
- **dotenv**: Loads environment variables from a `.env` file.
- **Vitest**: Fast unit test framework for Node.js.
- **Supertest**: Library for testing HTTP servers.

## 3. Installation and Setup

To get this backend server up and running locally, follow these steps:

### Clone the Repository:
```bash
git clone <YOUR_REPOSITORY_URL>
cd car-insurance-recommendation-backend


### Install Dependencies:
Navigate to the project's root directory and run:
```bash
npm install

### Configure Environment Variables:
You need to set up your Google API Key. Create a file named .env in the root directory of this project (car-insurance-recommendation-backend/). Add your Google Generative AI API key to this file:

```bash
GOOGLE_API_KEY=YOUR_GEMINI_API_KEY_HERE
PORT=3001 # Optional: Specify a port, defaults to 3001 if not set
Replace YOUR_GEMINI_API_KEY_HERE with your actual API key obtained from the Google AI Studio.

## 4. Running the Application
Once dependencies are installed and the .env file is configured, you can start the backend server:

```bash
npm run dev
# or
# node server.js
The server will start and listen on the specified PORT (defaulting to 3001). You should see a message in your console like: Backend server running on http://localhost:3001.

## 5. API Endpoint
The backend provides a single primary API endpoint:

POST /chat
Description: Handles chat messages from the frontend, communicates with the Gemini AI model, and returns the AI's response along with the updated chat history.

Request Body:
```json


{
    "sessionId": "string",  // Unique identifier for the chat session
    "userResponse": "string" // User's message (can be an empty string for the initial greeting)
}
Response Body (Success 200):

```json
{
    "response": "string", // AI's generated response
    "history": [          // Full conversation history for the session
        { "role": "user", "text": "string" },
        { "role": "model", "text": "string" }
        // ... more messages
    ]
}
Response Body (Error 400/500):
```json


{
    "error": "string" // Error message
}

## 6. System Instruction Details (AI Persona and Rules)
The server.js file dynamically constructs a detailed system instruction for the Google Generative AI model (gemini-2.0-flash). This instruction defines Tina's behavior and knowledge:

Role: AI insurance consultant named Tina, focused on helping users choose suitable car insurance.
Greeting: Must start with a specific polite greeting asking for permission to ask personal questions.
Questioning: Questions should be concise, natural, and adapt to previous answers. Specific order of questions (vehicle type, make/model, age, value, parking, usage, concerns, location) is enforced.
Product Knowledge: Comprehensive details on MBI, Comprehensive, and Third-Party car insurance (including pros, cons, typical costs, exclusions, and MoneyHub links) are embedded.
Business Rules: Strict adherence to rules like:
MBI is NOT available for trucks or racing cars.
Comprehensive insurance is ONLY available for motor vehicles LESS THAN 10 years old (i.e., 9 years old or less).
Recommendation Style: Emphasizes comparing quotes, advises on customer support, uses numbered lists for choices, and provides clear, reasoned recommendations.

## 7. Testing
Unit tests for the backend API endpoint are written using Vitest and Supertest.

To run the tests:

bash


npm test
# or
# yarn test
# pnpm test
The tests cover:

Initial chat greeting and session handling.
Processing subsequent user messages and AI responses.
Error handling for invalid request bodies.
Graceful handling of Google Generative AI API errors.

## 8. Contributing
Contributions to this project are welcome! Feel free to open issues for bug reports, feature suggestions, or submit pull requests.

## 9. License
This project is licensed under the [Specify your license here, e.g., MIT License].

## 10. Contact
If you have any questions or feedback, please feel free to reach out via taka.kroger@gmail.com or refer to the repository's Issues section].