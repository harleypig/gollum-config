# gollum-config

## Gollum configuration files and notes

### Systemd User Service File

Copy the service file to the user systemd service directory.

    cp gollum@.service $HOME/.config/systemd/user

Edit the service file and change the `WorkingDirectory` to match your setup.

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

---

### Configuration File

You will need to mix and match these files as needed. When I figure out how
to include a file I'll change these instructions accordingly.

#### Command line options

`config.rb.wiki-options` has an example of how you would set your command line
options instead of in your systemd file.

**NOTE**: This is not complete. Please point out something I'm missing or have wrong.

#### Set default markup

`config.rb.set-default-markup` shows how to change gollums default markup.

#### Commit as logged in user

`config.rb.commit-as-login-user` shows how to have commits tagged with the
logged in user instead of the system user running the process.

---

### Configure vimwiki

#### vimwiki settings

Make vim change to the directory of the current file. I've found there is less
confusion and issues with some plugins (markdownlint for one).

Either put this setting in a filetype file, or in an auto group.

I have mine in `ftplugin/vimwiki.vim`

    setlocal autochdir

An auto group definition might look like the following.

    augroup vimwiki
      au! BufEnter * silent setlocal autochdir
    augroup END

Finally, tell vimwiki to use the `md` extension by default.

    let g:vimwiki_list = [{ 'path': '~/path/to/wikis/yourwiki', 'syntax': 'markdown', 'ext': 'md' }]

#### syntastic settings

Where to put these settings is up to you. I've put this section in
`after/plugin/syntastic.vim` with other syntastic settings.

    " Markdown
    " mdl and proselint
    let g:syntastic_markdown_mdl_exec = "markdownlint"
    let g:syntastic_markdown_mdl_args = ""
    let g:syntastic_markdown_checkers = ['mdl', 'proselint']

    " Include vimwiki in Markdown checks
    let g:syntastic_vimwiki_checkers = ['markdown/mdl', 'markdown/proselint']

---

### Configure gitwatch
