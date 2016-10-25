# Site Maintenance

This repository provides an example site which works with the S2I builder ``getwarped/s2i-httpd-server`` and displays a maintenance page for all requests made against the site. The HTTP status code returned for all requests will be ``503``. Cache headers will be set to ensure that any response is never cached.

## Deploying the Site

The site can be deployed using the S2I builder by running:

```
oc new-app getwarped/s2i-httpd-server~https://github.com/getwarped/httpd-site-maintenance.git --name site-maintenance
```

Any route for a service which is to under going maintenance can then be switched to ``site-maintenance`` service for the period of the maintenance.