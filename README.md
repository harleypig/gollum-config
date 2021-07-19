# gollum-config

## Gollum configuration files and notes

### Systemd User Service File

Copy the service file to the user systemd service directory.

    cp gollum@.service $HOME/.config/systemd/user

Run the systemd enable command.

    systemd --user enable gollum@<yourwiki>.service

Use the systemd edit command to set which port you need to start gollum with.

    systemctl --user edit gollum@<yourwiki>.service

Add the following lines to the override file.

    [Service]
    Environment="PORT=<yourport>"

Reload the systemd daemon.

    systemctl --user daemon-reload

Start your wiki.

    systemctl --user start gollum@<yourwiki>.service

### Configuration File

You will need to mix and match these files as needed. When I figure out how
to include a file I'll change these instructions accordingly.

#### Command line options

`config.rb.wiki-options` has an example of how you would set your command line
options instead of in your systemd file.

This is not complete. Please point out something I'm missing or have wrong.

#### Set default markup

`config.rb.set-default-markup` shows how to change gollums default markup.

### Configure vimwiki

### Configure gitwatch
