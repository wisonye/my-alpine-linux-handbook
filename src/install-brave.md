# Install Brave

Plz make sure `dbus` service is running, otherwise, you will see the following
error:

```bash
cannot connect to system bus
```

</br>

- Add the Flathub repository

    ```bash

    doas flatpak remote-add flathub-beta https://flathub.org/beta-repo/flathub-beta.flatpakrepo
    ```

    </br>

- Install

    ```bash
    doas flatpak install flathub-beta com.brave.Browser

    # Looking for matches…
    # Required runtime for com.brave.Browser/x86_64/beta (runtime/org.freedesktop.Platform/x86_64/22.08) found in remote flathub
    # Do you want to install it? [Y/n]: Y
    # 
    # com.brave.Browser permissions:
    #     ipc                    network                  cups                          pulseaudio        wayland        x11       devices       file access [1]
    #     dbus access [2]        bus ownership [3]        system dbus access [4]
    # 
    #     [1] /run/.heim_org.h5l.kcm-socket, host-etc, xdg-desktop, xdg-documents, xdg-download, xdg-music, xdg-run/pipewire-0, xdg-videos, ~/.local/share/applications:create, ~/.local/share/icons:create
    #     [2] org.freedesktop.FileManager1, org.freedesktop.Notifications, org.freedesktop.ScreenSaver, org.freedesktop.secrets, org.gnome.Mutter.IdleMonitor.*, org.gnome.SessionManager
    #     [3] org.mpris.MediaPlayer2.chromium.*
    #     [4] org.freedesktop.Avahi, org.freedesktop.UPower
    # 
    # 
    #         ID                                             Branch            Op            Remote                  Download
    #  1. [✓] org.freedesktop.Platform.GL.default            22.08             i             flathub                 130.7 MB / 131.0 MB
    #  2. [✓] org.freedesktop.Platform.Locale                22.08             i             flathub                  39.1 MB / 333.0 MB
    #  3. [✓] org.freedesktop.Platform.openh264              2.2.0             i             flathub                   1.2 MB / 944.3 kB
    #  4. [✓] org.freedesktop.Platform                       22.08             i             flathub                 172.2 MB / 214.4 MB
    #  5. [✓] com.brave.Browser                              beta              i             flathub-beta            155.5 MB / 155.7 MB
    # 
    # Installation complete.
    ```

    </br>


- How to run

    ```bash
    dbus-run-session flatpak run \
        --filesystem=~/Downloads \
        --env=TZ=Pacific/Auckland \
        run com.brave.Browser
    ```

    </br>

- How to install chrome extension

    Watch [this](https://www.youtube.com/watch?v=zYBwOEfDJBM&t=85s)

    </br>

