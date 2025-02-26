# Use the official Node.js image
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy package.json (if exists)
COPY package.json ./

# Install dependencies (optional, for future scalability)
RUN npm install || true

# Copy all files into the container
COPY . .

# Expose port 3000
EXPOSE 3000

# Command to start the app
CMD ["node", "index.js"]
