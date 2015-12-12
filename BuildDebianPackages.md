## Install build dependencies ##

```
sudo apt-get install build-essential debhelper cmake libboost-python-dev
```

## Fetch sources ##

```
svn checkout http://libarea.googlecode.com/svn/trunk/ libarea
cd libarea
```

## Build package ##

```
dpkg-buildpackage -b -us -uc
```

This will produces 3 packages: libarea0, libarea-dev and python-area.