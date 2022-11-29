# Install ungoogled-chromium

If you like `Google Chrome` but don't like that it gathers your personal
information, then you can install `Ungoogled Chromium`!!!

[Here](https://github.com/ungoogled-software/ungoogled-chromium) is the github repo.

</br>

- Install `ungoogled-chromium`


    ```bash
    doas flatpak install flathub com.github.Eloston.UngoogledChromium

    # Looking for matches…
    # Required runtime for com.github.Eloston.UngoogledChromium/x86_64/stable (runtime/org.freedesktop.Platform/x86_64/21.08) found in remote flathub
    # Do you want to install it? [Y/n]:
    # 
    # com.github.Eloston.UngoogledChromium permissions:
    #     ipc                    network                  cups                          pulseaudio        wayland        x11       devices       file access [1]
    #     dbus access [2]        bus ownership [3]        system dbus access [4]
    # 
    #     [1] /run/.heim_org.h5l.kcm-socket, home
    #     [2] com.canonical.AppMenu.Registrar, org.freedesktop.FileManager1, org.freedesktop.Notifications, org.freedesktop.ScreenSaver, org.freedesktop.secrets, org.gnome.SessionManager, org.kde.kwalletd5
    #     [3] org.mpris.MediaPlayer2.chromium.*
    #     [4] org.freedesktop.Avahi, org.freedesktop.UPower
    # 
    # 
    #         ID                                                      Branch             Op            Remote             Download
    #  1. [✓] com.github.Eloston.UngoogledChromium.Codecs             stable             i             flathub              1.1 MB / 1.1 MB
    #  2. [✓] org.freedesktop.Platform.GL.default                     21.08              i             flathub            129.8 MB / 129.8 MB
    #  3. [✓] org.freedesktop.Platform.Locale                         21.08              i             flathub             34.2 MB / 326.3 MB
    #  4. [✓] org.freedesktop.Platform                                21.08              i             flathub            204.8 MB / 201.4 MB
    #  5. [✓] com.github.Eloston.UngoogledChromium                    stable             i             flathub            127.7 MB / 134.7 MB
    # 
    # Installation complete.
    ```

    </br>

- How to run

    ```bash
    dbus-run-session flatpak com.github.Eloston.UngoogledChromium
    ```

    </br>

