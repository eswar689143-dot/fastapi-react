# 1) Build stage
FROM node:20 AS build

WORKDIR /app

# copy package and install
COPY package*.json ./

RUN npm ci

RUN npm install


# copy source
COPY . .

# build for production
RUN npm run build

# ----------------------------

# 2) Serve stage
FROM nginx:stable-alpine

# Copy built static files
COPY --from=build /app/dist /usr/share/nginx/html

# Expose nginx port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
