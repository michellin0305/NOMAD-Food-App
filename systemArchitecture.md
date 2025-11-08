# NOMAD System Architecture 🧩

## Overview
NOMAD is a real-time, AI-driven food discovery platform built to match users’ hunger context with nearby restaurant availability. It integrates personalized recommendations, restaurant management tools, and quick user actions into a single system.

## Architecture Diagram (Mermaid)
```mermaid
flowchart TD
  App[Mobile App (React Native)]
  API[API Gateway - Node/Express]
  RE[Recommendation Engine (Python service)]
  DB[MongoDB Atlas]
  EXT[External APIs<br/>Google Maps, OpenTable]
  RD[Restaurant Dashboard (React Web)]

  App -->|Request: Feed Me Now| API
  API --> RE
  API --> DB
  API --> EXT
  RD --> API
  RE --> DB
  API -->|Return top 3| App

## Components

### 1. **Frontend**
- **User App (React Native):**
  - Displays nearby restaurants and “Feed Me Now” results.
  - Integrates with Maps and location APIs.
  - Handles user login and preferences.

- **Restaurant Dashboard (React Web App):**
  - Allows restaurants to update availability, post offers, and monitor engagement.
  - Communicates with backend APIs for real-time sync.

---

### 2. **Backend (Node.js / Express.js)**
- Acts as the central hub for all client requests.  
- Responsible for:
  - Routing and API management  
  - Connecting to the ML service for recommendations  
  - Authentication and user management via Firebase  
  - Managing session data and restaurant activity logs  

---

### 3. **Database (MongoDB Atlas)**
- **Users Collection:** profiles, preferences, and activity logs  
- **Restaurants Collection:** menus, availability, ratings, offers  
- **Recommendations Collection:** system-generated matches and analytics  

---

### 4. **Recommendation Engine (Python Microservice)**
- Uses historical user data, contextual signals (time, mood, weather), and restaurant metadata.  
- Algorithm: Collaborative + content-based filtering to deliver 3 top picks.  
- Communicates with backend through REST API calls.

---

### 5. **Communication Flow**
1. User hits **“Feed Me Now”** on the app.  
2. The frontend sends a request to the backend with user context (location, time, mood).  
3. Backend queries the Recommendation Engine.  
4. The engine returns top 3 restaurant matches.  
5. Backend fetches details (location, rating, menu) and returns them to the frontend.  
6. User acts (navigate, reserve, or order).  

---

### 6. **Technical Feasibility**
- **Scalability:** Microservices and cloud-based DB allow easy scaling.  
- **Speed:** Minimal API calls and caching of restaurant data ensure fast response.  
- **Maintainability:** Modular architecture allows teams to independently update components.  
- **Security:** HTTPS, JWT authentication, and Firebase Auth protect user data.  

---

### 7. **Deployment**
- **Backend:** Hosted on AWS Lambda or EC2  
- **Database:** MongoDB Atlas (Cloud)  
- **Frontend:** Deployed on App Store (iOS) and Play Store (Android)  
- **CI/CD:** GitHub Actions + Docker for continuous integration  

---

### 8. **Future Enhancements**
- AI voice assistant (“What should I eat today?”)  
- Social discovery (see what friends are eating)  
- Integration with ride-hailing apps for instant restaurant trips  