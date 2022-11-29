# Config git

- Install `git`

    ```bash
    doas apk --no-cache add git
    ```

    </br>

- Config `git`

    ```bash
    git config --global user.name "Your Name Comes Here"
    git config --global user.email you@yourdomain.example.com
    git config --global pull.rebase false
    ```

    You can run `git config --global --list` to confirmt the settings.

    </br>

    Make sure to [generate ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux)
    and add it to your github [SSH and GPG Keys](https://github.com/settings/keys)

    </br>

- Generate `~/.ssh/config` if not exists

    If you will use some docker images that contain an older version of `git`,
    then you better have the `IgnoreUnknown UseKeychain` settings, as older
    `git` doesn't recognize the `UseKeyChain` option:

    ```bash
    Host *
      IgnoreUnknown UseKeychain
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_ed25519
    ```

    </br>


- Install and config `git-delta`

    ```bash
    doas apk --no-cache add delta
    ```

    </br>

    Add the following configs to `~/.gitconfig`:

    ```bash
    [color]
    	ui = true
    [init]
    	defaultBranch = master
    [pull]
    	rebase = false
    [core]
        pager = delta

    [interactive]
        diffFilter = delta --color-only
    [add.interactive]
        useBuiltin = false # required for git 2.37.0

    [delta]
        navigate = true    # use n and N to move between diff sections
        light = false      # set to true if you're in a terminal w/ a light background color (e.g. the default macOS terminal)
        line-numbers = true
        side-by-side = true
        show-syntax-themes = true

    [merge]
        conflictstyle = diff3

    [diff]
        colorMoved = default
    ```


    </br>

