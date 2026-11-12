# Nginx for buildable Moodle on Wodby

The web server of the [buildable Moodle](https://github.com/wodby/service-moodle-buildable) service. It is the
[php-nginx](https://github.com/wodby/service-php-nginx) service with Moodle's rules.

## Image

The image is built on `wodby/nginx` from the same build directory as the Moodle image, after the pipeline's
`moodle-install-release` has put Moodle and the repository's plugins together. Only Moodle's `public/` directory goes
into the image, at `/var/www/html/public`, the same path as in the Moodle image, so Nginx serves the plugins' static
files itself and passes PHP scripts to the Moodle service (`backend` link).

## Rules

The `preset` config replaces the image's PHP preset with the rules of the prebuilt Moodle Nginx image:

- requests for paths that are not files go to Moodle's router, `r.php`;
- PHP scripts with slash arguments, such as `/pluginfile.php/12/...`, reach PHP-FPM with their path info;
- Composer files, `vendor/`, readmes, upgrade notes, test fixtures and lock files are never served;
- static files are cached by browsers for a year.

Uploads and form posts are limited to 256 MB (`NGINX_CLIENT_MAX_BODY_SIZE`), matching the Moodle service.
