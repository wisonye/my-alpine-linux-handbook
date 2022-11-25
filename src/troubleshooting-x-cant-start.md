# Troubleshooting of X can't start

### 1. Print the `dmesg`

The first thing first, print the `dmesg` for all error cases:

```bash
doas dmesg -ctime | rg -e fail -e error -e Fail -e Error
```

</br>

Or you if you're focusing on the GPU driver issue, then do this:


```bash
doas dmesg -ctime | rg amd
doas dmesg -ctime | rg intel
```

</br>


### 2. Print the `Xorg.0.log`

```bash
bat ~/.local/share/xorg/Xorg.0.log | rg -e fail -e Fail
```

</br>

