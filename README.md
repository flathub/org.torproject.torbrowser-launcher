# Tor Browser Launcher Flatpak

This is the [Tor Browser Launcher](https://gitlab.torproject.org/tpo/applications/torbrowser-launcher) Flatpak.


## Before opening a new issue 

The most common reason why users are tempted to open a new issue is the [Qt](https://www.qt.io/) patch version
changing in `org.kde.Platform`, and downstream flatpaks not catching up with this change.
The maintainers of this flatpak are well aware of this, are tracking this and taking immediate action,
but the maintainers of other packages also have to adapt to this change before the fix here can materialize.
Therefore instead of wasting precious time for yourself and maintainers, consider applying the usual temporary workaround.

### Check logs

If in the logs you find an `ImportError` for `PySide6.QtGui` like many of the previous occurences (
[1](https://github.com/flathub/org.torproject.torbrowser-launcher/issues/180),
[2](https://github.com/flathub/org.torproject.torbrowser-launcher/issues/209),
[3](https://github.com/flathub/org.torproject.torbrowser-launcher/issues/234),
[4](https://github.com/flathub/org.torproject.torbrowser-launcher/issues/235),
[5](https://github.com/flathub/org.torproject.torbrowser-launcher/issues/244)),
then it is almost certain that you could successfully apply the temporary workaround by downgrading the platform.

### Downgrade org.kde.Platform

```bash
QT_MINOR='6.11'
PARENT_COMMIT="$(flatpak --user remote-info --log flathub org.kde.Platform/$(uname --machine)/${QT_MINOR} | awk '/Parent:/{print $2}')"
flatpak update -y --commit="${PARENT_COMMIT}" "org.kde.Platform/$(uname --machine)/${QT_MINOR}"
```
