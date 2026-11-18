# Week 6 Homework 1: Docker Practice and Reflection

## Practical Evidence

### Docker Hub

https://hub.docker.com/repository/docker/se93jmh0/week6-courses-api/tags/1/sha256-e24422c00bb2fc1010397fff1acbb8a20f3b4c91fc1e20fc108837363f821f14

### Terminal Output

The `week6-courses-data` image running:

    2026-Nov-17 23:20:28 UTC student@lab-5
    0 115 ~/week6-fastapi-docker
    $ docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api
    27daa368e4b3a99f1523eb5e7944992a6cf6c94805f1e50aed8966c969ce291c se93jmh0/week6-courses-api:1 week6-courses-data → /data

    2026-Nov-17 23:20:31 UTC student@lab-5
    0 116 ~/week6-fastapi-docker
    $ 

The Courses API home:

    2026-Nov-17 23:20:38 UTC student@lab-5
    0 116 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/
    HTTP/1.1 200 OK
    date: Tue, 17 Nov 2026 23:21:00 GMT
    server: uvicorn
    content-length: 35
    content-type: application/json

    {"message":"Courses API version 1"}
    2026-Nov-17 23:21:01 UTC student@lab-5
    0 117 ~/week6-fastapi-docker
    $ 

Adding a new course:

    2026-Nov-17 23:21:07 UTC student@lab-5
    130 117 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses -H "Content-Type: application/json" \
        -d '{ "code": "ACC28", "title": "Advanced Cloud Computing [2028 edition]", "lecturer": "Jeff Dean" }'
    HTTP/1.1 201 Created
    date: Tue, 17 Nov 2026 23:21:25 GMT
    server: uvicorn
    content-length: 96
    content-type: application/json

    {"code":"ACC28","title":"Advanced Cloud Computing [2028 edition]","lecturer":"Jeff Dean","id":3}
    2026-Nov-17 23:21:25 UTC student@lab-5
    0 118 ~/week6-fastapi-docker
    $ 

Adding another course with the same code:

    2026-Nov-17 23:21:25 UTC student@lab-5
    0 118 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses -H "Content-Type: application/json" \
        -d '{ "code": "ACC28", "title": "ACC", "lecturer": "JD" }'
    HTTP/1.1 409 Conflict
    date: Tue, 17 Nov 2026 23:22:57 GMT
    server: uvicorn
    content-length: 39
    content-type: application/json

    {"detail":"Course code already exists"}
    2026-Nov-17 23:22:57 UTC student@lab-5
    0 119 ~/week6-fastapi-docker
    $ 

Adding a course with a code that is too short:

    2026-Nov-17 23:22:57 UTC student@lab-5
    0 119 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses -H "Content-Type: application/json" \
        -d '{ "code": "X", "title": "ACC", "lecturer": "JD" }'
    HTTP/1.1 422 Unprocessable Entity
    date: Tue, 17 Nov 2026 23:24:20 GMT
    server: uvicorn
    content-length: 146
    content-type: application/json

    {"detail":[{"type":"string_too_short","loc":["body","code"],"msg":"String should have at least 2 characters","input":"X","ctx":{"min_length":2}}]}
    2026-Nov-17 23:24:21 UTC student@lab-5
    0 120 ~/week6-fastapi-docker
    $ 

Retrieving an unknown course:

    2026-Nov-17 23:24:21 UTC student@lab-5
    0 120 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses/100
    HTTP/1.1 404 Not Found
    date: Tue, 17 Nov 2026 23:24:56 GMT
    server: uvicorn
    content-length: 29
    content-type: application/json

    {"detail":"Course not found"}
    2026-Nov-17 23:24:56 UTC student@lab-5
    0 121 ~/week6-fastapi-docker
    $ 

Retrieving the previously-created course:

    2026-Nov-17 23:24:56 UTC student@lab-5
    0 121 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses/3
    HTTP/1.1 200 OK
    date: Tue, 17 Nov 2026 23:25:38 GMT
    server: uvicorn
    content-length: 96
    content-type: application/json

    {"code":"ACC28","title":"Advanced Cloud Computing [2028 edition]","lecturer":"Jeff Dean","id":3}
    2026-Nov-17 23:25:38 UTC student@lab-5
    0 122 ~/week6-fastapi-docker
    $ 

Replacing the container:

    2026-Nov-17 23:25:43 UTC student@lab-5
    130 122 ~/week6-fastapi-docker
    $ docker stop courses-api && docker rm courses-api && \
        docker run -d --name courses-api -p 80:8000 --env-file .env \
            --mount type=volume,source=week6-courses-data,target=/data \
            se93jmh0/week6-courses-api:1
    courses-api
    courses-api
    b43d1336fb419521e99ea4c80738c338ae85550b546691021a5b5ac51d063c9e

    2026-Nov-17 23:26:17 UTC student@lab-5
    0 123 ~/week6-fastapi-docker
    $ docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api
    b43d1336fb419521e99ea4c80738c338ae85550b546691021a5b5ac51d063c9e se93jmh0/week6-courses-api:1 week6-courses-data → /data

    2026-Nov-17 23:26:36 UTC student@lab-5
    0 124 ~/week6-fastapi-docker
    $ 

Re-Retrieving the previously-created course:

    2026-Nov-17 23:26:36 UTC student@lab-5
    0 124 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses/3
    HTTP/1.1 200 OK
    date: Tue, 17 Nov 2026 23:28:48 GMT
    server: uvicorn
    content-length: 96
    content-type: application/json

    {"code":"ACC28","title":"Advanced Cloud Computing [2028 edition]","lecturer":"Jeff Dean","id":3}
    2026-Nov-17 23:28:49 UTC student@lab-5
    0 125 ~/week6-fastapi-docker
    $ 

### Migrate to Version 2

https://hub.docker.com/repository/docker/se93jmh0/week6-courses-api/tags/2/sha256-1ddb869ae67aa9fd0bebb98200b0901c233b5dbbe67740e4928f41fe783c8b66

    2026-Nov-17 23:28:49 UTC student@lab-5
    0 125 ~/week6-fastapi-docker
    $ docker stop courses-api && docker rm courses-api && \
        docker run -d --name courses-api -p 80:8000 --env-file .env \
            --mount type=volume,source=week6-courses-data,target=/data \
            se93jmh0/week6-courses-api:2
    courses-api
    courses-api
    Unable to find image 'se93jmh0/week6-courses-api:2' locally
    2: Pulling from se93jmh0/week6-courses-api
    4822b4f28fd6: Pull complete 
    Digest: sha256:1ddb869ae67aa9fd0bebb98200b0901c233b5dbbe67740e4928f41fe783c8b66
    Status: Downloaded newer image for se93jmh0/week6-courses-api:2
    90e9499d573fc7467b12f7f742ae6ffa099c983074dcf76761f6d87a4da1334c

    2026-Nov-17 23:32:08 UTC student@lab-5
    0 126 ~/week6-fastapi-docker
    $ 

The `week6-courses-data` version 2 image running:

    2026-Nov-17 23:32:08 UTC student@lab-5
    0 126 ~/week6-fastapi-docker
    $ docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api
    90e9499d573fc7467b12f7f742ae6ffa099c983074dcf76761f6d87a4da1334c se93jmh0/week6-courses-api:2 week6-courses-data → /data

    2026-Nov-17 23:33:28 UTC student@lab-5
    0 127 ~/week6-fastapi-docker
    $ 

The modified Courses API home:

    2026-Nov-17 23:33:34 UTC student@lab-5
    130 127 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/
    HTTP/1.1 200 OK
    date: Tue, 17 Nov 2026 23:34:21 GMT
    server: uvicorn
    content-length: 35
    content-type: application/json

    {"message":"Courses API version 2"}
    2026-Nov-17 23:34:21 UTC student@lab-5
    0 128 ~/week6-fastapi-docker
    $ 

...and the previously-created course persists!:

    2026-Nov-17 23:34:21 UTC student@lab-5
    0 128 ~/week6-fastapi-docker
    $ curl -i http://34.56.85.72/courses/3
    HTTP/1.1 200 OK
    date: Tue, 17 Nov 2026 23:34:45 GMT
    server: uvicorn
    content-length: 96
    content-type: application/json

    {"code":"ACC28","title":"Advanced Cloud Computing [2028 edition]","lecturer":"Jeff Dean","id":3}
    2026-Nov-17 23:34:46 UTC student@lab-5
    0 129 ~/week6-fastapi-docker
    $ 


## Reflection

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
(or paid) service for users and organizations to publish their software.

One of the important things to be aware of when using a registry like Docker
Hub, however, is the difference between referring to an image by its digest, and
referring to an image by tag.  An image's digest is basically a hash, and so it
uniquely identifies a version of an image.  A tag, on the other hand, can be
updated to point at any version.  Therefore the safest thing to do when
specifying dependencies is to use the digest to avoid supply chain attacks.

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

You now have an instance of the CoursesAPI running locally, which is a boon for
simple deployment in Cloud environments.

One issue I have noticed, with the CLI at least, is that when running a
container with a volume, the volume will be silently created if it does not
already exist.  This means it's easy to accidentally run against the wrong
(probably blank) database and be puzzled why your tests are not working.

Not that that happened to me, of course.  O&:)
