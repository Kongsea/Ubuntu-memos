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

4. Backup and restore settings of Terminal:

  - backup: `dconf dump /org/gnome/terminal/ > gnome_terminal_settings_backup.txt`

    [backup files](./gnome_terminal_settings.txt)

  - restore: `dconf load /org/gnome/terminal/ < gnome_terminal_settings_backup.txt`

5.Windows下访问WSL文件夹提示`\\wsl.localhost 无法访问。你可能没有权限使用网络资源。请与这台服务器的管理员联系以查明你是否有访问权限。` [refer](https://lotl.cn/wsl/)

  - 打开注册表编辑器，修改两个文件

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\NetworkProvider\Order`
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\NetworkProvider\HwOrder`

  - 将两个目录下的`ProviderOrder`原始数值都修改成: `P9NP,RDPNP,LanmanWorkstation,webclient`
