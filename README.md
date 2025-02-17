# secure-redirect
🔒 Apache .htaccess configuration to enforce HTTPS redirects. Includes code for standard setups and proxies (e.g., Cloudflare).

```markdown
# .htaccess Files for Various Website Configurations

This repository contains `.htaccess` configurations for different website functionalities. Below you'll find examples for redirecting HTTP to HTTPS, optimizing site performance, handling redirects, and more.

## Table of Contents
- [HTTP to HTTPS Redirection](#http-to-https-redirection)
- [Custom Error Pages](#custom-error-pages)
- [Caching and Compression](#caching-and-compression)
- [URL Rewriting](#url-rewriting)
- [Blocking Access to Specific Files](#blocking-access-to-specific-files)

## HTTP to HTTPS Redirection

To ensure that all traffic to your website is served over HTTPS, you can use the following `.htaccess` configuration:

```apache
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

- **Explanation**: 
  - `RewriteCond %{HTTPS} off`: This checks if the request is not using HTTPS.
  - `RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]`: Redirects to the HTTPS version of the same URL.
  - The `301` code means it's a permanent redirect.

## Custom Error Pages

To create custom error pages for your website (e.g., 404 Not Found, 500 Internal Server Error), add the following to your `.htaccess` file:

```apache
ErrorDocument 404 /error-pages/404.html
ErrorDocument 500 /error-pages/500.html
ErrorDocument 403 /error-pages/403.html
```

- **Explanation**: This configuration redirects specific error codes to custom HTML error pages located in the `/error-pages/` directory.

## Caching and Compression

To enhance your website's performance, you can enable caching and compression:

```apache
# Enable GZIP Compression
<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css application/x-javascript application/javascript
</IfModule>

# Leverage Browser Caching
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresDefault "access plus 1 year"
    ExpiresByType image/jpeg "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
</IfModule>
```

- **Explanation**:
  - `mod_deflate`: Compresses content sent to the browser to reduce load times.
  - `mod_expires`: Caches content for a specific period, reducing server load and speeding up load times.

## URL Rewriting

To remove `.php` extensions from URLs or to create pretty URLs, use the following rewrite rules:

```apache
RewriteEngine On
RewriteRule ^([^/]+)$ $1.php [L]
```

- **Explanation**: This rule rewrites URLs to point to the corresponding PHP file without showing the `.php` extension.

## Blocking Access to Specific Files

If you want to prevent access to certain files or directories, you can use the following directives:

```apache
# Block access to .env file
<Files .env>
    Order Allow,Deny
    Deny from all
</Files>

# Block access to wp-config.php
<Files wp-config.php>
    Order Allow,Deny
    Deny from all
</Files>
```

- **Explanation**: These rules block access to sensitive files such as `.env` and `wp-config.php`.

## How to Use

1. Copy the desired configuration to your `.htaccess` file.
2. Upload the `.htaccess` file to the root directory of your website.
3. Make sure that your server is running Apache and that the `mod_rewrite` and other required modules are enabled.

## Notes
- Be cautious when editing your `.htaccess` file, as incorrect settings can break your website.
- Always back up your `.htaccess` file before making changes.

## License

This repository is licensed under the MIT License. See `LICENSE` for more information.
