# Use a Debian-based image with Apache and PHP 8 installed
FROM php:8.0-apache-buster

# Metadata
LABEL org.opencontainers.image.title="HRConvert2" \
      org.opencontainers.image.description="A web-interface for converting file formats on a server" \
      org.opencontainers.image.authors="Justin Grimes <www.github.com/zelon88>" \
      org.opencontainers.image.licenses="GPL-3.0-or-later"

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libreoffice \
    libreoffice-java-common \
    unoconv \
    clamav \
    tesseract-ocr \
    rar \
    unrar \
    p7zip-rar \
    ffmpeg \
    imagemagick \
    meshlab \
    dia \
    pandoc \
    mkisofs \
    poppler-utils \
    nodejs \
    gnuplot \
    tar \
    default-jre \
    zip \
    gd \
    && rm -rf /var/lib/apt/lists/*

# Enable Apache mods
RUN a2enmod rewrite

# Update the PHP ini file, enable required extensions
RUN { \
        echo 'max_execution_time=90'; \
        echo 'max_input_time=90'; \
        echo 'memory_limit=512M'; \
        echo 'display_errors=On'; \
        echo 'post_max_size=3000M'; \
        echo 'upload_max_filesize=3000M'; \
        echo 'max_file_uploads=100'; \
        echo 'zlib.output_compression=On'; \
    } > /usr/local/etc/php/conf.d/hrconvert2.ini

# Copy HRConvert2 application files
COPY . /var/www/html/

# Adjust permissions to allow Apache to serve the app
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

# Expose port 80
EXPOSE 80

# Launch Apache in the foreground
CMD ["apache2-foreground"]
