title: Runit user-side services
summary: A minimal guide for runnit user-level services with runit
authors: Komeil
date: Mar 30, 2026 03:59:53
tags: runit,user-side,services,desystemd,void
slug: runit-user-side-services

A minimal guide for running **user‑level services with runit** without systemd.

This setup allows you to supervise background services in your user session (similar to `systemd --user` units) using a lightweight runit service tree.

---

## Overview

runit can supervise services from any directory.
For user services we create a dedicated service directory and run a user instance of `runsvdir`.

Example layout:

```sh
~/.local/service/
    pipewire/
        run
    wireplumber/
        run
    dunst/
        run
```

Each directory represents one service.

---

## Starting the Supervisor

Run a user service tree with:

```sh
runsvdir -P ~/.local/service
```

This should be started **inside your graphical/session environment** so services inherit variables like:

- `DBUS_SESSION_BUS_ADDRESS`
- `WAYLAND_DISPLAY`
- `XDG_RUNTIME_DIR`

Example (**__niri__** config):

```kdl
spawn runsvdir ~/.local/service
```

---

## Creating a Service

A runit service only needs a `run` script.

Example:

```sh
% kak ~/.local/service/dunst/run  # Or easily you can use `./csrv dunst` for creating this staff
#!/bin/sh
exec dunst
```

Rules:

- always use `exec`
- do not daemonize programs
- do not use `&`

Make it executable:

```sh
chmod +x run
```

The service will start automatically when `runsvdir` sees it.

---

## Managing Services

Use `sv` to control services.

```sh
sv status ~/.local/service/*
sv restart ~/.local/service/dunst  # Yeah, we also have ./sv-user script for this
sv down ~/.local/service/dunst
sv up ~/.local/service/dunst
```

---

## Logging (optional)

Add a logging service:

```
service/foo/log/run
```

Example:

```sh
#!/bin/sh
exec svlogd -tt ./main
```

Logs will appear in:

```
service/foo/log/main/current
```

---

## One‑Shot Services

For tasks that should **not automatically restart**, create a `down` file:

```
touch service/wallpaper/down
```

Run manually:

```
sv up service/wallpaper
```

---

## Tips

- Keep `run` scripts simple.
- Avoid running multiple instances of the same program.
- Separate **core services** (pipewire, portals) from **session services** (notifications, idle managers).
