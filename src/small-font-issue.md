# GTK/QT Small font issue

Sometimes, you will see application font size is too small, easy fix:

- GTK Application

    Pass the `GDK_DPI_SCALE=SCALE_NUMBER_HERE` env var to the program like this:

    ```bash
    GDK_DPI_SCALE=1.5 pavucontrol

    GDK_DPI_SCALE=1.5 dbus-run-session flatpak --filesystem=~/Downloads run com.brave.Browser
    ```

    </br>


- QT Application

    ```bash
    QT_SCALE_FACTOR=1.5 PROGRAM_NAME_HERE
    ```

    </br>


