# CERTBOT HTTP 01 Verification Script

## Overview

This project provides a streamlined method for generating certificates with Certbot using HTTP-01 verification on an NGINX web server running on a Linux machine. This approach is especially useful for scenarios where you have access to a server but lack direct access to the DNS provider.

## Key Features

- **Automatic Creation:** Generates an acme-challenge directory in your webroot (typically located at `/var/www/`).

- **NGINX Configuration:** Automatically creates the necessary NGINX server configuration for the acme-challenge.

- **Certificate Generation:** Produces the required SSL/TLS certificates.

## Prerequisites

Before you begin, ensure that you have the following:

- A running NGINX web server.

- An active and valid domain name pointing to your server.

- Certbot version `2.*` installed.

- An empty `/etc/nginx/sites-enabled` directory. (This is optional; if there is a working configuration, you may skip this step, but it’s recommended to clean it up)

- Your current user must have sudo privileges.

## Usage

1. **Run the script**

```bash
# Replace "a.foo.com b.foo.com c.foo.com" with the appropriate subdomain.
# Replace "email@example.com" with the appropriate email that will own the certificates.
curl -s https://raw.githubusercontent.com/aldee07/certbot-scripts/refs/heads/main/http01-verification/acme-generate | sudo bash -s -- -d "a.foo.com b.foo.com c.foo.com" -e "email@example.com"
```

2. **Voila!** Your certificates will be generated in the `/var/www/acme-challenge` directory.

## Next steps

- **Review Configuration:** Check `/etc/nginx/sites-enabled/acme-challenge` to see how to integrate the certificates into your NGINX configuration.

- **Restore Previous Configurations:** If you cleaned up the `/etc/nginx/sites-enabled` folder earlier, you may want to restore any previous configurations and consider deleting the `acme-challenge` configuration.

- **Move Certificates:** Optionally, move the generated certificates to their appropriate locations. Once you’ve done that, you can safely remove the `/var/www/acme-challenge` folder.
