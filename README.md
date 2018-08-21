# common-Ubuntu-operations

Record common system operations on Ubuntu

# Files and Folders

## 1. Make links to a file or a folder

- `ln -s source_file target_file`
- `ln -s source_folder target_folder`

Make links to specific files:

- `ln -s source_folder/{1000..1025}.jpg target_folder`
- copy files from 200001.jpg to 200100.jpg: `cp source_folder/20{0001..0100}.jpg target_folder`

## 2. Copy files the links linked to to a folder

Use **rsync**:

- `rsync -aL source_folder target_folder`

## 3. Copy files from or to remote servers

From local to remote:

- Folder: `scp -P port -r source_folder username@192.168.3.3:/target_folder`
- File: `scp -P port source_file username@192.168.3.3:/target_file`

From remote to local:

- Folder: `scp -P port -r username@192.168.3.3:/source_folder target_folder`
- File: `scp -P port username@192.168.3.3:/source_file target_file`

## 4. Copy folder from or to remote servers exclude some files or folders

Copy `source_folder` to `target_folder`:
- `rsync -arP -e "ssh -p 2222" --max-size='100M' --exclude /exclude_folder1/ --exclude /exclude_folder2/ username@192.168.3.3:/source_folder/ target_folder/`

  - a: archive mode
  - r: recursively
  - P: partial and progress
  - e: ssh and set port
  - max-size: emit large files
  - exclude: exclude some files or folders

## 5. Check disk usage and show large files and folders

- `du -h --threshold=1G | sort -h`
- Or: `sudo du -h --threshold=1G | sort -h`

## 6. Count files

Count files in current folder or some folder:

- `ls | wc -l`
- Or: `ls -al | wc -l`

## 7. Mount a remote filesystem

Mount a remote filesystem to local and use it like local drives:

- `sshfs -p 2222 user@192.168.3.3:/remote_folder/ local_folder/`

# Operations

## 1. login to a remote machine

Use **ssh**:

- `ssh -p port username@192.168.3.3`

## 2. Run a program background after closing Terminal

Use **screen**:

- `screen -S screen_name`
- Run the program in the opened scene, then close the Terminal
- `screen -r screen_name` to restore the running program and look up the running status

## 3. Run a shell after closing Terminal

- `./shell.sh &`

For example:

- `tensorboard --logdir tensor_dir &`

## 4. Visualize an image from Terminal

Sometimes there are a huge number of images in a folder, you want to visualize
an image from Terminal instead of opening the folder. Use:

- `eog file_path`

## 5. Look up some running process

We want to check some running process, for example, processes running using python. Use:

- `ps -ef | grep python`

## 6. Search contents of files

Search from contents of files.

- `grep -r content [file or folder]`

## 7. Git operations

Set Git user.name and user.email:

- `git config --global user.name "Kongsea"`
- `git config --global user.email "Kongsea@gmail.com"`

Look up the settings:

- `git config --global user.name`
- `git config --global user.email`

## 8. Login to server while not input the password every time

Use ssh-copy-id:

- `ssh-copy-id user@192.168.3.3`
- `ssh-copy-id -p 23 user@192.168.3.3`

Then you can use `ssh` or `scp` and don't need to input the password.

## 9. Count file numbers under current directory according to subfolders

Use find:

```
find . -type d -print0 | while read -d '' -r dir; do
  files=("$dir"/*)
  printf "%5d files in directory %s\n" "${#files[@]}" "$dir"
done
```
or:

- `find -type d -maxdepth 1 | xargs -I {} sh -c "echo {}; ls -1 {} | wc -l"`

or use:

- `du -a | cut -d/ -f2 | sort | uniq -c | sort -nr`

## 10. Check a file in hex mode

Use hexdump:

Check 512 bytes from 800 bytes:

- `hexdump -C -s 800 -n 512 filename`

or use:

- `tail -f somefile | hexdump -C`

to check a file from end


