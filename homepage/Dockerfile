FROM nginx:stable-alpine

# Remove default site config
RUN rm /etc/nginx/conf.d/default.conf

# Copy your Nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Copy static content
COPY html/ /usr/share/nginx/html/

# Expose port 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

