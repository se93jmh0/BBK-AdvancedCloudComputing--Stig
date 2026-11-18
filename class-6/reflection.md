### Some Docker Basics

One of the key things to understand when working with Docker is the difference
between an image and a container.  An image is the result of following the
instructions in a Dockerfile; for example, assembling the files that it should
contain, building the environment, and specifying the command to run.

A container, on the other hand, is an instantiation of an image.  Each
container has its own unique id, even if there is more than one created from
the same image.  And anything done within a container, including on the
filesystem, is local to that container.

### About Docker Hub

Docker Hub is Docker-the-company's container registry.  It is the default public
registry used for pulling images using the docker CLI, and it provides a free
(and paid) service for users and organizations to publish their software.

### Docker Volumes

The description of a docker container, in _Some Docker Basics_ above was not
quite correct.  Just like it's possible to mount a device at an arbitrary point
in the filesystem in Linux, it's possible to mount a Docker Volume in a
container's filesystem.  And any changes beneath the mount are stored within
that volume.  This is how its possible to keep changes made to the Courses API
database across different instances of the `week6-courses-api` container image.

### Docker Advantages & Disadvantages

The beauty of docker can be summed up quite succinctly:

    docker run -d -p 80:8000 se93jmh0/week6-courses-api:2

You now have an instance of the CoursesAPI running locally.

