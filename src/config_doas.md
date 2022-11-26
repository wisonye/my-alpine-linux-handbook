# Config doas

- Install `doas` (run as `root`)

    ```bash
    apk --no-cache add doas doas-doc
    ```

    </br>

- Config `doas`

    Then edit `/etc/doas.d/doas.conf` and add the following settings:

    ```bash
    permit persist keepenv setenv { PATH } YOUR_USER_NAME_HERE as root
    ```

    For more details, run `man doas.conf` to know more.

    </br>



