# Sandboxed dropbox

Runs sandbox in a systemd-nspawn container with only access to ~/Dropbox (and .dropbox / .dropbox-dist)

# Usage

- install systemd-container (debian anyway)
- edit dropbox.service.example, search and replace USERNAME with your username
- copy dropbox.service.example to /etc/systemd/system/dropbox.service
- mkdir -p /var/lib/machine/dropbox/{etc,bin,usr,usr/bin}
- copy passwd and group and delete everything but you and root
- download dropbox headless, untar as normal
- systemctl daemon-reload
- systemctl start dropbox.service
- enable at boot with systemctl enable dropbox.service
- configure your desktop environment to run dropboxicon script at startup


# TODO

- capabilities assignment is rubbish: we want KILL but it's not possible to say "everything but KILL", so they have to be enumerated
- timeout on socket operations
