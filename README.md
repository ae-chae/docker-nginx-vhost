# docker-nginx-vhost
![image](https://github.com/ae-chae/docker-nginx-vhost/assets/102152330/f298abb9-aeaa-4052-bd39-bf3ce2998f2e)


# load-balancing
https://www.nginx.com/resources/glossary/load-balancing/
# step 1
docker rm * rmi
```
$ sudo docker images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
$ sudo docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

# step 2
```
$ docker run -itd -p 8002:80 --name serv-a nginx
$ docker run -itd -p 8003:80 --name serv-b nginx
$ docker run -itd -p 8001:80 --name lb nginx:latest


$ sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                   NAMES
2fe6b3ebdb6e   nginx          "/docker-entrypoint.…"   5 seconds ago    Up 4 seconds    0.0.0.0:8002->80/tcp, :::8002->80/tcp   serv-a
fafba17b8cf6   nginx          "/docker-entrypoint.…"   18 seconds ago   Up 17 seconds   0.0.0.0:8003->80/tcp, :::8003->80/tcp   serv-b
fd3ca54a154a   nginx:latest   "/docker-entrypoint.…"   3 minutes ago    Up 3 minutes    0.0.0.0:8001->80/tcp, :::8001->80/tcp   lb
```

# step 3
```
$ sudo docker network create aaa
$ sudo docker network connect aaa serv-a
$ sudo docker network connect aaa serv-b
$ sudo docker network connect aaa lb

```

```
$  sudo docker network inspect aaa
[
    {
        "Name": "aaa",
        "Id": "881a59f83da24a5002ec7a403dd323e400a05120e2ff9d0a9e0280ffd6229321",
        "Created": "2024-02-14T16:13:56.021336615+09:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "09803963d0aa5b70f4f71a0ddce3d17945ec2c2cc5534f45871cf04028dd42d0": {
                "Name": "serv-a",
                "EndpointID": "b260d972f06cd1d721e523136e206112dcade947bc83a08d7efe2659c8a32f62",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            },
            "5a936b389688915698d604318f654ee8a95f0946a947ea0a908fd13c8fc207ae": {
                "Name": "serv-b",
                "EndpointID": "f2bb7e4ff101550a3b51bf4007dc964660edee87482a5bb570e0c92ae017885a",
                "MacAddress": "02:42:ac:13:00:03",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            },
            "c51d7db70ff1466bbc0c085f090512c376f4c3a4b50c53c7da0b9ec1e09de301": {
                "Name": "lb",
                "EndpointID": "c4c578c7e7c6749787e85d9a81cef65ff805e6f476455d363de8112f0f995cdf",
                "MacAddress": "02:42:ac:13:00:04",
                "IPv4Address": "172.19.0.4/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
```



# ref
https://hub.docker.com/
