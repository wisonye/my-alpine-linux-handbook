# Base configuration after installation

- Update and upgrade all installed packages

    ```bash
    apk update && apk upgrade
    ```

    </br>

- Install man pages

    Alpine doesn't inclue man pages by default, you have to install by yourself:

    ```bash
    apk add mandoc man-pages
    ```

    </br>

    From now on, you need to install `xxxx-doc` when needed, for example:

    ```bash
    # Install software
    apk add doas

    # Install software man pages
    apk add doas-doc
    ```

    </br>



- Add user and config `doas`

    ```bash
    adduser YOUR_USER_NAME_HERE

    # Add user to `wheel` group
    adduser YOUR_USER_NAME_HERE wheel
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

