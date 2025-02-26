FROM ubuntu:latest

# Update package list and install Nginx
RUN apt-get update && apt-get install -y nginx

# Remove the default Nginx HTML files
RUN rm -rf /var/www/html/*

# Copy your custom website files
COPY myapp /var/www/html/

# Expose port 8281
EXPOSE 8281

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
