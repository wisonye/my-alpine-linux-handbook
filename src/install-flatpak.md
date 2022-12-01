# Install flatpak

[Flatpak](https://flatpak.org/) - The future of apps on Linux

</br>

- Install

    ```bash
    doas apk --no-cache add flatpak
    ```

    </br>


    Plz make sure `dbus` service is running, otherwise, you will see the following
    error when running `flatpak remote-add`

    ```bash
    cannot connect to system bus
    ```

    </br>

    Add the Flathub repository

    ```bash
    doas flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
    ```

    Better to restart to make sure take affect.

    </br>


- List all installed apps

    ```bash
    flatpak list

    # Name                          Application ID                                Version                Branch          Origin               Installation
    # Brave Browser                 com.brave.Browser                             1.47.99                beta            flathub-beta         system
    # ungoogled-chromium            com.github.Eloston.UngoogledChromium          88.0.4324.183          beta            flathub-beta         system
    # Freedesktop Platform          org.freedesktop.Platform                      20.08.21               20.08           flathub              system
    # Freedesktop Platform          org.freedesktop.Platform                      22.08.3                22.08           flathub              system
    # Mesa                          org.freedesktop.Platform.GL.default           21.1.8                 20.08           flathub              system
    # Mesa                          org.freedesktop.Platform.GL.default           22.1.7                 22.08           flathub              system
    # openh264                      org.freedesktop.Platform.openh264             2.1.0                  2.0             flathub              system
    # openh264                      org.freedesktop.Platform.openh264             2.1.0                  2.2.0           flathub              system
    ```

    </br>

- Query app info

    ```bash
    flatpak info APPLICATION_ID
    ```

    </br>

- Search apps to install

    ```bash

    flatpak remote-ls | rg Ungoogled

    # UngoogledChromium      com.github.Eloston.UngoogledChromium           stable  x86_64  flathub
    # Codecs                 com.github.Eloston.UngoogledChromium.Codecs    stable  x86_64  flathub
    # UngoogledChromium      com.github.Eloston.UngoogledChromium           beta    x86_64  flathub-beta
    # Codecs                 com.github.Eloston.UngoogledChromium.Codecs    beta    x86_64  flathub-beta
    ```

    Or go to [here](https://flathub.org/home) to search

    </br>

- Install

    ```bash
    doas flatpak install [Congifured Remote Branch] APPLICATION_ID
    ```

    </br>

- Uninstall

    ```bash
    doas flatpak uninstall APPLICATION_ID
    ```

    </br>

- List configured remotes

    ```bash
    flatpak remotes

    # Name         Options
    # flathub      system
    # flathub-beta system
    ```

    </br>


- How to run

    ```bash
    # For normal app
    doas flatpak run APPLICATION_ID

    # For the app that needs a message bus, you should use a session bus to run
    # For example, most browser apps need message bus to work
    dbus-run-session flatpak run \
        --filesystem=~/Downloads \
        --env=TZ=Pacific/Auckland \
        run com.brave.Browser
    ```

    </br>

    - About sandbox file access permissions

        This is the tricky part, as `flatpak` runs app in sandbox by default. That
        means the app itself cannot access the host file system.

        If you want to import bookmark from a file or save the download file to
        somewhere (on your host file system), then you have to give it the permission
        like this:

        ```bash
        # Suppose that allow the app to access (read & write) to host `~/Downloads`
        dbus-run-session flatpak run --filesystem=~/Downloads run com.brave.Browser

        # Suppose that allow the app to access (read only) to host `/tmp`
        dbus-run-session flatpak run --filesystem=/tmp:ro run com.brave.Browser
        ```

        Even if you want a browser app to get the correct timezone from your host,
        you need to pass via the `--env` like this:

        </br>

        ```bash
        dbus-run-session flatpak run \
            --filesystem=~/Downloads \
            --env=TZ=Pacific/Auckland \
            run com.brave.Browser
        ```

        </br>

