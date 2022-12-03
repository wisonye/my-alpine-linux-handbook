# Change default shell

- Install `fish`

    First, you need to enable the community repo by running:

    ```bash
    doas vi /etc/apk/repositories


    # Make sure the uncomment the `community` repo
    http://mirror.2degress.nz/alpine/v.{OS_VERSION}/community
    ```

    </br>

    Now, update and install `fish` and `libuser`

    ```bash
    doas apk update

    # If you don't install `fish-doc`, then you won't have internal command
    # man pages (includes `--help` support)
    doas apk add --no-cache fish fish-doc libuser
    ```

    </br>

- Change the default shell

    ```bash
    doas touch /etc/login.defs
    doas mkdir /etc/default
    doas touch /etc/default/useradd

    # Print the `fish` path
    which fish

    # Change user shell
    doas lchsh YOUR_USER_NAME_HERE
    ```

    </br>

    Tips:

    _If you see `Authentication failed for files.` (even though you've already
    typed the correct password), then you should give up and modify the `shell`
    part directly in `/etc/passwd`, that does the trick!!!_

    </br>


    After re-login, add the following settings to fish config for a better
    typeing life:

    ```bash
    vi ~/.config/fish/confish.fish


    #--------------------------------------------------------
    # 1. Enable `vi mode` key bindings
    # 2. bind `jj` to escape
    # 3. bind `ctrl+l` to accept the first suggection
    #
    # Tips: When u don't know what key (or key combo) to write
    #       into the `bind` command, just run `fish_key_reader`
    #       binary and press the key (or key combo), it will 
    #       print out which `key` you should put into the `bind`
    #       command.
    #--------------------------------------------------------
    set -g fish_key_bindings fish_vi_key_bindings
    bind -M insert -m default jj  backward-char force-repaint
    bind -M insert \f accept-autosuggestion


    #--------------------------------------------------------
    # Path
    #--------------------------------------------------------
    set PATH /sbin /usr/sbin $PATH

    #--------------------------------------------------------
    # Abbreviation
    #--------------------------------------------------------
    abbr c "clear"
    abbr shutdown "doas poweroff"
    ```

    </br>

