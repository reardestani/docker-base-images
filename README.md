# Docker Base Images

Reusable Docker build configurations and examples for projects deployed with Coolify.

This repository focuses on reusable build patterns rather than one universal runtime image.

## Examples

- `examples/wordpress-apache/` — WordPress with Apache.
- `snippets/` — reusable Docker build snippets.

## Debian APT Mirror Workaround

Some network routes may have trouble reaching `deb.debian.org`.

A workaround tested successfully in a disposable Debian Trixie container:

- Main packages and updates: `http://ftp.fau.de/debian`
- Security packages: `http://security.debian.org/debian-security`

For Debian Trixie images, use this before installing packages:

```dockerfile
RUN set -eux; \
    sed -i \
        -e 's|http://deb.debian.org/debian-security|http://security.debian.org/debian-security|g' \
        -e 's|http://deb.debian.org/debian|http://ftp.fau.de/debian|g' \
        /etc/apt/sources.list.d/debian.sources; \
    apt-get update
```

**Important:** This workaround was tested with Debian Trixie. Other Debian releases may use different APT source configurations.

## Coolify Deployment

1. Push the project to GitHub.
2. Create an application in Coolify.
3. Select the Dockerfile build pack.
4. Configure the Dockerfile location and domain.
5. Configure persistent storage and databases separately where needed.

## Principles

- Prefer official upstream runtime images.
- Keep application-specific dependencies in each project's Dockerfile.
- Use Docker Compose for applications requiring multiple services.
- Avoid maintaining custom runtime images without a clear benefit.