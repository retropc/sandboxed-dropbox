# Sandboxed dropbox

Runs sandbox in a systemd-nspawn container, restricted to ~/Dropbox and ~/.dropbox*

# Usage

- install systemd-container (on debian)
- edit dropbox.service.example, search and replace USERNAME with your username
- copy dropbox.service.example to /etc/systemd/system/dropbox.service
- mkdir -p /var/lib/machine/dropbox/{etc,bin,usr,usr/bin}
- copy passwd and group and delete everything but you and root
- download dropbox headless, untar as normal
- mkdir -p ~/.dropbox_sandbox/{home,root}
- mv ~/.dropbox* ~/.dropbox_sandbox/home
- mv ~/Dropbox ~/.dropbox_sandbox/home
- copy "run" script to ~/.dropbox_sandbox/root
- ln -s ~/.dropbox_sandbox/home/Dropbox ~
- ln -s ~/.dropbox_sandbox/home/.dropbox ~
- systemctl daemon-reload
- systemctl start dropbox.service
- enable at boot with systemctl enable dropbox.service
- configure your desktop environment to run dropboxicon script at startup


# TODO

- capabilities assignment is rubbish: we want KILL but it's not possible to say "everything but KILL", so they have to be enumerated
- there is a cap that is preventing dropbox from upgrading properly... not sure which it is
- timeout on socket operations
