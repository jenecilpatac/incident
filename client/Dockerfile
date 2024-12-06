FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
CMD ["npm", "start"]
FROM nginx:alpine
COPY default.conf /etc/nginx/conf.d/
EXPOSE 5005
CMD ["nginx", "-g", "daemon off;"]