# Base cent os:7



## build

```shell
docker build -t hail/centos:7.1 ./base1
```

## IMPOTANT RUN IS A LITTLE TRICKY

I will explain why all options is needed
bello is base run option for cent os :7

```shell
docker run \
    --detach \
    --interactive \
    --tty \
    --publish 21312:22 \
    --tmpfs /tmp:exec \
    --tmpfs /run \
    --volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
    --volume dev_vol1:/home/hail \
    --name dev_centos \
    --hostname localhost \
        hail/centos:7.1
```

- first, tmpfs is kinds of mound volume inside dockerfile,
- docker centos didn't isolated by system kernul which host server use
- for isolation, needed mount volume and set different kernel group (cgroup)
- publish is most impotant option, if not, your contaienr dead right affer run, your contianer's kernul function like READ BIANRY etc.. is followed by speactial port

- detach container process and set with `docker exec -it dev_centos bash`, some command for develop may excute kernel, so it is more safe stay background your main contaienr process


### instance container option
```shell

docker run \
    --rm \
    --detach \
    --interactive \
    --tty \
    --publish 21312:22 \
    --tmpfs /tmp:exec \
    --tmpfs /run \
    --volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
    --volume dev_vol1:/home/hail \
    --name dev_centos_ins \
    --hostname localhost \
        hail/centos:7.1
```





## Dockerfile guide

- docker centos have some major & minor issue
- couldn't use CMD at last entry point, it is related with [init] and bash

