# Firebase-tools

- Install JDK/JRE

    ```bash
    doas apk --no-cache add openjdk11-jre
    ```

    </br>


- Use `npm` to install

    ```bash
    # Latest version
    doas npm install -g firebase-tools

    # Specific version
    doas npm install -g firebase-tools@9.14.0
    ```

    </br>


- You can't just download the GUN Linux binary like this:

    ```bash
    # Download latest version
    curl -Lo ~/my-shell/firebase https://firebase.tools/bin/linux/latest

    # Or download specific version
    curl -Lo ~/my-shell/firebase https://firebase.tools/bin/linux/v9.14.0
    ```

    That's NOT the accetable executable for Alpine Linux which use `musl` static
    link. You can prove that by running `file` and `ldd`:

    ```bash
    file ~/my-shell/firebase
    # ~/my-shell/firebase: ELF 64-bit LSB executable, x86-64, version 1 (GNU/Linux), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=06d669b4b84f03ea5198d36584f920d542ca0ab9, for GNU/Linux 2.6.32, stripped


    ldd ~/my-shell/firebase
    #        /lib64/ld-linux-x86-64.so.2 (0x7f4102d7d000)
    #        libdl.so.2 => /lib64/ld-linux-x86-64.so.2 (0x7f4102d7d000)
    #        libstdc++.so.6 => /usr/lib/libstdc++.so.6 (0x7f4102b2f000)
    #        libm.so.6 => /lib64/ld-linux-x86-64.so.2 (0x7f4102d7d000)
    #        libgcc_s.so.1 => /usr/lib/libgcc_s.so.1 (0x7f4102b11000)
    #        libpthread.so.0 => /lib64/ld-linux-x86-64.so.2 (0x7f4102d7d000)
    #        libc.so.6 => /lib64/ld-linux-x86-64.so.2 (0x7f4102d7d000)
    # Error loading shared library ld-linux-x86-64.so.2: No such file or directory (needed by /home/wison/my-shell/firebase)
    # Error relocating /home/wison/my-shell/firebase: gnu_get_libc_version: symbol not found
    # Error relocating /home/wison/my-shell/firebase: backtrace_symbols: symbol not found
    # Error relocating /home/wison/my-shell/firebase: __register_atfork: symbol not found
    # Error relocating /home/wison/my-shell/firebase: __strdup: symbol not found
    # Error relocating /home/wison/my-shell/firebase: setcontext: symbol not found
    # Error relocating /home/wison/my-shell/firebase: makecontext: symbol not found
    # Error relocating /home/wison/my-shell/firebase: backtrace: symbol not found
    # Error relocating /home/wison/my-shell/firebase: getcontext: symbol not found
    # Error relocating /home/wison/my-shell/firebase: __libc_stack_end: symbol not found
    ```

    </br>

