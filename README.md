mod_perl Docker image
=====================

Docker images for mod_perl.

Built upon [httpd](https://hub.docker.com/_/httpd) and [mod_perl](https://perl.apache.org/).

Tagging strategy
----------------

Docker image tags are formatted as `{perl_version}[-{httpd_version}[-{mod_perl_version}]]` eg. `5.30.0-2.4.39-2.0.11`, `5.30.0-2.4.39`, `5.30.0`.

If any part is omitted, it represents latest version.

For Dockerfiles,

* `perl_version` part corresponds to directories, such as `./5.30.0`.
* `httpd_version` and `mod_perl_version` parts correspond to git tag, such as `2.4.39-2.0.11`.
