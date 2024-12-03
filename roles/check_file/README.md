check_file
=========
This role will check the image files' checksum between target server and repository server, in order to determine if can skip the transfer or not

Role Variables
--------------

| Variable                         | Type          | Description                                                        |
|----------------------------------|---------------|--------------------------------------------------------------------|
| `check_file_target_file_path`    | str           | The file path on target server. |
| `check_file_repo_file_path`      | str           | The file path on repository server. |
| `check_file_repo_server`         | str           | The system that has the src ptf group's files, which will be transferred to the target system. |

Return Variables
--------------

| Variable                         | Type          | Description                                               |
|----------------------------------|---------------|-----------------------------------------------------------|
| `check_file_same_files`          | bool          | File consistency flag.                |

Example Playbook
----------------
```
- name: Example of check_file role
  hosts: testhost

  tasks:
    - name: Include check_files role to determine if the files are the same between repository server and target server
      include_role:
        name: check_file
      vars:
        check_file_target_file_path: "/home/tester/PTF/SF99876"
        check_file_repo_file_path: "/tmp/SF99876"
        check_file_repo_server: srchost

```
Example Returned Variables
----------------
```
"check_file_same_files": true

```
License
-------

Apache-2.0
