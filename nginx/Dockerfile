# Dockerfile for Nginx
FROM nginx



# Set working directory
WORKDIR /etc/nginx

# Create a volume for Nginx configuration
VOLUME ["/etc/nginx/conf.d"]

# Expose port 80
EXPOSE 80

# Start Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
