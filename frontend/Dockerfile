# Stage 1: Build the React app
FROM node:20.9.0-alpine AS builder

WORKDIR /usr/src/app

RUN npm install -g npm@10.2.4

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder /usr/src/app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
