# API Gateway

**Part of [Airline Booking & Operations Backend](https://github.com/hussainaabid99/AirTicketBookingService)**

## 🔗 Related Microservices

- [Auth Service](https://github.com/hussainaabid99/Auth_Service) - Authentication and user management
- [Flights & Search Service](https://github.com/hussainaabid99/FlightsAndSearchService) - Flight catalog and search
- [Air Ticket Booking Service](https://github.com/hussainaabid99/AirTicketBookingService) - Booking orchestration
- [Reminder Service](https://github.com/hussainaabid99/ReminderService) - Notification management

## 🎯 Overview

The API Gateway serves as the central entry point for all client requests, providing authentication, rate limiting, and intelligent routing to appropriate microservices.

## ✨ Features

- **Reverse Proxy**: Routes requests to appropriate microservices
- **Authentication**: Validates JWT tokens before forwarding requests
- **Rate Limiting**: Prevents API abuse (5 requests per 2 minutes)
- **Request Logging**: Morgan middleware for request monitoring
- **Service Discovery**: Hardcoded routing to microservices

## 🛠️ Technology

- Express.js
- http-proxy-middleware
- express-rate-limit
- Morgan (logging)
- Axios (HTTP client)

## 🚀 Quick Start

```bash
npm install
node index.js
```

## ⚙️ Configuration

- **Port**: 3005 (hardcoded)
- **Rate Limit**: 5 requests per 2 minutes
- **Protected Routes**: `/bookingservice/*`

## �� API Endpoints

### Public Endpoints
- `GET /home` - Health check endpoint

### Protected Endpoints
- `GET /bookingservice/*` - Proxied to Booking Service (port 3002)

## 🔐 Authentication Flow

1. Client sends request with `x-access-token` header
2. Gateway validates token with Auth Service
3. If valid, request is proxied to target service
4. If invalid, returns 401 Unauthorized

## �� Service Routing

| Route | Target Service | Port | Description |
|-------|----------------|------|-------------|
| `/bookingservice/*` | Booking Service | 3002 | Ticket booking operations |

## �� Request Flow

Client Request → Gateway → Auth Validation → Service Proxy → Response


## 🚨 Error Handling

- **401 Unauthorized**: Invalid or missing JWT token
- **429 Too Many Requests**: Rate limit exceeded
- **500 Internal Server Error**: Service communication issues

## 🔧 Environment Variables

Currently hardcoded, but can be externalized:
- `PORT`: Gateway port (default: 3005)
- `AUTH_SERVICE_URL`: Auth service endpoint
- `BOOKING_SERVICE_URL`: Booking service endpoint

## 🚀 Future Improvements

- Dynamic service discovery
- Load balancing
- Circuit breaker pattern
- Request/response transformation
- API versioning
- Caching layer
