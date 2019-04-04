# pangeo-stack-onbuild

An example of a binderable repo that uses an ONBUILD enabled PANGEO Stack
image. Our goals is to:

1. Make it possible and easy for user to specify base docker image
2. User should never have to edit Dockerfile nor understand Dockerfile syntax
3. User should be able to customize image with standard files such as
   `environment.yml` or `postBuild` or `requirements.txt`.


This is all accomplished with the [ONBUILD](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#onbuild)
directive.

## The end user's experience

1. User finds what image they wanna use. In this case, it is `yuvipanda/pangeo-base-notebook-onbuild:v1`, but ideally the PANGEO project
   itself would maintain official -onbuild images.
2. The user creates a file with contents `FROM yuvipanda/pangeo-base-notebook-onbuild:v1`, and names this Dockerfile. Nothing else is needed.
3. The user can add `environment.yml` or other such files to the repo
   supported by this particular base image to the repo, and they will
   automatically  be read and respected.


So from the user's perspective, they are specifying which image to use with
the `FROM` directive, but don't need to know anything at all about Docker
or Dockerfiles. Further customizations are done exclusively through the
environment.yml / postBuild mechanisms.

## The image builder's experience

This requires the PANGEO project maintain -onbuild variants for all its
images. This is fairly trivial and mechanistic. See the contents of the
Dockerfile under `base-notebook-onbuild` in this repository to see what
needs to be done. This base image currently supports customization through
environment.yml file and postBuild, but others can be added easily.