# 構建階段
FROM node:18-alpine as build

# 設置工作目錄
WORKDIR /app

# 複製 package.json 和 package-lock.json
COPY package*.json ./

# 清除 npm 快取並安裝依賴
RUN npm cache clean --force && \
    npm install --legacy-peer-deps

# 複製所有源代碼
COPY . ./

# 構建應用
RUN npm run build

# 生產階段
FROM nginx:alpine

# 複製構建文件到 Nginx 服務目錄
COPY --from=build /app/build /usr/share/nginx/html

# 複製 Nginx 配置文件
COPY nginx.conf /etc/nginx/conf.d/default.conf

# 暴露端口
EXPOSE 80

# 啟動 Nginx
CMD ["nginx", "-g", "daemon off;"] 