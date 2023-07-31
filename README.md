# parrot-build
Running ParrotOS HTB Edition: https://parrotlinux.org/download/

In the future, might switch to Architect to remove need for DE and choose specific tools.

Using virt-manager to provision the .iso and allocate CPU, memory etc.

Using the following aliases in my .bashrc to interact with the vm on host:

```bash
export PARROT=192.168.122.229 # Change IP here.
alias sshparrot="ssh -X user@$PARROT" # Change user here.

# I named my vm parrot, so edit the use of parrot here if needed.
# Make sure current user is part of libvirt group.
alias startparrot="virsh start parrot"
alias shutdownparrot="virsh shutdown parrot"
alias snapcreateparrot="virsh snapshot-create parrot"
alias snaploadparrot="virsh snapshot-revert parrot --current"
alias snapoverwriteparrot="virsh snapshot-delete parrot --current && virsh snapshot-create parrot"
```

I'm using ssh with X11 forwarding. The snapshot creations/reverts are useful when I have a tmux session because it saves the current state when I shutdown/start the host machine and choose to pick up where I left off.

## configure-ssh
`ssh-copy-id` to the target machine. Edit the ListenAddress and AllowUsers as well located in roles/configure-ssh/files/sshd\_config.

## Install

git clone the repo and run:
```bash
ansible-playbook main.yml
```

## TODO
Install gef for gdb, pwntools, Ghidra.
