# golang

```shell
# Split files
split -b 50M go-1.24.5-windows.msi go-1.24.5-windows.msi-

# Merge files
cat go-1.24.5-windows.msi-* > go-1.24.5-windows.msi
```
