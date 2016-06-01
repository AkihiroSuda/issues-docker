# How to debug failed `docker build`?

Append `sh -c "$HANDLER"` to handle failures

```dockerfile
FROM alpine:latest
ENV HANDLER 'echo build failed. You can debug this container by running \`docker exec -it THIS_CONTAINER_NAME sh\`. \(available for 1 hour\); sleep 3600'


RUN echo "something good 1 happened" || sh -c "$HANDLER"
RUN echo "something good 2 happened" || sh -c "$HANDLER"
RUN echo "something good 3 happened" || sh -c "$HANDLER"
RUN echo "something bad happend"; false || sh -c "$HANDLER"
```

```
$ docker build -t tmp1 .
Sending build context to Docker daemon 2.048 kB
Step 1 : FROM alpine:latest
 ---> 13e1761bf172
Step 2 : ENV HANDLER 'echo build failed. You can debug this container by running \`docker exec -it THIS_CONTAINER_NAME sh\`. \(available for 1 hour\); sleep 3600'
 ---> Using cache
 ---> 4f0f82d8901f
Step 3 : RUN echo "something good 1 happened" || sh -c "$HANDLER"
 ---> Using cache
 ---> ef3f4c00de1a
Step 4 : RUN echo "something good 2 happened" || sh -c "$HANDLER"
 ---> Using cache
 ---> d699259b0fb3
Step 5 : RUN echo "something good 3 happened" || sh -c "$HANDLER"
 ---> Using cache
 ---> ed6478617762
Step 6 : RUN echo "something bad happend"; false || sh -c "$HANDLER"
 ---> Running in 834cc509987e
something bad happend
build failed. You can debug this container by running `docker exec -it THIS_CONTAINER_NAME sh`. (available for 1 hour)
```
