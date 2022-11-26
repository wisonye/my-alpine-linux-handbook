# Rust

- Install

    ```bash
    # `curl` is not installed by default
    doas apk --no-cache add curl

    # Install Rust
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

    # Install `rust-analyzer`
    doas apk --no-cache add rust-analyzer
    ```

    </br>



- Install necessary binaries

    ```bash
    cargo install cargo-watch cargo-cache du-dust
    ```

    </br>


    So, you can run `cargo cache --autoclean` to release some spaces.

    </br>


