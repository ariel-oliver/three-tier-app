# Use official Golang image as base
FROM golang:1.25-alpine AS builder

# Set working directory
WORKDIR /app

# Install required packages
RUN apk add --no-cache curl git

# Copy go mod files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Install swag CLI tool for generating Swagger docs
RUN go install github.com/swaggo/swag/cmd/swag@latest

# Copy source code
COPY . .

# Generate Swagger documentation
RUN /go/bin/swag init

# Build the application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

# Use minimal alpine image for final stage
FROM alpine:latest

# Install ca-certificates and curl for health checks
RUN apk --no-cache add ca-certificates curl

WORKDIR /app

# Copy the binary from builder stage
COPY --from=builder /app/main .

# Copy Swagger documentation from builder stage
COPY --from=builder /app/docs ./docs

# Expose port
EXPOSE 8080

# Run the application
CMD ["./main"]