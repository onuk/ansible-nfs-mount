ansible-nfs-mount
=========

This ansible role manages NFS mounts in the system.

Requirements
------------

Ansible 2.10.8

Role Variables
--------------

|Variable|Description|
|--------|-----------|
| nfs_mount_opts | Default NFS mount options |
| nfs_version | Default NFS version to use (4) |
| nfs_share_mounts | List of dictionaries of NFS shares: (path: mount-point, location: nfs server path, opts: mount options (optional), dump: fs to dump (optional), passno: fs checks on reboot (optional), state: choose (https://docs.ansible.com/ansible/latest/modules/mount_module.html#parameter-state "the state") (default: mounted)|


Dependencies
------------
N/A

Example of how to use the role
----------------

    - hosts: localhost
      become: true
      gather_facts: yes
      
      vars:
        nfs_version: 3 # to force nfs version to 3.
        nfs_share_mounts:
        - path: /mnt/public
          location: nfs.example.org:/mnt/public
        # remove a mount from a server
        - path: /mnt/public_old
          location: nfs.example.org:/public_old
          state: absent
        - path: /mnt/readonly
          location: nfs.example.org:/read-only
          opts: "{{ nfs_mount_opts }},ro"
        - path: /mnt/ex_passno
          location: nfs.example.org:/ex_passno
          passno: 0
        - path: /mnt/ex_dump
          location: nfs.example.org:/ex_dump
          dump: 0
    roles:
      - role: ansible-nfs-mount

License
-------

MIT

Author Information
------------------
[Yurii Onuk](https://onuk.org.ua)