# syntax = docker/dockerfile:1.2

# Use Node.js for building and serving Next.js
FROM node:18-alpine AS builder

WORKDIR /app

RUN --mount=type=secret,id=_env,dst=./.env

# Copy code and install dependencies
COPY package.json package-lock.json ./
RUN npm install

# Copy source code and build the app
COPY . .
RUN npm run build

# Production image to serve the app
FROM node:18-alpine

WORKDIR /app
COPY --from=builder /app ./
EXPOSE 3000
CMD ["npm", "run", "start"]
