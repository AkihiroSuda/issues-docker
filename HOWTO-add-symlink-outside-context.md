You can't `ADD` a symlink of which destination is outside of the build context directory.

This can be a problem for a project like this:
```
proj/
proj/app-main/
proj/example/ex01/Dockerfile <-- this depends on ../../app-main
proj/example/ex02/Dockerfile <-- ditto
```

Workaround:
```
$ tar -czh . | docker build -
```


links: 
- http://superuser.com/questions/842642/how-to-make-a-symlinked-folder-appear-as-a-normal-folder
- https://github.com/docker/docker/issues/1676
