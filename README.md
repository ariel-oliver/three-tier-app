# Three Tier Application

A modern three-tier application demonstrating full-stack development with containerized deployment.

## Architecture

- **Frontend**: HTMX with modern CSS and nginx
- **Backend**: Go 1.25 with native HTTP server and PostgreSQL driver
- **Database**: PostgreSQL 14.19 with initialization scripts
-
## Features

- Modern HTMX frontend with dynamic UI interactions
- CRUD operations for user management
- RESTful API built with Go's native HTTP package
- PostgreSQL database with automatic schema initialization
- Fully containerized with Docker and Docker Compose
- Health checks and proper service dependencies

## Quick Start

1. **Prerequisites**
   - Docker and Docker Compose installed
   - Ports 3000, 8080, and 5432 available

2. **Run the application**
   ```bash
   docker-compose up --build
   ```

3. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8080
   - Swagger API Docs: http://localhost:8080/swagger/index.html
   - Database: localhost:5432
   - pgAdmin: http://localhost:5050 (Email: admin@admin.com, Password: admin)

## API Endpoints

Interactive API documentation available at http://localhost:8080/swagger/index.html

- `GET /users` - List all users
- `GET /users/{id}` - Get user by ID
- `POST /users` - Create new user
- `PUT /users/{id}` - Update user
- `DELETE /users/{id}` - Delete user
- `GET /health` - Health check
- `GET /swagger/` - Swagger UI

## Development

### Backend Development
```bash
cd backend
go mod tidy
go run main.go
```

To regenerate Swagger docs after API changes:
```bash
cd backend
swag init
```

### Frontend Development
The frontend is a static HTML/HTMX application served by nginx. Simply edit the files in `frontend/static/` and rebuild the container:
```bash
docker-compose up --build frontend
```

### Database Setup
The database is automatically initialized with sample data when the container starts.

### pgAdmin Access
1. Access pgAdmin at http://localhost:5050
2. Login with:
   - Email: `admin@admin.com`
   - Password: `admin`
3. Add a new server with these settings:
   - **General Tab:**
     - Name: `Three Tier App`
   - **Connection Tab:**
     - Host: `database` (or `three-tier-db`)
     - Port: `5432`
     - Database: `app_db`
     - Username: `postgres`
     - Password: `postgres`

## Project Structure

```
three-tier-app/
├── backend/
│   ├── main.go          # Go API server
│   ├── go.mod           # Go dependencies
│   ├── docs/            # Swagger documentation
│   └── Dockerfile       # Backend container
├── frontend/
│   ├── static/
│   │   ├── index.html   # HTMX interface
│   │   └── styles.css   # Styling
│   ├── nginx.conf       # Nginx configuration
│   └── Dockerfile       # Frontend container
├── database/
│   └── init.sql         # Database schema
└── docker-compose.yaml  # Multi-container setup
```

## Technology Stack

### Frontend
- HTMX 1.9 for dynamic interactions
- Modern CSS with responsive design
- Nginx for static file serving
- Gradient-based UI with smooth animations

### Backend
- Go 1.25 with native `net/http` package
- PostgreSQL driver (`lib/pq`)
- RESTful API design
- CORS support
- Environment-based configuration
- Swagger/OpenAPI documentation with interactive UI

### Database
- PostgreSQL 14.19
- Automated schema initialization
- Sample data insertion
- Health checks

## Container Features

- Multi-stage Docker builds for optimized image sizes
- Health checks for all services
- Proper service dependencies
- Volume persistence for database
- Network isolation
