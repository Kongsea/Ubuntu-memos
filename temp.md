# Record temporary usage

1. ssh -p 2222 -R 27017:localhost:27017 -N -f 192.168.3.4

  - run this command on 192.168.3.5, then run a program on 3.4 and the program will access port 27017 of 3.5

2. mount a local folder to docker

  - docker run -t --rm -v /local_folder:/folder_in_docker docker_name:tag

  - docker run -t --rm --mount type=bind,source=/local_folder,target=/folder_in_docker docker_name:tag

3. mount a folder mounted from a remote host to docker

   Use `docker volume`: [ref](https://github.com/vieux/docker-volume-sshfs)

  - docker volume ls

  - docker volume rm `volumename`

  - docker plugin install --grant-all-permissions vieux/sshfs

  - docker volume create -d vieux/sshfs -o sshcmd=username@remote_host:/folder_on_remote_host -o password='password' -o port='port' sshvolume

  - docker run -t --name sshfs-container --mount src=sshvolume,target=/folder_in_docker,type=volume,volume-driver=vieux/sshfs --rm docker_name:tag