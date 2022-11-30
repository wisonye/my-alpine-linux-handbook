# About cleaning cache

After running `Alpine Linux` for a while, you will notice that your disk free 
space keeps reducing and never stop, that should be a signal that you should
clean your cache. Usually, it will save over **`GB`** disk space:)

</br>

```bash
# Show how much your cache hold the disk space and remove the bigger you see
dust -d1 ~/.cache

# Remove apk cache if exists
# If you always use `--no-cache`, then it won't be large at all
doas rm -rf /var/cache/apk/*

# Remove cargo cache
cargo cache --autoclean

# After that, calculate again, it should get big improved.
dust -d1 ~/.cache
```
