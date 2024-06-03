# A und B

## A

```
# Bind Mounts:
# -v or --volume: Consists of three fields, separated by colon characters (:)
# In the case of bind mounts, the first field is the path to the file or directory on the host machine.
# The second field is the path where the file or directory is mounted in the container.
# The third field is optional, and is a comma-separated list of options, such as ro, z, and Z.

# The biggest difference is that the -v syntax combines all the options together in one field, while the --mount syntax separates them

docker run -v /Users/vanessenjonas/Documents/workspace-tbz/modules/m347/loesungen/kn05/A/localMount:/mnt/kn05 -d nginx
docker volume ls

```

## B
```
# Volumen:
# -v or --volume: Consists of three fields, separated by colon characters (:). 
# the first field is the name of the volume, and is unique on a given host machine. For anonymous volumes, the first field is omitted.
# The second field is the path where the file or directory are mounted in the container.
# The third field is optional, and is a comma-separated list of options, such as ro. 


docker run -v myVol:/mnt/myVol -d nginx
docker run -v myVol:/mnt/myVol -d nginx

# tmpfs Mounts:
# As opposed to volumes and bind mounts, a tmpfs mount is temporary, and only persisted in the host memory. 
# When the container stops, the tmpfs mount is removed, and files written there won't be persisted.


docker run --tmpfs /data3 --name web4 -d nginx
docker exec -it web4 /bin/bash

# all together
docker run --tmpfs /data3 -v myVol:/data1 -v C:\tmp:/data2 --name web5 -d nginx
docker exec -it web5 /bin/bash

# Falls -mount Option verwendet wird
# ==========================================
# --mount: Consists of multiple key-value pairs, separated by commas and each consisting of a <key>=<value> tuple.
# type=<>: The type of the mount, which can be bind, volume, or tmpfs. This topic discusses volumes, so the type is always volume.
# source=<>: The source of the mount. For named volumes, this is the name of the volume. For anonymous volumes, this field is omitted. Can be specified as source or src.
# destination=<>: The destination takes as its value the path where the file or directory is mounted in the container. Can be specified as destination, dst, or target.
# readonly=<>: The readonly option, if present, causes the bind mount to be mounted into the container as read-only. Can be specified as readonly or ro.
# volume-opt=<>: The volume-opt option, which can be specified more than once, takes a key-value pair consisting of the option name and its value.
docker run --mount source=myvol2,target=/data1 --mount type=bind,source=C:\tmp,target=/data2 --mount type=tmpfs,destination=/data3 --name web6 -d nginx
docker exec -it web6 /bin/bash

```

# C

Siehe [compose.yml](compose.yaml)
