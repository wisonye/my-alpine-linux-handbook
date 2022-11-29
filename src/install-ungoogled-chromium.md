# Install ungoogled-chromium

If you like `Google Chrome` but don't like that it gathers your personal
information, then you can install `Ungoogled Chromium`!!!

[Here](https://github.com/ungoogled-software/ungoogled-chromium) is the github repo.

</br>

Plz make sure `dbus` service is running, otherwise, you will see the following
error:

```bash
cannot connect to system bus
```

</br>

- Install `flatpak` if not yet

    ```bash
    doas apk --no-cache add flatpak
    ```

- Add the Flathub repository

    ```bash
    doas flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
    ```

    Better to restart to make sure take affect.

    </br>


- Install `ungoogled-chromium`


    ```bash
    doas flatpak install flathub-beta com.github.Eloston.UngoogledChromium

    # Looking for matches…
    # Required runtime for com.github.Eloston.UngoogledChromium/x86_64/beta (runtime/org.freedesktop.Platform/x86_64/20.08) found in remote flathub
    # Do you want to install it? [Y/n]: Y

    # Info: runtime org.freedesktop.Platform branch 20.08 is end-of-life, with reason:
    #    org.freedesktop.Platform 20.08 is no longer receiving fixes and security updates. Please update to a supported runtime version.
    # Info: applications using this runtime:
    #    com.github.Eloston.UngoogledChromium

    # Info: runtime org.freedesktop.Platform.GL.default branch 20.08 is end-of-life, with reason:
    #    org.freedesktop.Platform 20.08 is no longer receiving fixes and security updates. Please update to a supported runtime version.
    # Info: applications using this runtime:
    #    com.github.Eloston.UngoogledChromium

    # com.github.Eloston.UngoogledChromium permissions:
    #     ipc wayland x11



    #         ID                                               Branch            Op            Remote                  Download
    #  1. [✓] org.freedesktop.Platform.GL.default              20.08             i             flathub                 105.8 MB / 106.4 MB
    #  2. [✓] org.freedesktop.Platform.Locale                  20.08             i             flathub                 143.3 MB / 322.5 MB
    #  3. [✓] org.freedesktop.Platform.openh264                2.0               i             flathub                   1.8 MB / 1.5 MB
    #  4. [✓] org.freedesktop.Platform                         20.08             i             flathub                 292.7 MB / 270.4 MB
    #  5. [✓] com.github.Eloston.UngoogledChromium             beta              i             flathub-beta             11.0 kB / 10.8 kB

    # Installation complete.

    ```

    </br>
