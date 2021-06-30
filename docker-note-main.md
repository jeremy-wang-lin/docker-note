# Docker 筆記

Command Line Reference:
https://docs.docker.com/engine/reference/commandline/docker/

Management command 與 傳統 command 對照：
https://blog.couchbase.com/docker-1-13-management-commands/



## docker image
### docker image pull
```
### Syntax
docker image pull = docker pull

docker image pull <repository>:<tag>
<repository> = [<image registry>/][<namespace>/]<repository base name>

### [Examples]
docker image pull ubuntu:latest
docker image pull microsoft/powershell:nanoserver
docker image pull k8s.gcr.io/kube-apiserver:v1.15.5
docker image pull gcr.io/nigelpoulton/tu-demo:v2
```
### docker image inspect
```
# 顯示 image 的詳細資訊
docker image inspect ubuntu:latest
```

### docker image history
```
# 看 image 每層 layer 建置的 history. 可以得知用哪些指令建置了這個 image
docker image history = docker history

docker image history web:latest

# 顯示完整的建置指令
docker image history --no-trunc web:latest

```

### docker image ls
```
docker image ls = docker images

# show all images (including intermediate images)
docker image ls -a

# show all images with digests
docker images --digests

# only show id
docker image ls -q
```

### docker image rm
```
# 刪除 docker image 以及相關的 image layer(s)
docker image rm <image name/image id>

## 如果要刪除的 image 有 container 在執行則會失敗
## 必須停止並移除該 image 相關的所有 container 才可以移除 image

## 如果相關的 image layer 有其他 image 有使用，則該共享的 image layer 不會被刪除


# tip: 刪除所有 image
docker image rm $(docker image ls -q) -f

## docker images ls -q 只會回傳 image id


```
### Build docker image from Dockerfile

勿輕忽 Dockerfile
- 對程式以及 dependency 有精準的描述
- 實現開發與部署的無縫接軌
- 本身就是個文件，協助他人很快地理解專案 
- 應該像重視 code 般地重視 Dockerfile, 並納入版控

```
docker image build = docker build

docker image build -t web:latest .
=
docker image build -f ./Dockerfile -t web:latest .

# 沒指定 Dockerfile 位置，預設則是當前目錄的 Dockerfile
# 最後的 . 不要漏了，它是指定 build docker image 的 context
```

### Tag and Push docker image
```
docker login
# 登入到 docker hub. 會提示要輸入帳號密碼

docker image tag web:latest jeremywanglin/web:lastest

docker image push jeremywanglin/web:latest
```

### docker image save
```
# backup docker image to tar file
docker image save = docker save

docker image save -o <image>.tar <image name>
```

### docker image load
```
# backup docker image to tar file
docker image save = docker save

docker image save -o <image>.tar <image name>
```



## docker container
[Docker Container](/8FKs_YAyRN2_5yDQUWKKmw)


## docker service
docker service create


## docker kill (send signal to container)
Send a custom signal to a container🔗
https://docs.docker.com/engine/reference/commandline/kill/#send-a-custom-signal--to-a-container

```
docker kill --signal=SIGHUP <my_container>
```

## docker logs 
```
docker logs <my_container>
```

###### tags: `docker`