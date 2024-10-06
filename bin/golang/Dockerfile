# Step 1: Build the Go app
FROM golang:1.22 AS builder

WORKDIR /app

# Copy go mod and sum files
COPY www/api/v3/go-crud/go.mod www/api/v3/go-crud/go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source from the current directory to the Working Directory inside the container
COPY www/api/v3/go-crud ./

# Copy the .env file to the working directory
COPY .env .env

# Build the Go app statically
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

# Step 2: Create a smaller image for running the Go app
FROM alpine:latest

WORKDIR /root/

# Copy the Pre-built binary file and .env file from the previous stage
COPY --from=builder /app/main .
COPY --from=builder /app/.env .env

# Install necessary tools for debugging (optional)
RUN apk add --no-cache bash tzdata

# Command to run the executable
CMD ["./main"]
