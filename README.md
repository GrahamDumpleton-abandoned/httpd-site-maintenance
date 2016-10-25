# Site Maintenance

This repository provides an example site which works with the S2I builder ``getwarped/s2i-httpd-server`` and displays a maintenance page for all requests made against the site. The HTTP status code returned for all requests will be ``503``. Cache headers will be set to ensure that any response is never cached.

## Deploying the Site

The site can be deployed using the S2I builder by running:

```
oc new-app getwarped/s2i-httpd-server~https://github.com/getwarped/httpd-site-maintenance.git --name site-maintenance
```

## Switching Traffic

Once the service is running, any route for a service which is to under go maintenance can then be switched to the ``site-maintenance`` service for the period of the maintenance. This can be done using the command:

```
oc set route-backends mysite site-maintenance=100
```

The name ``mysite`` should be substituted with the ``route`` name of the web application.

When done with maintenance on the site, traffic can be switched back using the command:

```
oc set route-backends mysite mysite=100
```

The first occurrence of ``mysite`` is again the ``route`` name of the web application. The second occurrence is the ``service`` name of the web application. Under normal circumstances these would be the same name.