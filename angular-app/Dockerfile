# Use a stable Node.js version for building the app
FROM node:18 AS build

WORKDIR /app

# Copy package.json and package-lock.json first to leverage Docker caching
COPY package*.json ./
RUN npm install

# Copy the rest of the application
COPY . .

# Build the Angular application
RUN npm run build -- --configuration production

# Use NGINX to serve the Angular application
FROM nginx:alpine

# Copy the built files from the previous stage
COPY --from=build /app/dist/angular-app /usr/share/nginx/html

# Expose port 80 for the web server
EXPOSE 80

# Command to run NGINX
CMD ["nginx", "-g", "daemon off;"]
