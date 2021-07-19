# gollum-config

Gollum configuration files and notes.

## Systemd User Service File

Copy the service file to the user systemd service directory.

    cp gollum@.service $HOME/.config/systemd/user

Run the systemd enable command.

    systemd --user enable gollum@<yourwiki>.service

Use the systemd edit command to set which port you need to start gollum
with.

    systemctl --user edit gollum@<yourwiki>.service

Add the following lines to the override file.

    [Service]
    Environment="PORT=<yourport>"

Reload the systemd daemon.

    systemctl --user daemon-reload

Start your wiki.

    systemctl --user start gollum@<yourwiki>.service


## Configuration File
