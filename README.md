# Reverie — test builds

A navigable 3D landscape built from a knowledge corpus. Spatial position encodes
learned relatedness, so moving through the world is moving through a topic.

This repository carries the Linux test builds and nothing else. Each release is
a self-contained tarball: the engine, the native extension and the corpus are
all inside it, and no toolchain is needed to run one.

## Install

```bash
mkdir -p ~/.local/opt && cd ~/.local/opt
curl -fsSL https://github.com/paul-jo-dreyer/Reverie-distro/releases/latest/download/reverie-linux-x86_64.tar.gz | tar xz
reverie/install.sh
```

`install.sh` is optional. It adds Reverie to the applications menu with its icon
and puts a `reverie` command on your PATH; without it the build still runs:

```bash
~/.local/opt/reverie/Reverie.x86_64
```

Upgrading is the same two commands — a new tarball unpacks over the old build
and leaves your notes alone.

## Uninstall

```bash
~/.local/opt/reverie/uninstall.sh            # menu entry, icons, `reverie` command
~/.local/opt/reverie/uninstall.sh --purge    # ... and your notes, collections and tutor key
rm -rf ~/.local/opt/reverie                  # the build itself
```

The default keeps everything you made; `--purge` names the directory and its
size and asks you to type `delete` before removing it.

## What it needs

- x86_64 Linux with glibc 2.34 or newer — Ubuntu 22.04, Debian 12, Fedora 35
  and later.
- A Vulkan driver. Without one the world will not draw, and
  `./Reverie.x86_64 --rendering-method gl_compatibility` is the way round it.

If `reverie` is not found after installing, `~/.local/bin` is not on your PATH.
The menu entry works regardless.

## What it does on your machine

- Writes notes, collections and settings to
  `~/.local/share/godot/app_userdata/Reverie/`, and nothing outside it.
- Fetches article text from Wikipedia's API as you read. Offline, the reader
  falls back to the excerpts held in the build. Set `REVERIE_CONTACT` to an
  address you read to identify yourself to the API.
- The tutor is off until you enter an API key in Settings. The key is kept in
  that same directory and is never sent anywhere but the provider you chose.
