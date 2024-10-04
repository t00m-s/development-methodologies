# Use the official Golang image to build the app
FROM golang:latest AS build

# Set the Current Working Directory inside the container
WORKDIR /app

# Copy go mod and sum files
COPY go.mod go.sum ./

# Download all dependencies. Dependencies will be cached if the go.mod and go.sum files are not changed
RUN go mod download

# Copy the source from the current directory to the Working Directory inside the container
COPY . .

# Build the Go app
RUN go build -o main .

# Start a new stage from scratch
FROM alpine:latest

# Set environment variable
ENV GIN_MODE=release

# Expose port 8080 to the outside world
EXPOSE 8080

# Create a directory to store app files
WORKDIR /root/

# Copy the Pre-built binary file from the build stage
COPY --from=build /app/main .

# Command to run the executable
CMD ["./main"]
