# Use official Ubuntu image

FROM ubuntu:24.04

# Install dependencies
RUN apt-get update && \
    apt-get install -y software-properties-common curl zip unzip git && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y php8.4 php8.4-cli php8.4-fpm php8.4-common php8.4-mbstring php8.4-xml php8.4-zip php8.4-gd php8.4-curl php8.4-mysql php8.4-pgsql php8.4-redis php8.4-tokenizer php8.4-bcmath php8.4-ctype php8.4-fileinfo php8.4-pdo php8.4-imagick && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install additional libraries for PDF and Excel processing and PostgreSQL client
RUN apt-get update && \
    apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev libzip-dev libonig-dev libxml2-dev libpq-dev postgresql-client nginx && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY --from=composer:2.8.10 /usr/bin/composer /usr/bin/composer

# Expose port 80 for nginx
EXPOSE 80

# Expose port 9000 for PHP-FPM
EXPOSE 9000

# Create startup script
RUN echo '#!/bin/bash\n\
service php8.4-fpm start\n\
nginx -g "daemon off;"' > /start.sh && chmod +x /start.sh

# Default command to start both PHP-FPM and nginx
CMD ["/start.sh"]
