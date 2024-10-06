# Use the official NGINX image as the base image
FROM nginx:alpine

# Copy the build output to the NGINX html directory
COPY heweb-app/browser /usr/share/nginx/html

# Copy a default Nginx configuration
COPY nginx.conf /etc/nginx/conf.d/nginx.conf

# Expose port 80
EXPOSE 80

# Start NGINX when the container starts
CMD ["nginx", "-g", "daemon off;"]
