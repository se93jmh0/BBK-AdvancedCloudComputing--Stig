# Thing

## Other thing


Include a link to your Docker Hub repository, the explicit versioned image reference, and its registry digest.

Docker Hub repo: https://hub.docker.com/repository/docker/se93jmh0/week6-courses-api/general
se93jmh0/week6-courses-api:1
https://hub.docker.com/repository/docker/se93jmh0/week6-courses-api/tags/1/sha256-e24422c00bb2fc1010397fff1acbb8a20f3b4c91fc1e20fc108837363f821f14


docker stop courses-api
docker rm courses-api
docker image rm se93jmh0/week6-courses-api:1
docker image rm se93jmh0/week6-courses-api:2

docker run -d --name courses-api -p 80:8000 --env-file .env \
    --mount type=volume,source=week6-courses-data,target=/data \
    se93jmh0/week6-courses-api:1

docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api


The week6-courses-data image running:

2026-Nov-17 23:20:28 UTC student@lab-5
0 115 ~/week6-fastapi-docker
$ docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api
27daa368e4b3a99f1523eb5e7944992a6cf6c94805f1e50aed8966c969ce291c se93jmh0/week6-courses-api:1 week6-courses-data → /data

2026-Nov-17 23:20:31 UTC student@lab-5
0 116 ~/week6-fastapi-docker
$ 

### Here's the Courses API home:

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

### Here's adding 

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

Duplicate:

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

Invalid:

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

Missing:

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

Retrieval before:

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

# Replace

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

After

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

-> 2:

se93jmh0/week6-courses-api:2
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

Image running:

2026-Nov-17 23:32:08 UTC student@lab-5
0 126 ~/week6-fastapi-docker
$ docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api
90e9499d573fc7467b12f7f742ae6ffa099c983074dcf76761f6d87a4da1334c se93jmh0/week6-courses-api:2 week6-courses-data → /data

2026-Nov-17 23:33:28 UTC student@lab-5
0 127 ~/week6-fastapi-docker
$ 

Changed home:

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

New course still there:

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

docker stop courses-api && docker rm courses-api && \
    docker run -d --name courses-api -p 80:8000 --env-file .env \
        --mount type=volume,source=week6-courses-data,target=/data \
        se93jmh0/week6-courses-api:1

curl -i http://34.56.85.72/
curl -i http://34.56.85.72/courses -H "Content-Type: application/json" \
    -d '{ "code": "ACC28", "title": "Advanced Cloud Computing [2028 edition]", "lecturer": "Jeff Dean" }'
curl -i http://34.56.85.72/courses -H "Content-Type: application/json" \
    -d '{ "code": "ACC28", "title": "ACC", "lecturer": "JD" }'
curl -i http://34.56.85.72/courses -H "Content-Type: application/json" \
    -d '{ "code": "X", "title": "ACC", "lecturer": "JD" }'
curl -i http://34.56.85.72/courses/100

curl -i http://34.56.85.72/courses/3



docker stop courses-api && docker rm courses-api && \
    docker run -d --name courses-api -p 80:8000 --env-file .env \
        --mount type=volume,source=week6-courses-data,target=/data \
        se93jmh0/week6-courses-api:2

docker inspect --format '{{.Id}} {{.Config.Image}}{{range .Mounts}} {{.Name}} → {{.Destination}}{{end}}' courses-api

curl -i http://34.56.85.72/

#### Practice README

Add a short `README.md` to your `week6-fastapi-docker` project. Include:

- What the practice API does and the required software.
- Commands to build, tag, publish, pull and run the image.
- Your Docker Hub image reference and digest.
- The runtime database setting and the named volume mounted at `/data`.
- How to test the API, replace its container while preserving the database, and clean up afterwards.

Keep the Dockerfile, `.dockerignore`, pinned dependency file and `.env.example` with your practice project. Check that the image excludes database files and real `.env` files. Your example configuration must use placeholders for any secrets. Share the practice repository link or attach the README for feedback; do not upload the database or your assessed Piazza implementation to Teams.

#### Reflection: 150–200 Words

Explain in your own words:

- The difference between an image and a container.
- How Docker Hub helps another machine obtain your packaged API, and how a version tag differs from a registry digest.
- Why your SQLite file belongs in a volume and what happened to your record when you replaced the container.
- One reason Docker helps with cloud deployment and one limitation or problem you observed.

The README, image reference, captions and evidence are separate from the reflection's word count.

#### Before You Finish

Collect evidence before cleanup. Follow the [lab cleanup steps](../lab/part-3.md#cleanup), keeping the named volume until your persistence check is complete. Stop `lab-5` when finished and keep its disk for later labs.

Do not share passwords, tokens, real secrets, `.env` files or database files in Teams, screenshots, public images or repositories. Keep `.env.example` safe to share.
