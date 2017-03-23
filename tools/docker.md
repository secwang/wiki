---
title: "docker"
date: 2016-06-30 23:00
---
[TOC]


Install docker
==============
## Linux
[install docker on centos](https://docs.docker.com/engine/installation/linux/centos/)
[docker boost](https://cr.console.aliyun.com/#/docker/booster)
```
sudo yum install docker
sudo systemctl enable docker
sudo systemctl start docker
sudo docker run rickfast/hello-oreilly

# add user with docker group
useradd deploy 
passwd deploy
# add docker group
sudo groupadd docker
sudo usermod -aG docker deploy 


```

## Mac OS X


# docker run options

```
   -d, --detach=true|false
          Detached mode: run the container in the background and print the new
       container ID. The default is false.

       At any time you can run docker ps in the other shell to view a list  of
       the  running  containers. You can reattach to a detached container with
       docker attach. If you choose to run a container in the  detached  mode,
       then you cannot use the -rm option.

       When  attached  in the tty mode, you can detach from the container (and
       leave it running)  using  a  configurable  key  sequence.  The  default
       sequence  is  CTRL-p  CTRL-q.  You configure the key sequence using the
       --detach-keys option or a configuration file.  See  config-json(5)  for
       documentation on using a configuration file.

   -i, --interactive=true|false
      Keep STDIN open even if not attached. The default is false.

       When set to true, keep stdin open even if not attached. The default  is
       false.


    -t, --tty=true|false
          Allocate a pseudo-TTY. The default is false.

       When  set  to  true  Docker can allocate a pseudo-tty and attach to the
       standard input of any container. This can be used, for example, to  run
       a throwaway interactive shell. The default is false.

       The  -t  option is incompatible with a redirection of the docker client
       standard input.
    --name=""
          Assign a name to the container

       The operator can identify a container in three ways:
           UUID                        long                         identifier
       (“f78375b1c487e03c9438c729345e54db9d20cfa2ac1fc3494b6eb60872e74778”)
           UUID short identifier (“f78375b1c487”)
           Name (“jonah”)

       The  UUID identifiers come from the Docker daemon, and if a name is not
       assigned to the container with --name then the daemon will also  gener‐
       ate  a  random string name. The name is useful when defining links (see
       --link) (or any other place you need to  identify  a  container).  This
       works for both background and foreground Docker containers.
   -P, --publish-all=true|false
          Publish  all  exposed  ports to random ports on the host interfaces.
       The default is false.

       When set to true publish all exposed ports to the host interfaces.  The
       default is false. If the operator uses -P (or -p) then Docker will make
       the exposed port accessible on the host and the ports will be available
       to  any client that can reach the host. When using -P, Docker will bind
       any exposed port to a random port on the host within an ephemeral  port
       range  defined  by  /proc/sys/net/ipv4/ip_local_port_range. To find the
       mapping between the host ports and the exposed ports, use docker port.
   --link=[]
          Add link to another container in the form of <name or  id>:alias  or
       just <name or id> in which case the alias will match the name

       If  the  operator  uses  --link when starting the new client container,
       then the client container can access the exposed  port  via  a  private
       networking interface. Docker will set some environment variables in the
       client container to help indicate which interface and port to use.
   -e, --env=[]
       Set environment variables

       This  option allows you to specify arbitrary environment variables that
       are available for the process that will be launched inside of the  con‐
       tainer.
   --restart="no"
          Restart  policy  to  apply  when  a  container  exits  (no, on-fail‐
       ure[:max-retry], always, unless-stopped).
```

# docker command

## port rm stop 
```
docker ps 
docker stop id
docker restart id
docker ps -a (show all docker id)
docker port id
```

## docker start and kill
we can use stop for graceful shutdown.
```
docker stop -t id (send SIGTERM first SIGKILL after)
docker kill id
docker rm (id)
```

## docker logs

docker logs add .

```
docker logs -f (id)
docker inspect --format='{{.NetworkSettings.IPAddress}}' (id)
```

## docker entrypoint
The ENTRYPOINT specifies a command that will always be executed when the container starts.

The CMD specifies arguments that will be fed to the ENTRYPOINT.
```
FROM ubuntu
ENTRYPOINT
CMD
```
### docker file ONBUILD
Build triggers.

```
ONBUILD ADD . /
ONBUILD RUN bunder install
```

## docker network

Three network available .
1. host
2. bridge
3. null

```
docker network ls
```



### docker-compose

docker-compose up can start a docker compose app.

before docker compose you should run 
```
docker-machine create --driver virtualbox default
docker-machine start default
```
