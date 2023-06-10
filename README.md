# Base cent os:7



## Build base image from `Dockerfile`

```shell
docker build -t centos/base:7.1  ./base1
```



## RUN (IMPOTANT RUN IS A LITTLE TRICKY)

1) Base Run Option
```shell
docker run \
    --detach \
    --interactive \
    --tty \
    --publish 21312:22 \
    --tmpfs /tmp:exec \
    --tmpfs /run \
    --volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
    --volume dev_vol1:/home/dev \
    --name dev_centos \
    --hostname localhost \
        centos/base:7.1
```

- 1) `tmpfs` mount option : 
- 2) `cgroup` : because of Linux Isolation problem, docker-centos need to be allocated another system-group
- 3) `publish and port-forwarding` : logicaly isolated from linux system so that  if docker-centos(cgroup) use kernul function, need `tcp-connection with main-system`
- 4) `detach` : recommanded option, after runing container with background, attach bash shell insteed 
- - `docker exec -it dev_centos bash`


2) Instance Run option

```shell

docker run \
    --rm \
    --detach \
    --interactive \
    --tty \
    --publish 22312:22 \
    --tmpfs /tmp:exec \
    --tmpfs /run \
    --volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
    --name dev_centos_ins \
    --hostname localhost \
        centos/base:7.1
```

## Make Snapshot

1) commit running container

```shell
docker commit dev_centos dev_centos_commited1
```

2) Re-Run commited Image

```shell
docker run \
    --detach \
    --interative \
    --tty \
    --publish 22234:22 \
    --name commited_dev \
    --hostname localhost \
        dev_centos_commited1
```

## Attach Bash Shell On running container

```shell
docker exec -it container_name bash
```


## Tip for Dockerfile 

- docker centos have some major & minor issue
- couldn't use `CMD`at last entry point, it is related with [init] and bash

