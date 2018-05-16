# common-Ubuntu-operations

Record common system operations on Ubuntu

# Files

## 1. Make links to a file or a folder

- `ln -s source_file target_file`

- `ln -s source_folder target_folder`

Make links to specific files:

- `ln -s source_folder/{1000..1025}.jpg target_folder`

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

# Operations

## 1. loginto a remote machine

Use **ssh**:

- `ssh -p port username@192.168.3.3`

