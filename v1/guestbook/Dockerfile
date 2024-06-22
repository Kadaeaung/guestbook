# Stage 1: Build the Go application
FROM golang:1.18 as builder

# Set the working directory inside the container
WORKDIR /app

# Copy go.mod and go.sum files
COPY go.mod go.sum ./

# Download dependencies
RUN go mod download

# Copy the Go source code
COPY main.go .

# Build the Go application
RUN go build -o guestbook main.go

# Stage 2: Create the final image
FROM ubuntu:18.04

# Copy the built Go binary from the builder stage
COPY --from=builder /app/guestbook /app/guestbook

# Copy static files
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

# Set the working directory
WORKDIR /app

# Define the command to run the application
CMD ["./guestbook"]

# Expose the application port
EXPOSE 3000
