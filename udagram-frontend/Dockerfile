# Build stage
FROM node:16.14.0 AS build-stage

# Cài đặt Ionic CLI
RUN npm install -g @ionic/cli@7.2.0

# Tạo thư mục ứng dụng
WORKDIR /usr/src/app

# Sao chép file package.json và package-lock.json
COPY package*.json ./

# Cài đặt các dependencies
RUN npm ci

# Sao chép toàn bộ mã nguồn ứng dụng
COPY . .

# Build ứng dụng
RUN ionic build

# Run stage
FROM nginx:alpine

# Sao chép các file đã build từ build-stage sang image nginx
COPY --from=build-stage /usr/src/app/www /usr/share/nginx/html

# Expose port 80 để truy cập web
EXPOSE 80

# Chạy Nginx server
CMD ["nginx", "-g", "daemon off;"]