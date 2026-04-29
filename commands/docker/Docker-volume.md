To create a Docker Volume use the command:
```
docker volume create [volume_name]
```
```
docker volume create data
```
To verify you have successfully created a Docker volume, prompt Docker to list all available volumes with:
```
docker volume list
```
To see more information about a Docker volume, use the inspect command:
```
docker volume inspect [volume_name]
```
To run a container and mount a data volume to it, follow the basic syntax:
```
docker run --mount source=[volume_name],destination=[path_in_container] [docker_image]
```
```
docker run -it --name=example1 --mount source=data,destination=/data ubuntu
```
Then, check to verify the volume was successfully mounted by listing the content of the container:
```
ls
```
Copying Files Between Containers From a Shared Volume
```
cd data
```
```
touch sample1.txt
```
```
exit
```
launch a new container example2 with the same data volume:
```
docker run -it --name=example2 --mount source=data,destination=/data ubuntu
```
List the content of the container. You should find the data directory, as in example1:
```
ls
```
```
cd data
```
```
ls
```

Mounting a Host Directory as a Data volume
docker run -v "$(pwd)":[volume_name] [docker_image]

mkdir tmp
cd tmp
touch file.txt
docker run -it -v "$(pwd)":/data1 ubuntu
ls
cd data1
ls
