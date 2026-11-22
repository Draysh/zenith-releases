<p align="center">
  <img src="zenith.svg" width="96" height="96" alt="Zenith">
</p>

<h1 align="center">Zenith</h1>

<p align="center">
  Clip the last minute of any game, on Linux and Windows.
</p>

<p align="center">
  <a href="https://github.com/Draysh/zenith-releases/releases/latest"><img src="https://img.shields.io/github/v/release/Draysh/zenith-releases?label=newest%20version&color=3DE0F5&labelColor=02161A" alt="Newest version"></a>
  <a href="https://github.com/Draysh/zenith-releases/releases"><img src="https://img.shields.io/github/downloads/Draysh/zenith-releases/total?label=downloads&color=FF3DA5&labelColor=02161A" alt="Downloads"></a>
</p>

<p align="center">
  <b><a href="https://github.com/Draysh/zenith-releases/releases/latest">Download the newest version</a></b>
  &nbsp;·&nbsp;
  <a href="https://github.com/Draysh/zenith-releases/releases">What changed in each version</a>
</p>

---

A small background recorder keeps a rolling buffer while a game runs. Press
your shortcut and the last seconds are saved as a clip. The app is where you
browse your clips, trim and cut them, and export them at a size that fits
Discord.

- **Light.** The recorder does nothing until a game starts, and capture and
  encoding happen on the graphics card.
- **Three sound tracks.** Game, voice chat and microphone are recorded
  apart, so each can be turned down or muted afterwards.
- **An editor that does not touch your files.** Trim, cut out as many parts
  as you like, undo anything. The original clip stays as it was.
- **Export to a size.** 20 MB for Discord, 50 or 500 MB for Nitro, or any
  size: resolution and frame rate are picked to fit, and the result is
  copied, ready to paste.
- **A library that keeps up.** Clips sorted by game and by day, with
  favourites, tags, notes and search, quick with thousands of clips.
- **No account, and your clips stay on your computer.** The one thing Zenith
  contacts is GitHub, to see whether there is a newer version; that can be
  switched off in the settings.

## Install

### Windows

For 64-bit Windows 10 (version 2004 or later) and Windows 11.

1. From the [newest release](https://github.com/Draysh/zenith-releases/releases/latest),
   download `Zenith-<version>-windows-x86_64-setup.exe`.
2. Run it. It installs for your user only and does not ask for administrator
   rights. Windows may say it does not know the publisher: choose
   "More info", then "Run anyway".
3. Open Zenith from the Start Menu, and pick your clip key in
   Settings → Shortcut.

Everything Zenith needs comes with the setup program.

### Linux

For x86_64, with PipeWire. Zenith uses these, from your distribution's
packages:
[`gpu-screen-recorder`](https://git.dec05eba.com/gpu-screen-recorder/about/),
`ffmpeg`, `mpv` and Qt 6 (`qt6-declarative`). The programs are built on Arch,
so they want a recent Qt 6.

1. From the [newest release](https://github.com/Draysh/zenith-releases/releases/latest),
   download `zenith-<version>-linux-x86_64.tar.gz`.
2. Unpack it and put the files in place:

   ```sh
   tar -xzf zenith-*-linux-x86_64.tar.gz
   install -Dm755 zenithd zenith-clips -t ~/.local/bin
   mkdir -p ~/.local/share/applications
   sed "s|^Exec=zenith-clips\$|Exec=$HOME/.local/bin/zenith-clips|" zenith-clips.desktop \
       > ~/.local/share/applications/zenith-clips.desktop
   install -Dm644 zenithd.service -t ~/.config/systemd/user
   systemctl --user enable --now zenithd
   ```

3. Bind a key to `zenithd save` in your desktop's keyboard settings, and
   open Zenith from the launcher.

`zenithd doctor` says whether everything is in place.

## Updates

Zenith looks here for a newer version and offers to install it; "What is
new" in the app shows that version's notes. Nothing is installed unless it
was signed with Zenith's key, and the check can be switched off in the
settings.

## Check a download yourself

Every file in a release has a `.minisig` signature beside it. With
[minisign](https://jedisct1.github.io/minisign/):

```sh
minisign -Vm zenith-<version>-linux-x86_64.tar.gz -P RWRbpJoO4zv5xIakhl47gZhlVzAgDOk8tGr4aTlTZZ7LBh4HRwdAvPlv
```

## What is in a release

| File | What it is |
|---|---|
| `Zenith-<version>-windows-x86_64-setup.exe` | the setup program for Windows |
| `zenith-<version>-linux-x86_64.tar.gz` | the two programs for Linux, the launcher entry and the service |
| `latest.json` | what installed copies read to see whether there is a newer version |
| `*.minisig` | the signature of the file it is named after |

## Something not working?

In the app, Settings → Setup check → "Copy report" gathers versions, the
setup check and the recorder's last log lines. Paste that into a
[new issue](https://github.com/Draysh/zenith-releases/issues/new) with what
you were doing.

---

<p align="center"><sub>Zenith is free software, under the GPL, version 3 or later.</sub></p>
