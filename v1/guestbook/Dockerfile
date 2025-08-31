# ---- Build stage ----
    FROM golang:1.18 AS builder

    WORKDIR /app
    COPY main.go .
    RUN go mod init guestbook
    RUN go mod tidy
    RUN go build -o main main.go
    
    # ---- Runtime stage ----
    FROM ubuntu:18.04
    
    # bring the compiled binary from the builder stage
    COPY --from=builder /app/main /app/guestbook
    
    # bring static assets
    COPY public/index.html     /app/public/index.html
    COPY public/script.js      /app/public/script.js
    COPY public/style.css      /app/public/style.css
    COPY public/jquery.min.js  /app/public/jquery.min.js
    
    WORKDIR /app
    EXPOSE 3000
    CMD ["./guestbook"]
    