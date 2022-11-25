# Base configuration after installation

- Update and upgrade all installed packages

    ```bash
    apk update && apk upgrade
    ```

    </br>

- Add user and config `doas`

    ```bash
    adduser YOUR_USER_NAME_HERE

    # Install `doas`
    apk add doas

    # Add user to `wheel` group
    adduser YOUR_USER_NAME_HERE wheel
    ```

    Then edit `/etc/doas.d/doas.conf` and add the following settings:

    ```bash
    permit persist :wheel
    ```

    Optional, add newly created user to `audio,video,netdev` groups if that's
    your dialy user:

    ```bash
    adduser YOUR_USER_NAME_HERE audio
    adduser YOUR_USER_NAME_HERE video
    adduser YOUR_USER_NAME_HERE netdev
    adduser YOUR_USER_NAME_HERE input
    ```

    Re-login to take effect.

    After re-login with your new user, run `groups` to confirm all assigned groups.

    </br>

- Install `fish` and set it as default shell

    First, you need to enable the community repo by running:

    ```bash
    doas vi /etc/apk/repositories


    # Make sure the follow line is uncomment
    http://mirror.2degress.nz/alpine/v.315/community
    ```

    </br>

    Now, update and install `fish` and `libuser`

    ```bash
    doas apk update
    doas apk add --no-cache fish libuser
    ```

    </br>

    ```bash
    doas touch /etc/login.defs
    doas touch /etc/default/useradd

    # Print the `fish` path
    which fish

    # Change user shell
    doas lchsh YOUR_USER_NAME_HERE
    ```

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


- Install and config `git`

    ```bash
    doas apk --no-cache add git

    git config --global user.name "Your Name Comes Here"
    git config --global user.email you@yourdomain.example.com
    ```

    You can run `git config --global --list` to confirmt the settings.

    </br>


- Fixed the unicode display issue in console

    If you use `bat` to print content, it can't display correctly!!!

    ```bash
    doas vi /etc/rc.conf

    # Change unicode value to `YES`
    unicode="YES"
    ```

    Reboot to take effect.

    </br>

