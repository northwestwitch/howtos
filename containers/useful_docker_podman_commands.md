# Useful docker and podman commands
## Show containers
```
podman ps
```

## Remove all containers
```
podman rm -f $(podman ps -aq)
```

## Show images
```
podman images
```
```
podman image ls
```

## Remove all images
```
podman image rm -f $(podman images -aq)
```

## Remove everything:
```
podman system prune
```
This is is especially good when you run out of memory
