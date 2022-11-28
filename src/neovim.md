# `Neovim`

- Installation build base

    `build-base` is the `build-essential` simular package in another Linux distro.

    You will see the following errors if you don't install it when using `treesitter`:

    ```bash
    cannot find -lstdc++: No such file or directory

    cc1p no such file or directory and -lstdc++ cannot find
    ```

    </br>

    ```bash
    doas apk --no-cache add build-base
    ```

    </br>


- Install `Neovim`

    ```bash
    doas apk --no-cache add neovim neovim-doc py3-pynvim xclip
    ```

    </br>

    If you don't install `xclip`, then clipboard copy&paste won't work, you can
    confirm that by running `:checkhealt` in `neovim`:

    ```bash
    ## Clipboard (optional)
        - OK: Clipboard tool found: xclip
    ```

    </br>

