# Reverie — test builds

A navigable 3D landscape built from a knowledge corpus. Spatial position encodes
learned relatedness, so moving through the world is moving through a topic.

This repository carries the Linux test builds and nothing else. Each release is
one self-contained tarball — engine, native extension and corpus — and needs no
toolchain to run.

## Install

```bash
mkdir -p ~/.local/opt && cd ~/.local/opt
curl -fsSL https://github.com/paul-jo-dreyer/Reverie-distro/releases/latest/download/reverie-linux-x86_64.tar.gz | tar xz
reverie/install.sh
```

`install.sh` is optional: it adds Reverie to the applications menu with its icon
and puts a `reverie` command on the PATH. Without it the build still runs.

```bash
~/.local/opt/reverie/Reverie.x86_64
```

Upgrading is the same two commands. A new tarball unpacks over the old build and
leaves your notes untouched.

## Uninstall

```bash
~/.local/opt/reverie/uninstall.sh            # menu entry, icons, `reverie` command
~/.local/opt/reverie/uninstall.sh --purge    # ... and notes, collections, tutor key
rm -rf ~/.local/opt/reverie                  # the build itself
```

The default keeps everything you made. `--purge` names the directory and its
size, then waits for you to type `delete`.

## Prerequisites

- x86_64 Linux, glibc 2.34 or newer — Ubuntu 22.04, Debian 12, Fedora 35 and
  later.
- A Vulkan driver. Without one the world does not draw, and
  `Reverie.x86_64 --rendering-method gl_compatibility` is the way round it.

A `reverie` command that is not found after installing means `~/.local/bin` is
off your PATH. The menu entry works regardless.

## Local data and network

- Notes, collections and settings are written to
  `~/.local/share/godot/app_userdata/Reverie/`, and nothing outside it.
- Article text is fetched from Wikipedia's API while you read. Offline, the
  reader falls back to the excerpts held in the build. `REVERIE_CONTACT` sets
  the address that identifies you to the API.
- The tutor stays off until you enter an API key in Settings. The key is kept in
  that same directory and goes nowhere but the provider you chose.
