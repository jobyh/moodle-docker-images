# Docker Image Scripts

Build scripts Efor Docker images which can be used in combination
with `docker-compose` and other containers of your choosing to create
custom local environments ready to run Moodle.

Please note **the built images will not include Moodle**. The `Dockerfile`s
are my own builds and intended to work in conjunction with a locally checked
out Moodle or Totara Learn repository. Organising here is a WIP so for details
on the volumes you should mount please check out the corresponding `Dockerfile`.
At present the builds also contain configurations specific to my own needs such
as setting the current timezone locale to London or the Xdebug IDE key for PHPStorm.
