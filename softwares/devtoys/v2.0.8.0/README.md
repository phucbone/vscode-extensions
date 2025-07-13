# devtoys

```shell
# Split files
split -b 50M devtoys-v2.0.8.0-source.tar.gz devtoys-v2.0.8.0-source.tar.gz-
split -b 50M devtoys-v2.0.8.0-windows-x64-portable.zip devtoys-v2.0.8.0-windows-x64-portable.zip-
split -b 50M devtoys-v2.0.8.0-windows-x86-portable.zip devtoys-v2.0.8.0-windows-x86-portable.zip-
split -b 50M devtoys-v2.0.8.0-windows-x64.exe devtoys-v2.0.8.0-windows-x64.exe-
split -b 50M devtoys-v2.0.8.0-windows-x86.exe devtoys-v2.0.8.0-windows-x86.exe-

# Merge files
cat devtoys-v2.0.8.0-source.tar.gz-* > devtoys-v2.0.8.0-source.tar.gz
cat devtoys-v2.0.8.0-windows-x64-portable.zip-* > devtoys-v2.0.8.0-windows-x64-portable.zip
cat devtoys-v2.0.8.0-windows-x86-portable.zip-* > devtoys-v2.0.8.0-windows-x86-portable.zip
cat devtoys-v2.0.8.0-windows-x64.exe-* > devtoys-v2.0.8.0-windows-x64.exe
cat devtoys-v2.0.8.0-windows-x86.exe-* > devtoys-v2.0.8.0-windows-x86.exe
```
