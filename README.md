# Nginx service for buildable Moodle on Wodby

The web server for [buildable Moodle](https://github.com/wodby/service-moodle-buildable)
on Kubernetes with Wodby: Nginx with Moodle's rules, built from the same code
as the Moodle image, so it serves your plugins' and themes' files.

- [Browse Wodby services](https://wodby.com/services)
- [Wodby service documentation](https://wodby.com/docs/2.0/services/)
- [Service manifest reference](https://wodby.com/docs/2.0/services/template/)

## Service overview

| Property | Manifest configuration |
| --- | --- |
| Service name | `moodle-buildable-nginx` |
| Based on | [`php-nginx`](https://github.com/wodby/service-php-nginx) |
| Type | Web server |
| Image | Moodle's `public/` directory from the app's build on top of `wodby/nginx` |
| Configuration | Moodle's Nginx rules in `preset.conf.tmpl` |
| Links | `backend`: the buildable Moodle service |

For the prebuilt Moodle stack, use the [Moodle Nginx service](https://github.com/wodby/service-moodle-nginx) instead.

## Maintain a custom version

1. Fork this repository.
2. Edit the service manifest and referenced files.
3. Import the repository as a [Git-backed service](https://wodby.com/docs/2.0/services/create/#create-a-git-backed-service).
4. Reference the service from a stack manifest.

Validate the manifest with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```
