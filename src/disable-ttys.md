# Disable TTYs

If you run in `Parallels Desktop`, then you don't need too much `tty` instance.

```bash
doas vim /etc/inittab
```

And then comment out all `ttys` except the `tty1`, as that's the current tty you're login to:

```bash
# Set up a couple of getty's
tty1::respawn:/sbin/getty 38400 tty1
# tty2::respawn:/sbin/getty 38400 tty2
# tty3::respawn:/sbin/getty 38400 tty3
# tty4::respawn:/sbin/getty 38400 tty4
# tty5::respawn:/sbin/getty 38400 tty5
# tty6::respawn:/sbin/getty 38400 tty6
```

Re-login to take affect.

</br>

