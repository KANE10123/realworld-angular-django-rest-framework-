FROM node:18 as build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm install -g @angular/cli
RUN ng build --configuration production

# Serve stage
FROM nginx:alpine

# Copy only the contents of the browser folder to NGINX root
COPY --from=build /app/dist/frontend /usr/share/nginx/html/

EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]