# Git

_**Speed Tip:**_ If the complete repository history isn't needed, then using a shallow clone (`git clone --depth 1`) will save significant time.

```
git clone --depth 1
```

_**On Windows:**_ Two git options are required to check out sources on Windows. Since it's a common source of Git issues on Windows anyway, those options could be set globally (execute those commands before cloning any of intellij-community/android repositories):

```
git config --global core.longpaths true
```

```
git config --global core.autocrlf input
```

---
