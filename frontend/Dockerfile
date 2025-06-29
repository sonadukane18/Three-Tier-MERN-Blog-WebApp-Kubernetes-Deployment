# -------- Stage 1: Build --------
FROM node:21 AS builder

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
COPY .env.docker .env
RUN npm run build

# -------- Stage 2: Serve with Nginx --------
FROM nginx:alpine

# Copy production build files from builder
COPY --from=builder /app/dist /usr/share/nginx/html

# Copy custom nginx config to handle SPA routing
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
