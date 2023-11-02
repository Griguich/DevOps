# Use a base image with Node.js and Alpine Linux
FROM node:14-alpine

# Set the working directory within the container
WORKDIR /app

# Copy the Angular application source code to the container
COPY . .

# Install Angular CLI globally (optional, if not already installed)
RUN npm install -g @angular/cli

# Install dependencies and build the Angular app
RUN npm install
RUN ng build --prod

# Expose the port your Angular app will run on (e.g., 80)
EXPOSE 80

# Command to serve the Angular app
CMD ["nginx", "-g", "daemon off;"]