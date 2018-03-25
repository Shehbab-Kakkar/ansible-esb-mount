# ansible-esb-mount
Ansible role for mounting ESB volumes on Amazon EC2 instances.
This role is meant to be used on an **empty** volume.
The changes are persistent, the volume will automount on boot. 

## Requirements
This role assumes that you have your instance setup and ESB volume attached to it. You will need the device name, which you can obtain with **lsblk** command.
Use [Making an Amazon EBS Volume Available for use](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html) for reference.

## Role Variables
`file_system` Which filesystem will be created on the volume. Defaults to ext4
`device_name` Device name of the volume. Defaults to /dev/xvdb
`mount_point` Mount point directory. Defaults to /data
`user` Owner of the mount point directory. Defaults to ubuntu. Also used for group

## Dependencies
There are no external dependencies

## Example Playbook
```
- hosts: ec2
  gather_facts: no
  remote_user: ubuntu
  become: yes
  become_method: sudo
  roles:
   - esb.mount

  vars:
    file_system: ext4
    device_name: /dev/xvdb
    mount_point: /data
    user: ubuntu 
```