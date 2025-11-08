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
