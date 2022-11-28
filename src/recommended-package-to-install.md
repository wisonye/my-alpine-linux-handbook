# Recommended package to install

All the packages below are optional but recommended which can make your life a bit easier before you install any DE (**`Desktop Environment`**) or WM (**`Window Manager`**).

- Useful utils

    ```bash
    doas apk --no-cache add ripgrep bat openssh bash neofetch util-linux lf
    ```

    `util-linux` package provides somthing like `lscpu, lsblk`, etc

    </br>

    If you use `bat` to print content, it can't display correctly, then try this
    to fix that:

    ```bash
    doas vi /etc/rc.conf

    # Change unicode value to `YES`
    unicode="YES"
    ```

    Reboot to take effect.

    </br>

- `procs` is a replacement for `ps` written in `Rust`.

    ```bash
    doas apk --no-cache procs
    ```

    Optionally, you can add `alias ps="procs"` (for `bash`) or `abbr ps "pros"` (for `fish`)
    to your shell configuration file.

    Some use cases:

    ```bash
    # Query `vim` related process
    procs vim

    # Query `vim` or `alacritty` related process
    procs --or vim alacritty

    # Query `vim` or `alacritty` and ascending sort by PID
    procs --or --sorta PID vim alacritty

    # Query `vim` or `alacritty` and descending sort by memory
    procs --or --sortd VmRss vim alacritty

    # Query `vim` or `alacritty` related process in watch mode (1s refresh rate)
    procs --or --watch vim alacritty
    ```

    </br>

    Also, you can custom the config to control which informat you want to show:

    `vim ~/.config/procs/config.toml` with the following settings:

    ```bash
    # For more detail setting information, plz visit https://github.com/dalance/procs
    
    [[columns]]
    # The column kind to show
    kind = "Pid"
    # Use which color to show
    style = "BrightYellow|Yellow"
    # This column can be search for as numeric parameter passed
    # to `procs` command?
    numeric_search = true
    # This column can be search for as non-numeric parameter passed
    # to `procs` command?
    nonnumeric_search = false
    # Alignment, "Left, Center, Right". "Left" by default.j
    # align = "Right"
    
    [[columns]]
    kind = "User"
    style = "BrightMagenta|Magenta"
    numeric_search = false
    nonnumeric_search = true
    align = "Right"
    
    [[columns]]
    kind = "Separator"
    style = "BrightWhite|White"
    color_075 = "BrightWhitee"
    numeric_search = false
    nonnumeric_search = false
    align = "Center"
    
    [[columns]]
    kind = "Tty"
    style = "BrightWhite|White"
    numeric_search = false
    nonnumeric_search = false
    align = "Center"
    
    [[columns]]
    kind = "Threads"
    style = "BrightWhite|White"
    numeric_search = false
    nonnumeric_search = false
    align = "Center"
    
    [[columns]]
    kind = "TcpPort"
    style = "BrightCyan|Cyan"
    numeric_search = true
    nonnumeric_search = false
    align = "Right"
    
    [[columns]]
    kind = "VmRss"
    style = "BrightGreen|Green"
    numeric_search = false
    nonnumeric_search = false
    align = "Right"
    
    # [[columns]]
    # kind = "UsageCpu"
    # style = "BrightGreen|Green"
    # numeric_search = false
    # nonnumeric_search = false
    # align = "Center"
    # 
    # [[columns]]
    # kind = "UsageMem"
    # style = "BrightGreen|Green"
    # numeric_search = false
    # nonnumeric_search = false
    # align = "Center"
    
    [[columns]]
    kind = "Separator"
    style = "BrightWhite|White"
    numeric_search = false
    nonnumeric_search = false
    align = "Center"
    
    [[columns]]
    kind = "Command"
    style = "BrightWhite|White"
    numeric_search = false
    nonnumeric_search = true
    align = "Left"
    
    [search]
    numeric_search = "Exact"
    nonnumeric_search = "Partial"
    logic = "And"
    
    [display]
    show_self = false
    show_thread = false
    show_thread_in_tree = true
    cut_to_terminal = true
    cut_to_pager = false
    cut_to_pipe = false
    color_mode = "Always"
    
    [sort]
    column = 0
    order = "Ascending"
    # order = "Descending"
    
    [docker]
    path = "unix:///var/run/docker.sock"
    
    [pager]
    mode = "Auto"
    ```

    The custom config above show with the follow colums:

    `PID, User, TTY, Threads, TCP, VmRSS, Command`

    Here is the running example:

    - Search by TCP port:

        ![procs-search-by-tcpport](./images/procs-search-tcp-port.png)

    - `Or` search by name and sort (desc) by memory usage:

        ![procs-search-name-and-sort-by-memory.png](./images/procs-search-name-and-sort-by-memory.png) <++>
    </br>

