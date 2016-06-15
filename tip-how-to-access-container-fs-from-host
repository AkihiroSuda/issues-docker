# How to access a container's filesystem from the host

```
$ sudo ls /proc/$(docker inspect -f '{{.State.Pid}}' $containerid)/root/
```

This seems working well with volumes
