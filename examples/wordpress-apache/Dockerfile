
FROM wordpress:php8.3-apache

# Use an alternative Debian mirror for package downloads.
# Keep security updates on Debian's official security repository.
RUN set -eux; \
    if [ -f /etc/apt/sources.list.d/debian.sources ]; then \
        sed -i \
            -e 's|http://deb.debian.org/debian-security|http://security.debian.org/debian-security|g' \
            -e 's|http://deb.debian.org/debian|http://ftp.fau.de/debian|g' \
            /etc/apt/sources.list.d/debian.sources; \
    fi; \
    apt-get update; \
    rm -rf /var/lib/apt/lists/*
