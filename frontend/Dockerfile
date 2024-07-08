# Use the official Node.js image as the base image
FROM node:18 AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the Vite application
RUN npm run build

# Print the contents of the dist directory for debugging
RUN ls -la /app/dist

# Use the official Nginx image to serve the build files
FROM nginx:alpine

# Copy the build files from the previous stage to the Nginx web server
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start the Nginx server
CMD ["nginx", "-g", "daemon off;"]
