# My ST Setup

## Custom build of libXFT

The current libXFT build included in the Ubuntu package registry doesn't work well with colored emoji's. St crashes when trying to render a colored emoji due to this feature missing in libXFT.

Clone libXFT:

```sh
https://gitlab.freedesktop.org/xorg/lib/libxft.git
```

If still not merged to master apply patch from this PR: https://gitlab.freedesktop.org/xorg/lib/libxft/-/merge_requests/1

Build library:

```sh
./configure --prefix=/usr --sysconfdir=/etc --disable-static
make
sudo make install
```

Backup current libXFT binary and replace old lib with patched version:

```sh
sudo cp /lib/x86_64-linux-gnu/libXft.a /lib/x86_64-linux-gnu/libXft.a.old

sudo cp /lib/x86_64-linux-gnu/libXft.so.2.3.3 /lib/x86_64-linux-gnu/libXft.so.2.3.3.old

sudo ln -sf /usr/lib/libXft.a /lib/x86_64-linux-gnu/libXft.a 

```

## Create ST gnome icon launcher

/home/[your username]/.local/share/applications, create a “[MyJavaApplication].desktop“

- https://blomsmail.medium.com/how-to-create-an-icon-launcher-for-ubuntu-616a197cb06a
- https://www.reddit.com/r/gnome/comments/g4m4e4/no_icon_on_the_dock_for_simple_terminal_st/fnyk9u2

```
cp st.desktop ~/.local/share/applications
```

## Setting st as default app

```
sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator /usr/local/bin/st 0

sudo update-alternatives --set x-terminal-emulator /usr/local/bin/st
```