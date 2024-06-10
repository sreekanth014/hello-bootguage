# Use the official Golang image to create a build artifact.
FROM golang:1.18-alpine AS build

# Set the working directory inside the container.
WORKDIR /app

# Copy the Go module files first.
COPY go.mod ./
COPY go.sum ./

# Download dependencies.
RUN go mod download

# Copy the rest of the Go source code to the working directory.
COPY . .

# Build the Go application.
RUN go build -o hello-botgauge

# Use a minimal Docker image to run the application.
FROM alpine:latest

# Set the working directory inside the container.
WORKDIR /root/

# Copy the binary from the build stage to the final stage.
COPY --from=build /app/hello-botgauge .

# Expose port 8080.
EXPOSE 8080

# Command to run the application.
CMD ["./hello-botgauge"]

